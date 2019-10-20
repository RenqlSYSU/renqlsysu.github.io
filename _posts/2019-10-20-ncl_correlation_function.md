---
layout: post
title: ncl相关系数的计算函数
categories: ncl
tags: ncl
author: renql
---

* content
{:toc}

`esccr(x,y,mxlag)` 计算x和y最右边维的交叉时滞相关，0 <= mxlag <= N/4。如果要算超前滞后相关，需要进行两次运算，如下所示：  
```
 	 mxlag    = 9
	 x_Lead_y = esccr(x,y,mxlag)
     y_Lead_x = esccr(y,x,mxlag)    ; switch the order of the series

     ccr = new ( 2*mxlag+1, float)    
     ccr(0:mxlag-1) = y_Lead_x(1:mxlag:-1)  ; "negative lag", -1 reverses order
     ccr(mxlag:)    = x_Lead_y(0:mxlag)     ; "positive lag"
```

`esacr(x,mxlag)`，计算时滞自相关系数

`escorc(x,y)`，只能计算Pearson同时线性交叉相关

`run_cor(x,y,time,wSize)`,计算滑动相关。使用该函数需要调用一个脚本：  
```
load "$NCARG_ROOT/lib/ncarg/nclscripts/contrib/run_cor.ncl"
```

![](https://wx1.sinaimg.cn/large/006fa9Xlly1g84mcjve3cj30r30esgod.jpg)

<a href="https://wenku.baidu.com/view/fdfece05a6c30c2259019eed.html" target="_blank">更详细版相关系数检验临界值表</a>
