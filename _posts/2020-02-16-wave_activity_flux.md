---
layout: post
title: 瞬变涡旋诊断量
categories: ncl 大气科学
tags: 诊断量 eddy
author: renql
---

* content
{:toc}

## 折射指数
![](https://s1.ax1x.com/2020/04/13/GvA6bj.md.jpg)

在**折射指数为正**的区域，**波动传播**。   
在**折射指数为负**的地方，**波动容易消散**。  
且波动倾向于往正反射指数大的区域传播。  

上面图a与图b分别显示的是不同情况下的纬向平均U风和折射指数的合成图。  
**在high index时，急流强度减弱且变得更宽**，此时波动向赤道移动，离开了波动源（即eddy-driven jet区域），有利于产生eddy momentum fluxes，进而通过波流相互作用维持西风急流异常。  
**在low index时，急流变窄且增强**，此时折射指数在波动源区达到最大，意味着波动难以离开波源，不利于eddy momentum fluxes的产生，使得波流相互作用减弱，难以维持西风急流异常。
此时若计算两种情况下的eddy momentum fluxes，会发现high index的eddy momentum fluxes高于low index。该图也表明，**当急流过强时，它就像一个波导，减弱了波动的径向传播，波流相互作用减弱。**




## eddy的几种计算
1. 逐日数据减去**当年季节平均**或**当年月平均**，这样处理的异常包含2-90天或2-30天的瞬变波动  
2. 逐日数据减去**气候态季节平均**或**气候态月平均**，或者**气候态逐日年循环**（用气候态年平均值+气候态逐日年循环的前四个Fourier谐波分量）。这样的瞬变异常中可能还包含年际异常，但该异常与瞬变异常相比较弱很多。也包含高低频瞬变波动  
3. 2-10天或2-7天滤波得到高频天气尺度瞬变，10-90天滤波得到低频波动。该滤波可以基于原始数据（滤波时会减去平均值），或者方法1方法2计算得到的anomaly

上述几种计算方法得到的EKE大值区基本一致，只是大小会因为包含的频率范围而有差异。此外还有基于时间平均纬向平均的异常，这包含瞬变和定常波动。也可根据纬向空间滤波。

其中前四个Fourier谐波分量的提取常用`ezfftf`和`ezffeb`两个函数，而滤波可以用`bw_bandpass_filter`,具体见<a href="https://renqlsysu.github.io/2019/04/25/fourier_spectral/#%E5%B8%A6%E9%80%9A%E6%BB%A4%E6%B3%A2" target="_blank">我的另一篇博文</a>。

## 瞬变涡旋诊断量意义
1. **涡旋能量**是一个客观、具有物理动力意义的诊断量，包含**瞬变涡旋动能EKE**和**瞬变涡旋有效位能EAPE**。其中EKE可以直接反应涡旋环流变率，而EAPE则代表了与气象事件有关的温度波动。
2. **EP通量**只能用于全球纬向平均的二维平面上，等于Rossby群速乘以波活动密度，其辐合辐散也代表局地波活动密度的增加减少。此外，其辐合辐散也可以代表由eddy贡献的纬向平均的径向位涡通量，在EP通量辐合处，有向南的异常位涡的异常输送。**由于EP通量可以表示波活动密度的传播，其中eddy heat flux与波活动的垂直通量成正比，因此可以用底层eddy heat flux来表征垂直波活动通量的变化。而时间平均的eddy动量通量散度的变化可能是因为地表向上的波活动通量减少或者从波源向外传播的波活动减弱。**
3. **E矢量**可以作为二维EP通量的扩展，其**辐合或辐散**代表着波活动密度的**增加或减少**。其**方向**代表着相对于平均流的Rossby波群速或波动能量传播速度。其辐合辐散也能**诊断波流相互作用**，在E矢量辐合处，西风风速降低。此外，E矢量水平分量与时间平均纬向风速的水平梯度的**点乘**与平均流和扰动场的局地正压能量转换率成正比，**当点乘为正时，存在正的能量转换，通过从平均流向eddy的正压动量转换**减弱纬向风场的不均一性。E矢量的垂直分量（即瞬变热量输送）在高层很弱，因此在高层可以只考虑水平分量。其x分量可以反映波动形状。
4. **波活动通量 WAF**，它能根据背景流来量化波能量传播。可以在背景流存在纬向变化情况下，明确描绘瞬变涡旋的传播，其方向于Rossby波群速平行。其辐散或辐合也意味着波包的源或汇。

顺便再解释一下**有效位能**的概念：即可以转化为动能的全位能（内能和重力位能之和），指**系统的全位能**与该系统经绝热调整到正压及静力平衡状态（一种参考状态）时所具有的全位能（即**最小全位能**）之差，取决于等压面上的位温离差（相对于区域平均的异常）、温度离差或比容离差，即**大气斜压性**。一般来说有效位能约为全位能的**二百分之一**，且有效位能中只有大约**十分之一**转变成了动能。因此，若将大气视为一部由太阳辐射驱动的热机，太阳辐射能首先转变为大气全位能，然后再由全位能转变为大气运动的动能，其效率非常低。

中纬度，热量是顺梯度输送的，且一般都是将**平均有效位能**向**扰动有效位能**转换。动量是逆梯度输送（动量都向急流轴（动量大的区域）输送），此时将**扰动动能**转向**平均动能**。平均动能和平均有效位能之间通过垂直温度通量来转换，扰动动能和扰动有效位能之间通过扰动垂直温度通量来转换。如果一个环流在暖区域上升，冷区域下沉，那么是平均有效位能向平均动能转化（例如Hadley环流）。但如果是暖区域下沉，冷区域上升，那么是平均动能向平均有效位能转化（例如Ferrel环流）。全球实际大气中，大部分能量都是以平均全位能的形式储存。

在一个斜压波的生命周期内，在**eddy初期**，有扰动温度通量，能量从平均有效位能向扰动有效位能转化。在**eddy后期**，扰动动量通量强，能量从扰动动能向平均动能转化，急流增强。

下面是各诊断量的计算公式及效果图  
![](https://s1.ax1x.com/2020/04/13/GvAB28.md.jpg)
![](https://s1.ax1x.com/2020/04/13/GvtZrj.md.jpg)
![](https://s1.ax1x.com/2020/04/13/GvAsKg.md.jpg)


参考来源：
1. Gu, S., Zhang, Y., Wu, Q., & Yang, X.‐Q. ( 2018). The linkage between arctic sea ice and midlatitude weather: In the perspective of energy. Journal of Geophysical Research: Atmospheres, 123, 11,536– 11,550. https://doi.org/10.1029/2018JD028743  
2. 贺海晏 2010年 《动力气象学》 第十章

## Eady growth rate
**Eady growth rate** 是斜压最不稳定模态的线性增长速率，是衡量斜压性或涡旋增长速率的一个常用指标，从Eady model (1949) 推导出来。其量级一般在 3x10^-6 s^-1 倒数一般与中纬度气旋的特征生命长度相吻合。其数值大小**与静力稳定度成反比**，**与纬向风速的垂直切变即径向温度梯度成正比**。

ncl有直接计算该诊断量的函数 `eady_growth_rate (th, uwnd, hgt, lat, opt, lev_dim)` ，但只适用于 ncl6.4.0版本及其以后，其计算公式如下：

```
eady_growth_rate = 0.3098*g*abs(f)*abs(du/dz)/N  

N**2 = g[d(lnθ)/dz] ;the Brunt-Vaisala frequency of atmosphere，
;也有文章认为这是大气静力稳定度，N^2 的量级 10^-4 s^-1
```

![](http://glossary.ametsoc.org/w/images/thumb/f/fa/Brunt_V_final.png/170px-Brunt_V_final.png)

由于**Eady growth rate**是一个非线性量，因此不能用月平均或年平均的量来直接计算。如果需要气候态的**EGR**，需要先用高频的变量（例如逐3h，逐6h，daily）来计算**EGR**，然后再算气候态。

发现用ncl的函数计算EGR和自己编程计算得到的对流层底层EGR结果类似，但高层自己编程写的大很多。

```
; 用ncl自带的函数 eady_growth_rate 计算

opt = 0 ;opt=0, Return the Eady growth rate
;opt=1, Return the Eady growth rate and the vertical gradient of the zonal wind (du/dz)
;opt=2, Return the Eady growth rate and the vertical gradient of the zonal wind (du/dz) 
;        and the Brunt-Vaisala frequency

lev_dim = 1
lat = conform(air,vars&lat,2)
hgt = hgt/9.8 ;convert unit from m2/s2 to m
th  = pot_temp(lev*100, air, lev_dim, False) ；calc potential temperature
EGR = eady_growth_rate(th, uwnd, hgt, lat, opt, lev_dim)



; 根据公式自己写，结果几乎一样，表明 the Brunt-Vaisala frequency of atmosphere 与静力稳定度的计算类似。
lev_dim = 1
lat = conform(air,vars&lat,2)
pi = atan(1.0)*4
f0  = 2*(2*pi/24.0/3600.0)*sin(lat*pi/180.0)

static = static_stability(lev*100, air, lev_dim, 0)
static = conform(air,dim_avg_n(static,0),(/1,2,3/))
static = where(abs(static).lt.0.0000000001, 0.000001, static)

opt    = 0     ;used by center_finite_diff_n, no meanging
cyclic = False ;used by center_finite_diff_n
hgt = hgt/9.8 ;convert unit from m2/s2 to m
EGR  = 0.3098*(f0/static)*center_finite_diff_n(uwnd, hgt, cyclic, opt, lev_dim)
```

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

准定常波活动通量的激发源主有三个：  
1. 大地形扰动  
2. 绝热加热  
3. 与瞬变涡流相互作用，导致热量和动量的传输 

