---
layout: post
title: 辐散风和旋转风
categories: ncl 大气科学
tags: 散度涡度 流函数势函数 经圈流函数 整层积分
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
	divg = uv2dvF_Wrap( uwnd, vwnd )
	vort = uv2vrF_Wrap( uwnd, vwnd )
``` 




虽然官网说用球谐函数计算散度和涡度比用中央差分法更精确，但我在用乳源地区的日降水量与涡度散度算相关时，
却发现用球谐函数计算得到的散度和涡度不是很靠谱。  
![](http://wx3.sinaimg.cn/large/006APL3qgy1fosp01jvhkj31j60t14qp.jpg)  
![](http://wx3.sinaimg.cn/large/006APL3qgy1fosp033kxoj31j60ub4qp.jpg)  

# 二、流函数和速度势计算 #  
![](http://wx4.sinaimg.cn/large/006fa9Xlgy1g19omn0hncj30ou0huwka.jpg)   
无辐散流有**流函数**，流函数的拉普拉斯是**涡度**，流函数的高值中心代表反气旋（顺时针），低值中心代表气旋（逆时针）    
无旋转流有**速度势**，速度势的拉普拉斯是**散度**

```
uv2sfvpf ( uwnd, vwnd, stream_function, velocity_potential )  
;calculate stream function and velocity potential via spherical harmonics on a fixed grid
sfvp2uvf ( stream_function, velocity_potential, uwnd, vwnd )
;Computes the wind components given stream function and velocity potential (on a fixed grid) via spherical harmonics.

uv2vrf (uwnd,vwnd,vort)  ;calculate the vorticity via spherical harmonics on a fixed grid   
vr2uvf (vort,ur,vr)      ;calculate the rotational wind components via spherical harmonics on a fixed grid
;ur and vr are the return data 

uv2dvf (uwnd,vwnd,divg)  ;calculate the vorticity via spherical harmonics on a fixed grid   
dv2uvf (divg,ud,vd)      ;calculate the divergent wind components via spherical harmonics on a fixed grid
;ud and vd are the return data 

;the data used by these function must be on a global grid and no missing values    
; If any missing values are encountered in a particular 2D input grid, then all of the values in the corresponding output grids will be set to the missing value
;if there are missing values, you can make the missing value zero by this method
uwnd = where(ismissing(uwnd),0,uwnd)

sf = sf/1000000    ;the stream function's unit is m^2/s, and the magnitude is large, so divided by 10^6
copy_VarMeta(vars,sf(0,0,:,:))
```   

# 三、经圈质量流函数 #  
![](https://image2.slideserve.com/4148663/slide12-n.jpg)    
上图显示的是全球纬向平均的经圈质量流函数的推导过程，一般常用该流函数来研究Hadley环流。其具体计算方案及计算结果如下图所示。   
![]()
![]()

综上，研究Hadley环流的诊断量有以下三种：   
1. 利用径向风计算的全球纬向平均的经圈质量流函数，但它忽略了热带大气环流的区域多样性  
2. The vertical shear of the meridional wind between 200 and 850 hPa (V200–V850)，可以用于研究Hadley环流强度的纬向变化，已有学者利用该诊断量研究Hadley环流的多尺度变率及其与其他气候现象（如ENSO）间的关系。但无法用该指数精确定义Hadley环流的南北边界  
3. 利用辐散风的径向风分量计算的区域纬向平均的经圈流函数，即可以研究Hadley环流的纬向变化，又可以确定Hadley环流的强度及南北范围。但该指数只用到了环流的辐散风分量，无法全面描述环流整体的变化。  

参考文献：
1. Zhang, G. and Z. Wang, 2013: Interannual Variability of the Atlantic Hadley Circulation in Boreal Summer and Its Impacts on Tropical Cyclone Activity. J. Climate, 26, 8529–8544, https://doi.org/10.1175/JCLI-D-12-00802.1   
2. Sun, Y., Li, L.Z.X., Ramstein, G. et al. 2019: Regional meridional cells governing the interannual variability of the Hadley circulation in boreal winter. Clim Dyn, 52: 831. https://doi.org/10.1007/s00382-018-4263-7  
3. Nguyen, H., Hendon, H.H., Lim, E.P. et al. 2017: Variability of the extent of the Hadley circulation in the southern hemisphere: a regional perspective. Clim Dyn, 50: 129. https://doi.org/10.1007/s00382-017-3592-2

ncl计算方法大约有两种：
1. 直接用ncl自带的函数计算 <a href="https://www.ncl.ucar.edu/Document/Functions/Built-in/zonal_mpsi.shtml" target="_blank">zonal_mpsi (v,lat,p,ps) </a> ，但该函数只能计算经圈流函数，且若计算区域经圈环流，需先将径向风的辐散分量计算出来，再利用该函数。  
2. 自己做垂直积分计算。


# 四、可降水量 #
```
	flux = wgt_vert_avg_beta ( shum&level, shum, pres_sfc, punits, opt ) / g ；将比湿垂直积分得到该地区可降水量
	;punits = 0表明shum&level和pres.sfc的单位为hPa或mb；1表明单位为Pa
	;opt = 0 计算各气压层之和；1则计算平均值
```
发现用该函数时，青藏高原地区都是缺测。因此准备换一种计算方法。如下所示

```
  hyai = f->hyai  ;A one-dimensional array equal to the hybrid A coefficients.
  hybi = f->hybi  ;A one-dimensional array equal to the hybrid B coefficients.
  p0   = f->P0  ;A scalar value equal to the surface reference pressure. Must have the same units as ps.
  ps   = f->PS  ;An array of surface pressure data in Pa or hPa (mb). The rightmost dimensions must be latitude and longitude.
  
  dp   = dpres_hybrid_ccm (ps,p0,hyai,hybi)  
  ;Calculates the pressure differences of a hybrid coordinate system Pa [kg/(m s2)]   
  ;the return array will have an additional level dimension compare to PS  
  ;The size of the lev dimension is one less then the size of hyai

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

这里介绍模式的垂直坐标——atmosphere_hybrid_sigma_pressure_coordinate，假设垂直分层30层，则有：  

- **lev（30）**：hybrid level at midpoints (1000*(A+B))，每一层的中间点  
- **hyam（30）**：hybrid A coefficient at layer midpoints   
- **hybm（30）**：hybrid B coefficient at layer midpoints   

- **ilev（31）**：hybrid level at interfaces (1000*(A+B))，每一层的上下界面，故有31层   
- **hyai（31）**：hybrid A coefficient at layer interfaces   
- **hybi（31）**：hybrid B coefficient at layer interfaces   


```
    lev = f->lev  ; (/  1,  2,  3,  5,   7, 10, 20, 30, \
                  ;    50, 70,100,150, 200,250,300,400, \
                  ;   500,600,700,775, 850,925,1000 /)

    Q   = f->Q    ; kg/kg      (time,lev,lat,lon)
    psfc= f->PS   ; PA         (time,lat,lon)
    lev = lev*100
    lev@units = "Pa"    ; to match PS
    ptop= 0             ; integrate 0==>psfc at each grid point

    dp  = dpres_plevel_Wrap(lev, psfc, ptop, 0) 
    ;Calculates the pressure layer thicknesses of a constant pressure level coordinate system,dp(time,lev,lat,lon)
    
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
