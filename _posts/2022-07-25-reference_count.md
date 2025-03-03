---
layout: post
title: reference count问题
categories: python
tags: 易犯错误
author: renql
---

* content
{:toc}

最近发现 python 一个非常操蛋的内存存储问题，好像叫 reference count，一不留心就容易计算失误。

```py
import numpy as np
def diff(a):
    b=a 
    b[1:4]=a[1:4]-a[2:]
    return b
a=np.array([0,2,1,3,4])
c=diff(a)
print(a) # array([ 0,  1, -2, -1,  4])
print(c) # array([ 0,  1, -2, -1,  4])
```

可以看到变量a也发生了变化。问题在于`b=a`这个命令在python中不属于赋值，只是为a多增加了一个索引，a和b都指向同一个内存地址。因此改变b的同时，a也会发生变化。
`b=a[0:2]`numpy数组的切片赋值也存在类似的问题。但列表的切片赋值不存在这个问题。

避免这个问题的解决方法是`b=a.copy()`。或者a进行简单运算后再赋值给b，此时a与b指向不同的内存地址，如下例所示。  

```py
b=a/1.0 # 
b[0]=2
print(b) # array([ 2.,  1., -2., -1.,  4.])
print(a) # array([ 0,  1, -2, -1,  4])
```

xarray中也存在类似的问题，解决方法`b=foo[1:4].data.copy()`。
```py
import xarray as xr
a=np.array([0,2,1,3,4])
foo = xr.DataArray(a, dims=["time"])

b=foo[1:4].data
b[0]=10

print(foo) # foo也发生了变化
# <xarray.DataArray (time: 5)>
# array([ 0, 10,  1,  3,  4])
# Dimensions without coordinates: time

print(b)
# [10  1  3]
```
