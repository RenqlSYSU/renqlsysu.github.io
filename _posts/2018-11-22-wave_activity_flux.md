---
layout: post
title: 瞬变涡旋诊断量
categories: ncl 大气科学
tags: 诊断量
author: renql
---

* content
{:toc}

## 瞬变涡旋诊断量意义
1. **涡旋能量**是一个客观、具有物理动力意义的诊断量，包含瞬变涡旋动能EKE和瞬变涡旋有效位能。其中EKE可以直接反应涡旋环流变率，而EAPE则代表了与气象事件有关的温度波动。
2. **EP通量**只能用于全球纬向平均的二维平面上，等于Rossby群速乘以波活动密度，其辐合辐散也代表局地波活动密度的增加减少。此外，其辐合辐散也可以代表由eddy贡献的纬向平均的径向位涡通量，在EP通量辐合处，有向南的异常位涡的异常输送。
3. **E矢量**可以作为二维EP通量的扩展，其**辐合或辐散**代表着波活动密度的**增加或减少**。其**方向**代表着相对于平均流的Rossby波群速或波动能量传播速度。同时它也能诊断波流相互作用，在E矢量辐合处，西风风速降低。
4. **波活动通量 WAF**，它能根据背景流来量化波能量传播。可以在背景流存在纬向变化情况下，明确描绘瞬变涡旋的传播，其方向于Rossby波群速平行。其辐散或辐合也意味着波包的源或汇。

下面是各诊断量的计算公式及效果图  
![](https://wx4.sinaimg.cn/large/006fa9Xlly1gbx3bgpzpuj30tm0lswj5.jpg)
![](https://wx2.sinaimg.cn/large/006fa9Xlly1gbx3b92r69j30qo04eacr.jpg)
![](https://wx3.sinaimg.cn/large/006fa9Xlly1gbx3bkejpij30ph0k5gvj.jpg)

## 波活动通量算法参考
Nowadays，I am studying how to calculate the wave activity flux by ncl and the its theory as well as its hypothesis.   

Recommended by classmate，there is <a href="http://www.atmos.rcast.u-tokyo.ac.jp/nishii/programs/index.html" target="_blank">a website introducing the algorithm and procedure</a>.  

The algorithm of this website reference the following two papers：   
> Plumb, R. A. (1985). "On the three-dimensional propagation of stationary waves." Journal of the Atmospheric Sciences 42(3): 217-229.

> Takaya, K. and H. Nakamura (2001). "A formulation of a phase-independent wave-activity flux for stationary and migratory quasigeostrophic eddies on a zonally varying basic flow." Journal of the Atmospheric Sciences 58(6): 608-627.

其中，Pb85的文章是基于纬向平均的异常位势高度计算的，另外还用纬向平均的温度来计算位温。  
TN01基于气候态平均的异常位势高度计算，另外还用到daily（or monthly） T, U, V  

```
;  Gas constant
gc=290

;  Gravitational acceleration
ga=9.80665

;  Radius of the earth
re=6378388

; scale height
sclhgt=8000.

; pi
pi = atan(1.0)*4.
; cosine
coslat = cos(lat(:)*pi/180.)
```
