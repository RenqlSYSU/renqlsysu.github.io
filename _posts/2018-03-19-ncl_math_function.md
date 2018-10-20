---
layout: post
title: ncl常用数学函数
categories: ncl
tags: ncl 整理
author: renql
---

* content
{:toc}

整理ncl中的常用数学函数，如取整、平均、标准化




# 1 数学函数
```
a = b^2   ;平方表述
a = fspan(start, finish, number)   ;Creates an array of evenly-spaced floating point numbers
b = ispan(start, finish, spacing)  ;Creates an array of equally-spaced integer, long, or int64 values.

c = random_normal(av, sd, (/10,100/)) ;Generates random numbers array using a normal distribution.
c = rand() ;Returns a pseudo-random integral value in the range of 0 <= return_val <= 32766.只能生成一个数
```

# 取整函数
```
floor(values)  ;Returns the largest integral value less than or equal to each input value.
;values 可以是一个数或一个数组，此外，若输入的是double，则输出的也是double
；若要得到整数，需用  toint(floor(values))

ceil(values)   ;Returns the smallest integral value greater than or equal to each input value.
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

# 标记函数
```
  x = mask(y, y.lt.100,False)   ;会得到一个和y数组一样大小的x数组，x中相应位置上的y数值若小于100会被设为缺测值，若大于100则是y中该数字
  x = mask(y, y.lt.100,True )   ;与上例相同，只是此时是数值大于100的被设为缺测值
```

