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
可以对数据做纬向傅里叶变换，也可以做时间上的傅里叶变换，得到傅里叶系数。常用的函数有以下三种   
除以下三种外，还有基于复数时间序列的傅里叶变换 `cfftf, cfftb `

## fourier_info
```
finfo = fourier_info(data, nhx, sclPhase) ;返回数组 finfo[3][...][N/2]
;对data的最右边一维做傅里叶变换，返回每个周期对应的振幅、第一个极大值的位置、方差百分比
;其中，振幅即每个周期对应的傅里叶系数的平方和的均方根
;设data最右边一维的长度为N，则分解得到的每个周期中包含的谐波数范围为 (0, N/2]，谐波数值越大，周期越短。
;nhx=0时会返回谐波数分别为 (0, N/2] 时所对应的周期的信息，若 0 < nhx <= N/2，则返回谐波数分别为 (0, nhx] 时所对应的周期信息
;sclPhase其实就是data最右边一维点与点之间的间隔数，若最右边一维是经度，有72个点，则 sclPhase = 360/72 = 5

;注意点：data不能有缺测值，不包括周期点
;此外，该函数也有 fourier_info_n 的形式
```

## ezfftf 向前快速傅里叶变换
```
cf = ezfftf(data) ;返回数组 [2][...][N/2]
;对data最右边一维做傅里叶变换，设其最右边一维的长度为N，返回傅里叶的实部与虚部系数
;同时以属性 xbar 返回data最右边一维的均值，以 npts 返回data最右边一维的长度，最右边一维不需要是2的倍数
;如果有缺测值，计算出来的傅里叶系数为0
```

## ezfftb 向后快速傅里叶变换
其实就是根据傅里叶系数进行合成  
```
data = ezfftb(cf, xbar) 
;cf 即利用 ezfftf 生成的傅里叶系数，其最左边维的长度必须是2，且 cf(0,...) 为实部，cf(1,...) 为虚部
;xbar 是data最右边维的平均数，可以是一个数，也可以是一维数组，长度为 data 右边维数长度的乘积

;利用该函数及 ezfftf 函数可以提取出 data 前几个波数周期的合成
;或者只提取出其中一个波动的曲线
;设现在有一个 data (ntime, nlev, nlat, nlon)
cf = ezfftf (data) ;得到 cf (2, ntime, nlev, nlat, nlon/2)
cf(:,:,:,:,3:nlon/2) = 0.0
cf@xbar = 0
data_wave1_3 = ezfftb (cf, cf@xbar)
```

