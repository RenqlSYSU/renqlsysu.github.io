---
layout: post
title: ncl中的傅里叶变换与频谱分析
categories: ncl
tags: Fourier spectral space_time
author: renql
---

* content
{:toc}

红噪声是低频长波，其功率谱能量主要集中于低频处  
白噪声是各个频率上的谱密度值相同  

# 傅里叶变换
类似于谐波分析，将序列中的周期性视为正弦波  
可以对数据做纬向傅里叶变换，也可以做时间上的傅里叶变换，得到傅里叶系数。常用的函数有以下三种   

除以下三种外，还有基于复数时间序列的傅里叶变换 `cfftf, cfftb `，当把其中的虚部数值设为0时，其计算结果类似于用 `ezfftf`，但用 `ezfftf` 时得到的频率只有正值，而用 `cfftf` 时可以得到负的频率值，适用于纬向数据，可以得到东传和西传的傅里叶系数，用该函数也可以对经傅里叶变换的傅里叶系数再进行傅里叶变换。  
但用 `cfftf` 计算得到的结果没有标准化，若要得到标准化的结果，需要的输出结果再除以样本数




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

# 功率谱分析
**功率谱分析**以傅里叶变换为基础，将时间序列的总能量分解到不同频率上的分量，根据不同频率波的方差贡献诊断出序列的主要周期，从而确定周期的主要频率。

功率谱分析的步骤：   
1. **原始数据处理，求距平，去趋势**。求距平不会改变数据的总方差，但可以避免突变偏移量，因为在后续的分析步骤中一般会用0来扩充序列。而趋势会在频率为0的地方产生一个功率谱峰值，这个峰值会影响整个功率谱的分布，进而掩盖其他周期。The trend removal is performed first, then the trend-removed data are tapered. This combination minimizes "ringing" and "leakage".  
2. 利用自相关系数或离散傅里叶变换**计算粗谱估计**。  
3. 由于光谱估计的高方差，原始周期图几乎没有直接的用处。原始周期图的波动可以由采样变异性驱动，这个问题在序列越短时就越严重。**平滑原始周期图**可以减少这个问题。如果用不同跨度的Daniell滤波器对原始周期图进行平滑处理，得到的结果是光谱表面更加平滑。置信区间更小。但是过度的平滑会模糊重要的光谱细节，而不充分的平滑会留下不稳定的不重要的光谱细节。   

光谱估计的稳定性是**“从一个序列的不同部分计算出的谱估计在多大程度上是一致的”**或者**“周期图中不相关的精细结构被消除的程度”**。高稳定性对应于低方差的估计，是通过对多个周期图纵坐标求平均得到的。

常用的函数有 `specx_anal`, 交叉功率谱 `specxy_anal`, 功率谱显著性检验`specx_ci`

# Space-time Spectral Analysis
时空谱分析，主要用于研究热带波动。

# 带通滤波
bw_bandpass_filter ( x, fca, fcb, opt, dims )  
- x是需要滤波的数据列，可以是多维数组  
- fca和fcb是滤波范围，一般是时间段的倒数，且两个都必须要小于0.5，按理来说fcb要大于fca，但大小关系反一下问题也不大
- opt是选项，默认情况下是用6阶滤波（opt@m=6），时间间隔为1（opt@dt=1），减去平均值（opt@remove_mean=True），输出滤波后的时间序列（opt@return_filtered=True），不输出滤波后的波包（opt@return_envelope=True）

```
    ua    = f->U_anom(:,{LAT},{LON})   ; ua(time), read from one grid point

    ca    = 50.0        ; band start (longer period)
    cb    = 40.0        ; band end （时间间隔不能等于2）

    fca   = 1.0/ca      ; 'left'  frequency
    fcb   = 1.0/cb      ; 'right' frequency

    dims  = 0           ; 'time' dimension of ua  

    opt   = True        ; options to set
    opt@return_envelope = True ; time series of filtered and envelope values

    ua_bf = bw_bandpass_filter (ua,fca,fcb,opt,dims)       ; (ua,fca,fcb,opt,dims)
    copy_VarMeta(ua, ua_bf)
    ua_bf@long_name = "Band Pass: "+cb+"-"+ca+" day"
```

计算得到的结果示意如下，其中上图是原始序列，下图是滤波后的时间序列（蓝色）与波包（红色）  
![](https://www.ncl.ucar.edu/Document/Functions/Images/dim_bfband_20-100.ex01.png)
![](https://www.ncl.ucar.edu/Document/Functions/Images/dim_bfband_40-50.ex01.png)

http://www.seismosoc.org/Publications/BSSA_html/bssa_96-2/05055-esupp/
