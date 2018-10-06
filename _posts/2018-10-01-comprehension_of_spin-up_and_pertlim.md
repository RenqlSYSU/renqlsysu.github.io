---
layout: post
title: 模式spin-up理解及其计算量问题
categories: 模式学习
tags: spin-up pertlim cam4
author: renql
---

* content
{:toc}

## spin-up 模式计算达到平衡
模式中spin-up的时间指，模式从开始计算到能量收支平衡所用的时间。所谓能量收支平衡指模式中输入的总能量（FSNT,Net solar flux at top of model(W/m2),(time,lat,lon))等于输出的总能量（FLNT，Net longwave flux at top of model(W/m2),(time,lat,lon)）。    

以CO2为例。若CO2浓度忽然升高，此时FLNT减少，能量在地球中聚积，温度升高（FLNT增大），对流增加云增多（FSNT减少），于是经过一段时间后，FLNT与FSNT又达到平衡状态，地球温度保持不变。在地球温度对CO2的响应过程中存在滞后，可把这个理解为spin-up的过程。    

其中海洋的响应是比较缓慢的，尤其是在让深层海水变热的过程中。深层地表对温度的响应也是比较缓慢的。但大气对温度的响应则比较快速。**因此全耦合模式（B）spin-up的时间一般大于只有大气的F模式，当然B的计算量是F的两到三倍**。   

CO2缓慢增长到两倍，模式spin-up后的全球平均温度比CO2瞬间增长到两倍高。因为co2缓慢增长的话，其模式会随着co浓度的增长而不断处于调整过程，FLNT小于FSNT的时间长，热量聚积得多。当然也可能存在不确定性，这取决于co2增长速度与模式spin-up速度。

那么，如果地球中的陆地面积增加后，其spin-up的时间与水球spin-up时间相比，哪个长呢？（个人觉得必然是全水球的时间长）在相同CO2浓度的情况下，达到平衡后的温度有什么区别？    

## pertlim
官网解释为——Perturbation limit when doing error growth test  
然后，在实验中通常会在**user_nl_cam**文件中加入`pertlim = 0.01`来为初始场加入一个小扰动，常用于制造集合平均的案例。  

查阅CESM官网论坛，得到如下解释： 

```fortran   
!pertlim is a perturbation you apply to the initial temperature field.
!Usually, you add a perturbation of the order of 1e-14. 
!It is add to the initial temperature field using a random_number generator based on global column index

call random_seed(put=rndm_seed)
	do k = 1, km
		call random_number(pertval)
		pertval = 2.0 *pertlim*(0.5 - pertval)
		t3xy(i,j,k) = t3xy(i,j,k)* (1.0 + pertval)
	end do
```

## cam4，cam5，cam6
cam6的计算量是cam5的四五倍，cam5的计算量是cam4的四五倍。
