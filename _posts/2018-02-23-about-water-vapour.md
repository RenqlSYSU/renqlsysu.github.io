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
