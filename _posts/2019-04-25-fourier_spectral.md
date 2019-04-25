---
layout: post
title: ncl中的傅里叶变换与频谱分析
categories: ncl
tags: Fourier spectral space_time
author: renql
---

* content
{:toc}

# 傅里叶变换
可以对数据做纬向傅里叶变换，也可以做时间上的傅里叶变换，常用的函数有以下三种

## fourier_info
```
finfo = fourier_info(data, nhx, sclPhase) ;返回数组 finfo[3][...][N/2]
;对data的最右边一维做傅里叶变换，返回每个周期对应的振幅、第一个极大值的位置、方差百分比
;其中，振幅即每个周期对应的傅里叶系数的平方和的均方根
;设data最右边一维的长度为N，则分解得到的每个周期中包含的谐波数范围为 (0, N/2]，谐波数值越大，周期越短。
;nhx=0时会返回谐波数分别为 (0, N/2] 时所对应的周期的信息，若 0 < nhx <= N/2，则返回谐波数分别为 (0, nhx] 时所对应的周期信息
;sclPhase其实就是data最右边一维点与点之间的间隔数，若最右边一维是经度，有72个点，则 sclPhase = 360/72 = 5

;此外，该函数也有 fourier_info_n 的形式
```

## ezfftf 向前快速傅里叶变换
