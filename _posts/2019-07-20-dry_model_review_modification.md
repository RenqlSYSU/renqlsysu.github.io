---
layout: post
title: 简单模式动力设置和几种修改方法
categories: 文献笔记 模式学习
tags: model
author: renql
---

* content
{:toc}

发现有很多跑简单模式的文献，准备收集整理一下，以资参考。

## Held-Suare 1994年的基本设置 ##
> Held, I. M. and M. J. Suarez (1994). “A proposal for the intercomparison of the dynamical cores of atmospheric general circulation models.” Bulletin of the American Meteorological Society 75(10): 1825-1830.

觉得如果要修改CESM干模式的动力核，还是有必要把这篇经典的文章再读一遍。

为了评估大气环流模式独立于物理参数化的动力核，该文设计了一个基准实验。这个实验关注模式结果的长期统计特征，因此非常适合于气候模式的动力核比较
为了说明这个基准实验的用处，两个完全不同的大气动力核（谱模式、差分格式）用于比较。

利用牛顿松弛方法来施加强迫，当温度低于给定的辐射平衡温度时加热，反之则冷却。同时在风场底层（sigma>0.7的地方，sigma值为1时代表地表）用瑞利阻尼的方法来模拟边界层摩擦效应。  
![](http://wx2.sinaimg.cn/mw690/006fa9Xlgy1g5647vd178j30i30l0ju2.jpg)

其中辐射的松弛时间（Ka或者Ks的倒数）也是一个关于纬度和高度的函数，在sigma<0.7也就是大气内部，松弛时间是40天，而赤道地区近地表的松弛时间最短是4天。如果各个地方都用统一的松弛时间，那么会在近地表区域产生一个不真实的薄冷层，尤其在赤道地区。因此赤道地区的松弛系数较大（即松弛时间短），以减弱这种效应。

那么为什么会在底层产生一个不真实的冷区呢？我的猜想是：在没有地表摩擦消耗时，因为赤道的辐射平衡温度高，本身就存在环流。而地表摩擦的存在使得底层的能量存在耗散，为了维持环流的存在，就必须使地表温度弱于辐射平衡温度，以产生加热。  
![](http://wx1.sinaimg.cn/mw690/006fa9Xlgy1g5647w2rrhj31040u0nnl.jpg)

实验的目的不是为了产生了真实的大气环流，而是为了在可解析的所有尺度上更好地模拟大气运动。

## Schneider 2008年 加入辐射强迫的年循环 ##
Although the resulting Newtonian temperature relaxation rate is not easily justifiable as a radiative heating rate, we will call it, for simplicity, a radiative heating rate

![](http://wx2.sinaimg.cn/mw690/006fa9Xlgy1g564mg8kaqj30cz07g3zt.jpg)  
![](http://wx2.sinaimg.cn/mw690/006fa9Xlgy1g564mgv0pmj30d507kmyu.jpg)  
![](http://wx2.sinaimg.cn/mw690/006fa9Xlgy1g564mha15oj30cy0brq5q.jpg)  
