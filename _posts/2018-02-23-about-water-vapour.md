---
layout: post
title: 关于水汽概念的整理
categories: 大气科学
tags: 诊断量
author: renql
---

* content
{:toc}

# 比湿 Specific humidity #
湿空气中的水汽质量与湿空气的总质量之比，单位g/kg或g/g，通常大气中比湿都小于40g/kg。用字母**q**表示。    
![](https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/pic/item/b17eca8065380cd7998acfd0a844ad3459828172.jpg)   
![](https://gss2.bdstatic.com/9fo3dSag_xI4khGkpoWK1HF6hhy/baike/pic/item/d6ca7bcb0a46f21f5cb7326eff246b600c33ae08.jpg)   
式中气压（P）和水汽压（e）须采用相同单位（hPa），比湿q的单位是g/g。

# 水汽混合比 mixing ratio #
湿空气中的水汽质量与干空气质量之比，单位g/kg或g/g，用字母**w**表示。一般认为混合比与比湿近似，但依然存在些许差别。  
![](https://wx4.sinaimg.cn/large/006fa9Xlly1g84qpacae2j30kz01fwea.jpg)  

ncl中有专门的函数将**Specific humidity**和**mixing ratio**进行转换:  
```
   W   = 15.2       ; g/kg      iounit(0)=1
   q   = mixhum_convert(W, "w", (/1,1/)  ; q = 14.97; return g/kg, iounit(1)=1 比湿
   w   = mixhum_convert(q, "q", (/1,1/)  ; w = 15.2 ; return g/kg, iounit(1)=1 混合比
```

# 绝对湿度  Absolute humidity #
标准状况下，每立方米湿空气中所含水蒸气的质量，单位g/m^3




# 相对湿度 Relative humidity #
空气中水汽压与相同温度下饱和水汽压的百分比，或湿空气的绝对湿度与相同温度下可能达到的最大绝对湿度之比。

# 水汽通量 #
表示水汽输送强度的物理量，指单位时间内流经某一单位面积的水汽质量，单位g/(s\*hPa\*m)     
![](http://wx3.sinaimg.cn/mw690/006APL3qgy1foqpf4qsfbj30tm0mswn8.jpg)

可整层积分。

# 水汽通量散度 #
表示输送来的水汽集中程度，指单位时间里，单位体积（底面积1平方厘米，高1hPa）内汇合进来或辐散出去的水汽质量。

![](http://wx2.sinaimg.cn/mw690/006APL3qgy1foqq19xgnpj30vs05q0tk.jpg)

由于大气中的水汽主要集中在对流层的下半部，因此这种计算只要进行到500hPa即可。忽略更高层的水汽输送和水汽通量散度对降水分析影响不大。  

整层水汽水平辐和的大小近似地等于降水率。

# 可降水量 # 
将一地区上空整层大气的水汽全部凝结并降至地面的降水量称为该地区的可降水量，表示该地区整层大气的水汽含量。一般南方可降水量大于北方，海洋大于陆地。       
单位g/(m\*m)    

![](http://wx2.sinaimg.cn/small/006APL3qgy1foqqy1ys0ej308z05sjrb.jpg)

一地区较大的降水量一般远远超过该地区的可降水量，因为由其他地区的水汽向这里输送。

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

