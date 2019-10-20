---
layout: post
title: Wave Activity Flux
categories: ncl 大气科学
tags: 诊断量
author: renql
---

* content
{:toc}

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
