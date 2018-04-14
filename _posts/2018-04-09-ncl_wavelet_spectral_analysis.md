---
layout: post
title: ncl时频分析函数
categories: ncl
tags: ncl 整理 小波分析
author: renql
---

* content
{:toc}

## 小波分析
利用小波分析，可以得到一个时间序列里任意周期的振幅及该振幅随时间变化的情况。

```
wave = wavelet(data, mother, dt, param, s0, dj, jtot, npad, noise, isigtest, siglvl, nadof) ;ncl用于小波分析的计算函数
```
1. **data**，一维数组，用于进行小波分析的序列   
2. **mother**，整数，用于选择小波分析所使用的母小波函数，0 = Morlet，1 = Paul，2 = DOG (derivative of Gaussian)，
若该值大于2或小于0，则默认为‘Morlet’，多数情况下都用Morlet   
3. **dt**，序列的时间间隔，多数情况下为1   
4. **param**，表示母小波函数的参数（必须大于0），若小于0 则使用默认值。   
对于Morlet，该参数即波数，默认为6；对于Paul，改参数为order，默认为4；对于DOG，该参数为导数阶数，默认为2.   
5. **s0**，能进行小波分析的最小规模，多数为2*dt。为了更精确地计算，对于Morlet，s0 = dt；对于Paul，s0 = dt/4。  
6. **dj**，离散尺度之间的间距，一般为0.25。该值越小，尺度分辨率越高，但计算更慢。   
7. **jtot**，整数，能分析的尺度数量，一般尺度取值范围为`s0`至`s0*2^[(jtot-1)*dj]`。
因此，一般 `jtot = 1 + floattointeger( ( (log10(N*dt/s0)) /dj) /log10(2.) )`   
8. **npad**，整数，用于小波分析的序列样本数    
9. **noise**，整数，0表示用白噪音进行显著性检验；1表示用红噪音进行显著性检验，多数情况下用1    
10. **isigtest**，整数，0表示do a regular chi-square test，1表示do a "time-average" test on the global wavelet spectrum    
11. **siglvl**，显著性检验水平，一般为0.05    
12. **nadof**，设为0，暂时忽略其作用    




该函数运行后返回一数值类型同data的三维数组wave（2，jtot，npad），（0，：，：）是实部，（1，：，：）是虚部。该数组包含如下一些有用的属性：    
1. **wave@power**，功率谱，长为 jtot*npad 的一维数组，相当于 `wave(0,:,:)^2 + wave(1,:,:)^2`，
可通过 `power = onedtond (wave@power, (/jtot,npad/) ) `转换为二维数组   
2. **wave@phase**，位相，长为 jtot*npad 的一维数组，相当于 atan2(wave(1,:,:),wave(0,:,:))
3. **wave@mean**，用于小波分析序列的平均值
4. **wave@stdev**，用于小波分析序列的标准差
5. **wave@scale**，A one-dimensional array of length jtot (same type as wave) containing the wavelet scales that were used.
`scale = so*2^[(jtot-1)*dj]`   
6. **wave@period**，A one-dimensional array of length jtot (same type as wave) containing the "Fourier" periods (in time units) corresponding to "scale".    
7. **wave@signif**，A one-dimensional array of length jtot (same type as wave) containing significance levels versus scale.    
8. **wave@gws**，A one-dimensional array of length jtot (same type as wave) containing the global wavelet spectrum.     
9. **wave@coi**，A one-dimensional array of length N (same type as wave) containing the e-folding factor used for the cone of influence.是画边界区域必须的参数    
10. **wave@cdelta**，A scalar (same type as wave) containing the constant "Cdelta" for the mother wavelet (Table 2 of reference).     
11. **wave@psi0**，A scalar (same type as wave) containing the constant "psi(0)" for the mother wavelet (Table 2 of reference).

 ```    
 ;计算显著性水平
  SIG  = power           ; transfer metadata
  SIG  = power/conform (power,w@signif,0)  ; >= 1 is significant
  
  ;计算无偏差的小波功率谱，可以突出小尺度的功率谱值
  power = onedtond (wave@power, (/jtot,npad/) ) 
  power_no_bias = power/conform(power,wave@scale,0)
  gws_no_bias   = wave@gws/wave@scale
  
  ;如何画边界区域的曲线
  rescoi = True
  rescoi@gsFillIndex  = 1 ;确定填充类型  
  ;只要是gs开头的属性均可设置，另外还可以设置gsFillColor，gsEdgeColor，gsEdgeDashPattern，gsEdgeThicknessF
  plot = ShadeCOI(wks, plot, wave, data&time,rescoi)
  ```    
   
  其中函数 `conform` 是用于扩展数组的，其用法介绍如下
  ``` 
  data  = conform(x, r, ndim) ;将数组r扩充为和数组x同等大小的数组
  ;x，任何维数的数组
  ;r，一个值或一个数组，但这个数组必须是X的子集
  ;ndim，表明X的哪几维是与r相同的，若r是一个值，则ndim设为-1
  ```

无偏差的小波分析    
>  Liu Y (2007),Rectification of the bias in the wavelet power spectrum,Journal of Atmospheric and Oceanic Technology, 24(12), 2093-2102.


