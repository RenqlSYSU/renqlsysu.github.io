---
layout: post
title: 大气视热源
categories: 大气科学
tags: 诊断量
author: renql
---

* content
{:toc}

最近，经常接触**视热源**这个物理量。例如用**视热源**做滤波及EOF来衡量季节内振荡的传播过程，用**视热源**来衡量TP的热力作用。但始终不知道他是如何计算的，以及为什么要这么做。咨询了师兄师姐后，理解如下：

the vertically integrated atmospheric apparent heat source 整层积分的大气视热源  
下图选自论文《Interactions between boreal summer intraseasonal oscillations and synoptic-scale disturbances over the western North Pacific. Part II: Apparent heat and moisture sources and eddy momentum transport》  
![](https://camo.githubusercontent.com/84ad37af17aa8e6cc78fc4401d36582681863e6378b6a1bd0d1d54e03f93ee71/68747470733a2f2f73332e617831782e636f6d2f323032302f31322f30342f4471305563382e6a7067) 
![](https://camo.githubusercontent.com/c21ee09a32f5f0fc8762b6f4120f6111f496742d8a37ae5877a597ce395caac1/68747470733a2f2f73332e617831782e636f6d2f323032302f31322f30342f4471304e31662e6a7067)

上述公式1是用可观测的变量去估算**垂直扩散加热(感热加热)，大气潜热加热，辐射加热（包括长波短波）**，进而算得大气视热源。因为无法观测到上述三个加热过程，因此需要用可以观测到的风场、温度场去估算。其中垂直速度是p坐标系下的垂直速度（单位Pa/s)。Cp一般取 **1004.0 J/(K kg)** ，所以计算得到的视热源单位 **W/kg**，整层积分后的单位是 **W/m2**。

此外，计算时注意用**逐日的风场、温度资料**来计算，不能用气候平均的UVT来计算，那样会忽略瞬变涡旋的热通量，如下面的公式所显示的那样（下面的非绝热加热忽略了温度的时间变化率，因为这一项一般都比较小，可以忽略。此外该非绝热加热乘以Cp后即视热源）。听说，**对于热带这些瞬变涡旋作用很弱的地区，可以用气候平均的UVT来计算**   
![](https://s1.ax1x.com/2020/08/31/dLj2u9.png)

由于在模式中可以用物理方程求解所有过程，因此上述三个加热过程可以直接用方程计算出来，而不需要用观测资料去估算。  
CESM会默认输出月平均的上述三个加热过程的物理量，如下所示。把他们都加起来乘以Cp再整层积分后得到的值与用上述公式（1）得到的结果差不多。也可以分别看每一项对加热的贡献。

```
    float QRL(time, lev, lat, lon) ;
        QRL:mdims = 1 ;
        QRL:Sampling_Sequence = "rad_lwsw" ;
        QRL:units = "K/s" ;
        QRL:long_name = "Longwave heating rate" ;
        QRL:cell_methods = "time: mean" ;

    float QRS(time, lev, lat, lon) ;
        QRS:mdims = 1 ;
        QRS:Sampling_Sequence = "rad_lwsw" ;
        QRS:units = "K/s" ;
        QRS:long_name = "Solar heating rate" ;
        QRS:cell_methods = "time: mean" ;

    float DTCOND(time, lev, lat, lon) ;
        DTCOND:mdims = 1 ;
        DTCOND:units = "K/s" ;
        DTCOND:long_name = "T tendency - moist processes" ;
        DTCOND:cell_methods = "time: mean" ;

    float DTV(time, lev, lat, lon) ;
        DTV:mdims = 1 ;
        DTV:units = "K/s" ;
        DTV:long_name = "T vertical diffusion" ;
        DTV:cell_methods = "time: mean" ;
```

两种计算方法的对比
![](https://camo.githubusercontent.com/8e3014c18bdd365dacfd2a492f24beeaba5bd48c3f04edc10af4a7ba83692b77/68747470733a2f2f73332e617831782e636f6d2f323032312f30332f31322f36554f7835712e706e67)

他们的垂直分布如下（第一张图是模式输出资料，第二张图是由温度和风场反算的结果，色标一致，均未乘Cp）   
![](https://s3.ax1x.com/2021/03/12/6UOvan.png)  
![](https://s3.ax1x.com/2021/03/12/6UOjVs.png)  

