---
layout: post
title: 大气视热源
categories: 大气科学
tags: 热力 
author: renql
---

* content
{:toc}

最近，经常接触**视热源**的这个物理量。例如用**视热源**做滤波及EOF来衡量季节内振荡的传播过程，用**视热源**来衡量TP的热力作用。但始终不知道他是如何计算的，以及为什么要这么做。咨询了师兄师姐后，理解如下：

the vertically integrated atmospheric apparent heat source 整层积分的大气视热源

![](http://wx1.sinaimg.cn/mw690/006fa9Xlgy1fzqrjucw2oj30d40fsn0e.jpg)  
![](http://wx2.sinaimg.cn/mw690/006fa9Xlgy1fzqrjoh6q9j305g03amx4.jpg)

上述公式1是用可观测的变量去估算**垂直扩散加热(感热加热)，大气潜热加热，辐射加热（包括长波短波）**，进而算得大气视热源。因为无法观测到上述三个加热过程，因此需要用可以观测到的风场、温度场去估算。

由于在模式中可以用物理方程求解所有过程，因此上述三个加热过程可以直接用方程计算出来，而不需要用观测资料去估算。  
CESM会默认输出月平均的上述三个加热过程的物理量，如下所示。把他们都加起来再整层积分后得到的值与用上述公式（1）得到的结果差不多。也可以分别看每一项对加热的贡献。

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
