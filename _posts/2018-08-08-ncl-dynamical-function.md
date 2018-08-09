---
layout: post
title: ncl常用动力学函数整理
categories: ncl
tags: ncl 动力气象 整理
author: renql
---

* content
{:toc}

# 一、散度涡度 divergence and vorticity #
```
；以下是用中央差分的方法计算涡度散度
	divg = uv2dv_cfd ( uwnd, vwnd, uwnd&lat, uwnd&lon, scalar-integer )
	vort = uv2vr_cfd ( uwnd, vwnd, uwnd&lat, uwnd&lon, scalar-integer )
	;scalar-integer设为0，边界点都将设为缺测值；
	;1，则uwnd和vwnd在经度上刚好围城一个圆，此时设置上边界和下边界为缺测值；
	;2，边界点用单向差分法估计；
	;3，uwnd和vwnd在经度上刚好围成一个圈，无重复点，此时上边界和下边界分别用单向差分法估计。
	
；以下是用球谐函数 spherical harmonics 的方法计算涡度散度，  
；用球谐函数计算得到的散度和涡度比中央差分计算得到的值更精确。  
；但只有只有当输入的风场是全球风场且无缺测值时方可使用球谐函数计算。  
	uv2vrdvf ( uwnd, vwnd, vort, divg ) ;计算涡度和散度，括号中后两个值是返回值。  
	uv2sfvpf ( uwnd, vwnd, stream_function, velocity_potential )   
	divg = uv2dvF_Wrap( uwnd, vwnd )
	vort = uv2vrF_Wrap( uwnd, vwnd )
``` 




虽然官网说用球谐函数计算散度和涡度比用中央差分法更精确，但我在用乳源地区的日降水量与涡度散度算相关时，
却发现用球谐函数计算得到的散度和涡度不是很靠谱。  
![](http://wx3.sinaimg.cn/large/006APL3qgy1fosp01jvhkj31j60t14qp.jpg)  
![](http://wx3.sinaimg.cn/large/006APL3qgy1fosp033kxoj31j60ub4qp.jpg)  

# 二、流函数和速度势计算 #  
![](http://wx2.sinaimg.cn/large/006fa9Xlgy1fu2kqef91zj30lc0clq36.jpg)   
流函数的高值中心代表气旋，低值中心代表反气旋   
一般情况下，为查看风场的气旋反气旋情况，会用旋衡风分量计算流函数   
```
uv2vrf(uwnd,vwnd,vort)  ;calculate the vorticity via spherical harmonics on a fixed grid   
vr2uvf(vort,ur,vr)      ;calculate the rotational wind components via spherical harmonics on a fixed grid    
uv2sfvpf(ur,vr,sf,vp)   ;calculate stream function and velocity potential via spherical harmonics on a fixed grid
;the data used by these function must be on a global grid and no missing values    
;if there are missing values, you can make the missing value zero by this method
uwnd = where(ismissing(uwnd),0,uwnd)

sf = sf/1000000    ;the stream function's unit is m^2/s, and the magnitude is large, so divided by 10^6
copy_VarMeta(vars,sf(0,0,:,:))
```   

# 三、经圈质量流函数 #  
![](https://image2.slideserve.com/4148663/slide12-n.jpg)    
除水平流函数外，还有经圈环流的质量流函数，可方便查看Hadly环流，但目前还未研究出其具体计算方法。
但绝对不是水平流函数的**高度-经度剖面图**


# 四、可降水量 #
```
	flux = wgt_vert_avg_beta ( shum&level, shum, pres_sfc, punits, opt ) / g ；将比湿垂直积分得到该地区可降水量
	;punits = 0表明shum&level和pres.sfc的单位为hPa或mb；1表明单位为Pa
	;opt = 0 计算各气压层之和；1则计算平均值
```
发现用该函数时，青藏高原地区都是缺测。因此准备换一种计算方法。如下所示

```
  hyai = f->hyai
  hybi = f->hybi
  p0   = f->P0
  ps   = f->PS
  dp   = dpres_hybrid_ccm (ps,p0,hyai,hybi)  
  ;Calculates the pressure differences of a hybrid coordinate system Pa [kg/(m s2)]   

  T    = f->T                                ; K  (time,lev,lat,lon)
  cp   = 1004.                               ; J/(K kg)     [ m2/(K s2) ]
  g    = 9.81                                ; m/s
  
  Tdp  = T*dp                                ; [K kg/(m s2)]   (temporary variable)
  copy_VarCoords(T, Tdp)
  IE   = dim_sum_n_Wrap( Tdp, 1) 	     ;Vertically Integrated Internal Energy (time,lat,lon)
  IE   = cp*IE/g                             ; kg/s2  
  IE@long_name = "Vertically Integrated Internal Energy"
  IE@units     = "kg/s2"
```

```
    lev = f->lev  ; (/  1,  2,  3,  5,   7, 10, 20, 30, \
                  ;    50, 70,100,150, 200,250,300,400, \
                  ;   500,600,700,775, 850,925,1000 /)

    Q   = f->Q    ; kg/kg      (time,lev,lat,lon)
    psfc= f->PS   ; PA         (time,lat,lon)
    lev = lev*100
    lev@units = "Pa"    ; to match PS
    ptop= 0             ; integrate 0==>psfc at each grid point

    dp  = dpres_plevel_Wrap(lev, psfc, ptop, 0) ;Calculates the pressure layer thicknesses of a constant pressure level coordinate system,dp(time,lev,lat,lon)
                        ; latent heat of vaporization at 0C
    L   = 2.5e6         ; J/kg         [ m2/s2 ]
    g   = 9.81          ; m/s
    
    Qdp = Q*dp          ; temporary variable               
    copy_VarCoords(Q, Qdp)                   
    LE  = dim_sum_n_Wrap( Qdp,1 )   ; integrate vertically [level dimension = 1],  LE(ntim,nlat,mlon)
    LE  = (L/GR)*LE     ; (time,lat,lon)
    LE@long_name = "Latent Energy:  SUM[L*Q*dp]/g"
    LE@units     = "kg/s2"
```
