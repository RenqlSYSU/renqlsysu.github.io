---
layout: post
title: ncl切面图画法
categories: ncl
tags: ncl 绘图函数 整理
author: renql
---

* content
{:toc}

整理切面图包括**纬度-时间剖面图**，**经度-时间剖面图**，**高度-经度剖面图**，**高度-纬度剖面图**以及一些特殊的绘图函数。




# 特殊的绘图函数
## 只画某些等值线内的内容
```
res@gsnShadeFillType    = "color" or "pattern" 
res@gsnShadeFillScaleF  = 当fill type 为 pattern时，浮点数，数值大于1时，值越大，填充的形状数量越疏
res@gsnShadeLow     = a pattern or color index    ;用于填充等值线小于lowval的区域，若不设置则该区域不填充
res@gsnShadeMid     = a pattern or color index    ;用于填充等值线介于lowval和highval的区域，若不设置则该区域不填充
res@gsnShadeHigh    = a pattern or color index    ;用于填充等值线大于highval的区域，若不设置则该区域不填充
plot = gsn_contour_shade(plot, lowval, highval, res )  ;lowval和highval都是一个数值
;该函数是叠加在已有的图（但该图并没有draw和frame）之上
```
## 只画通过显著性检验的数据
```
var(var,prob.lt.siglvl,True) ;prob是统计概率值，维数与var相同，若siglvl为0.05，则未通过95%显著性检验的数据将被设置为缺测值
```

在用prob画显著性区域时，一定要先设置prob的lat和lon坐标，否则显著性区域会与实际不符 ``` copy_VarMate(var,prob) ```

# 纬度(经度）-时间剖面图
```
plot = gsn_csm_lat_time( wks, data, res ) ;data必须为（lat，time）的二维数组
plot = gsn_csm_time_lat( wks, data, res ) ;data必须为（time，lat）的二维数组
plot = gsn_csm_hov( wks, data, res)       ;data必须为（time，lon）的二维数组
```   
If the resource cnFillOn is set to True, then the following will happen automatically:   
- a labelbar will be automatically added (default horizontal)  
- contour line labels will be turned off  
- the contour information label will be turned off  
If you want to turn the labelbar off, set lbLabelBarOn to False.  

一般时间坐标是从0开始的数字，若要表示具体的年月日，需要自己指定横坐标
```
res@tmYLMode = "Explicit" 
res@tmYLValues = (/ 0. , 30., 61., 89., 120., 150. /)
res@tmYLLabels = (/"DEC","JAN","FEB","MAR","APR","MAY" /)
```
