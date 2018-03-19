---
layout: post
title: ncl常用数学函数
categories: ncl
tags: ncl 整理
author: renql
---

* content
{:toc}

# 取整函数
```
floor(values)  ;Returns the **largest** integral value less than or equal to each input value.
;values 可以是一个数或一个数组，此外，若输入的是double，则输出的也是double
；若要得到整数，需用  toint(floor(values))

ceil(values)   ;Returns the **smallest** integral value greater than or equal to each input value.
;values 可以是一个数或一个数组，此外，若输入的是double，则输出的也是double

;上述函数可以用来设置纵坐标的取值范围
  res@trYMinF = toint(floor(min(var)))
  res@trYMaxF = toint( ceil(max(var)))
  
round(values,opt)  ;Rounds a float or double variable to the nearest whole number.类似于四舍五入
;valus可以是任意纬度
;opt=0: return values of the same type as x
;opt=1: return values of type float
;opt=2: return values of type double
;opt=3: return values of type integer

```
