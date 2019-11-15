---
layout: post
title: 关于缺测
categories: ncl
tags: 数据
author: renql
---

* content
{:toc}

发现再分析资料中一般是没有缺测的，即便在青藏高原，1000hPa也依然有值。  
但模式输出的资料中，在有地形或地表气压低于1000hPa的地方，1000hPa等压面上就会有缺测值，因此模式陆地底层经常有大片区域的缺测。  
当利用模式资料算一些比较复杂的诊断量时要注意缺测值。  

## ncl中关于缺测的处理
ncl中的缺测值用 var@_FillValue 表示。
```
b = ismissing(a) ;当数组a中含有缺测值时，相应位置就会返回 True
c = where( ismissing(a), 0, a ) ;把数组a中的缺测值用0代换
c = where( a.eq.a@_FillValue, 0, a )  ;按理来说效果同上，但实践证明这样不行

if(all(ismissing(data))) then
    print("Your data is all missing. Cannot create plot.")
end if

if(any(ismissing(data))) then
    print("Your data contains some missing values. Beware.")
end if

N = num(.not.ismissing(data)) ;统计非缺测值数量，同理也可统计缺测值数量
;num 的作用是 Counts the number of True values in the input.
```

使用ncl函数时一定要看清楚该函数对缺测值的处理方法。   
- 自动忽略缺测值的函数： `dim_avg_n, dim_sum_n`    
- 把缺测值当正常值处理的函数：ncl的加减乘除、 `bw_bandpass_filter` 
