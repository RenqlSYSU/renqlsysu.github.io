---
layout: post
title: 大气位温、相当位温、饱和相当位温、静力稳定度
categories: ncl 大气科学
tags: 诊断量
author: renql
---

* content
{:toc}

## 位温 potential temperature ##
**位温**把干空气块绝热膨胀或压缩到标准气压（1000hPa）时的温度。在干绝热过程中具有**守恒性**，即一个气块的位温不随气块所处的高度或压强的改变而改变，而温度是非保守性的物理量，会随着气块的位置或压强的改变而变化。与温度相比**位温是一种稳定的示踪物**，方便我们追溯气块或气流的源地及研究他们以后的演变。

空气块受热位温上升，空气块放热时位温降低，干绝热过程位温保持不变  
位温的垂直分布：在对流层内，一般大气的垂直减温率小于干绝热减温率，所以位温随高度增加而增加。

未饱和湿空气的位温计算公式：  
![](https://gss3.bdstatic.com/7Po3dSag_xI4khGkpoWK1HF6hhy/baike/pic/item/a2cc7cd98d1001e9769209b0bc0e7bec55e797e6.jpg)
![](https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/pic/item/79f0f736afc37931c2c29e96efc4b74542a911e2.jpg)

ncl的计算：
```
opt   = False
theta = pot_temp(pres_Pa, temp_K, dim, opt)
;The dimension of temp_K which corresponds to pres_Pa
;opt这个选项目前还没有开发到，直接设为 False
```
使用该函数的时候，记得检查各变量的单位，必须使用函数要求的单位（Pa和K）。

若输入的温度为**相当温度 equivalent temperature**，则也可以计算相当位温，但感觉这样计算的相当位温同用函数`pot_temp_equiv`计算的，会低估。相当温度可以用下面的代码计算：  
```
cpd  = 1004. or 1005.7 ; specific heat dry air [J/kg/K]
Lv   = 2.5104e6        ; [J/kg]=[m2/s2]  Latent Heat of Vaporization of Water
r    = mixing_ratio    ; [kg/kg]; same size and shape as t 
teqv = t + (Lv/cpd)*r  ; equivalent temperature 
```

## 相当位温 equivalent potential temperature ##
**相当位温**是某一高度的气团下降（或上升）至参照气压值的位置时，经过绝热膨胀（或收缩）以及所含的水汽全部凝结为水滴释出潜热后，所具有的温度。一般适用于饱和湿空气，在饱和湿绝热过程中守恒。

**假相当位温**是饱和（或未饱和）湿空气块在绝热上升（先是干绝热上升到凝结高度，然后再湿绝热上升）过程中，在气块本身维持饱和的状态下，凝结出来的液态水立即脱离上升气块，直到该空气块所具有的水汽全部凝结完毕并脱落以后，该空气块所具有的位温。

个人感觉**相当位温和假相当位温是同一个物理量**，都是把**温度、气压、湿度**包括在一起的一个综合物理量。在ncl中，计算相当位温的函数的计算过程等同于假相当位温。

对于干绝热、湿绝热、假绝热过程，假相当位温都保持守恒。

ncl的计算：
```
;利用抬升凝结温度计算相当位温
theta_e = pot_temp_equiv_tlcl(pres, temp, tlcl, mixr, iounits)
;tlcl抬升凝结温度的单位同temp温度，四个数组的维数最好一样吧
;iounits是有四个数值的一维数组，用来说明各变量单位
;输出结果的维数同temp

;抬升凝结温度的计算有四种方法（就是用四种不同的变量计算tlcl）
tlcl = tlcl_mixr_bolton(temp, mixr, p, iounits) ;利用混合比计算tlcl
tlcl = tlcl_rh_bolton  (temp, rh, iounits)      ;利用相对湿度计算tlcl
tlcl = tlcl_evp_bolton (temp, evp, iounits)     ;利用水汽压计算tlcl
tlcl = tlcl_td_bolton  (temp, td, iounits)      ;利用露点温度计算tlcl
;函数中的所有数组的维数必须相同

;不用抬升凝结温度，直接估算相当位温，据说会存在系统性低估
theta_e = pot_temp_equiv(pres_Pa, temp_K, water, dim, humVarType)
;dim表示temp_K中的哪一维同pres_Pa,若这两个变量的维数相同，dim=-1
;humVarType是一个字节变量，表示water中具体选用哪一个与水汽有关的物理量，"r"表示用比湿(kg/kg)
```

因此，计算假相当位温需要变量：**气压**、**温度**、**混合比**（可以用比湿换算）。   
关于各水汽变量的概念，参考这篇博文 <a href="https://renqlsysu.github.io/2018/02/23/about-water-vapour/" target="_blank">https://renqlsysu.github.io/2018/02/23/about-water-vapour/</a>

## 饱和相当位温 Saturation equivalent potential temperature ##
当空气处于饱和状态时计算得到的相当位温。在相同温度和压强情况下，饱和相当位温大于相当位温。

## 广义位温 ##
位温适用于干空气，相当位温适用于饱和湿空气，那么广义位温适用于未饱和的湿空气状态，由曹洁和高守亭于2008年提出，计算公式如下：   
![](https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/pic/item/cf1b9d16fdfaaf51a3dc8800885494eef01f7a55.jpg)

感觉这个不如**假相当位温**好用

## 静力稳定度 ##
**静力稳定度**由密度或位温的垂直分层情况所决定。  

本来研究位温的计算就是为了计算静力稳定度（或对流不稳定指数），结果发现ncl就有计算静力不稳定的函数，所以一起看一下吧。发现输入的数据同位温函数`pot_temp`的计算。
```
sopt = 1
s1   = static_stability(press_Pa, temp_K, dim, sopt)

; explicitly extract each variable from the list
S1_s     = S1[0]   ; static stability
S1_pt    = S1[1]   ; theta
S1_dthdp = S1[2]   ; d(theta)dp

;The dimension of temp_K which corresponds to pres_Pa
;sopt=0, Return static stability only
;sopt=1, Return static stability, theta, d(theta)dp as type list
;使用的公式是 s = -T*d[log(theta)]/dp = -(T/theta)*d(theta)/dp
```

参考以下文献，**静力稳定度**指数可以用925hPa和600hPa的相当位温之差表示，值越大表明大气越不稳定。**对流不稳定**指数可以用925hPa的相当位温与500hPa的饱和相当位温之差。差值为正，表示对流不稳定。  
> Sampe, T. and S.-P. Xie (2010). Large-Scale Dynamics of the Meiyu-Baiu Rainband: Environmental Forcing by the Westerly Jet. Journal of Climate. 23: 113-134.  

## 参考资料 ##
1. https://baike.baidu.com/item/%E4%BD%8D%E6%B8%A9  
2. https://baike.baidu.com/item/%E5%81%87%E7%9B%B8%E5%BD%93%E4%BD%8D%E6%B8%A9  
3. https://baike.baidu.com/item/%E7%9B%B8%E5%BD%93%E4%BD%8D%E6%B8%A9  
4. http://glossary.ametsoc.org/wiki/Saturation_equivalent_potential_temperature  
