---
layout: post
title: 高原涡客观识别
categories: 大气科学 文献笔记
tags: TPV
author: renql
---

* content
{:toc}

**Tibetan Plateau Vortices (TPVs)**高原涡是发生在高原地区500hPa的一种**浅薄的中尺度alpha气旋系统**，垂直范围2-3km，水平范围400-800km，生命期一般为1-3天，是高原上产生降水的主要系统。其风场和高度场的关系不完全满足地转平衡特征。

当出现有利的环流形势时，会有部分低涡移出高原，引发下游地区一次大范围的暴雨、雷暴等灾害性天气过程。东移TPV会在下游产生有利于西南涡（**the southwest vortices**）发展的环境。此外，TPV与西南涡耦合亦会导致暴雨<sup>【1】</sup>。例如  
> Feng et al. (2014) describe a TPV event that lasted **from 19 to 24 July 2008** in which a TPV moved off the TP and traveled northeastward all the way to the coast of the Yellow Sea within five days. They report that this TPV caused heavy precipitation along its path, especially in Sichuan province, where the maximum 24-h accumulated precipitation at one station reached 288.4 mm (roughly a quarter of the average annual precipitation at that location) <sup>【2】</sup>.   
> Also, many heavy rainfall events, such as those during **14–15 July 1979 in the Sichuan basin** (Wang and Orlanski, 1987), **20–22 July 1998 near Hubei** (Bei et al., 2002), **21–26 July 2010 in Sichuan** (Xiang et al., 2013), and **10–13 June 2008 in South China** (Chen et al., 2015), have shown that vortices emanating from the TP play an important role <sup>【3】</sup>.   

因此有必要研究TPV的结构、发展机理、路径预报等等。 以往的研究认为高原涡的产生和发展与**地表热力和动力作用**及**对流潜热加热作用**有关。积云对流产生的感热结合**大气低频振荡**对TPV的产生和发展也有重要作用。Li et al (2014) 认为TPV的年际变率与水汽输送与潜热释放有关。也有认为TPV的热力结构与热带气旋类似。 (Li and Jiang, 2000; Li Guoping et al., 2011)

以往关于TPV的研究，主要通过500hPa天气及人工看图的方式对TPV活动进行统计（**当500hPa风场中有气旋性环流出现时，然后根据气旋中心判断高原涡中心**或者**500hPa等压面有闭合等高线的低压中心**），这种人工识别可以结合当时天气情况的分析和预报员经验，但工作量极大并具有很大的主观性，导致统计结果的差异很大。

因此，将客观识别技术结合高分辨率再分析资料来统计研究TPV成为趋势。目前已看到好几篇论文运用不同的识别技术来统计TPV，基本有以下几种方法（按发表时间排列，个人觉得第四种方法是最复杂的）：




## 一、Feng et al. 2014
**数据**：NECP Climate Forecast System Reanalysis （CFSR）再分析资料。**0.5度的分辨率，结合再分析和预报场后的时间间隔是3h**，该资料的优点有：usage of various satellite data, improved model, finer resolution, advanced assimilation, and ingestion of a variety of data from conventional observations, aircraft observations, and special observation programs。有研究<sup>【4】</sup>认为该数据对高原500hPa风向的刻画能力优于ERA-Interim和JRA-55。

**时间**：2000-2009年4月-10月的高原涡

**识别步骤**：  
1. 基于**500hPa流线和相对涡度场**识别出TP区域的所有中尺度气旋（未说明阈值选择）  
2. 进一步判断上述中尺度气旋是否伴随**500hPa局地气压低值**（是否闭合等压线）（如何确定这个等压线是否闭合？）
3. **水平尺寸筛选**。该气旋最外围的等压线x方向是否跨越了2个经度。
4. **生命期筛选**。只有生命期长于3h才认为该中尺度气旋是高原涡。

并未提到该方法参考了哪篇文献，也未说明追踪方法。

**结果**：
- 发现平均每年有103个高原涡产生，主要集中在5月到8月。
- 主要产生区域是高原西部，属于大尺度辐合区域。
- 也查看了日变化，一般是午后到晚上这段事件是产生高峰期，后半夜是消亡高峰
- 生命期一般是15h
- 平均水平尺度是280km。

## 二、Lin 2015
**数据**：1979到2013的The ERA-Interim data，1°的分辨率，逐6小时。Bao and Zhang (2013) 将该数据与TP上的探空资料对比，认为其可以精确地表示TP上的大气状况。3000m作为TP的地理边界

**识别步骤**：借鉴了 Wernli and Schwierz (2006) Surface cyclones in the ERA40 dataset (1958–2001). Part I: Novel identification method and global climatology  
1. 扫描500hPa位势高度场，挑选出位势高度小于周围8个格点值的格点，若周围有多个满足条件的格点，则取这些格点的平均位置  
2. 追踪500hPa每隔5gpm的等位势高度线，以识别出低压格点周围所有的闭合等压线，去掉没有闭合等压线的低值系统。并用**最外面的闭合等压线**来确定**低值系统的尺寸**，去掉尺寸小于10000km2。用**最里面的闭合等压线**作为低值系统中心，将低值系统中心位势高度与同纬度纬向平均的位势高度差作为**高原涡强度**（这可以有效去除因季节变化导致的气压变化）。  
3. 为了去掉TP区域的局地热低压系统，要求低值系统至少维持12个小时。  
4. **基于涡旋移动惯性追踪TPV**。基于前一时刻和该时刻的位置推测下一时刻的位置FGP，那么下一时刻的位置就应该出现在FGP周围一定半径D范围内的位置。该文选D=400m。对于一个新产生的TPV，没有前一时刻的信息，此时将该TPV的位置设定未FGP，然后在半径D范围内查找下一个时刻的TPV。若有多个TPV进入该范围，则选取离FGP最近的系统。
5. **确定TPV的热力属性**。圈出包含低值系统最外围闭合等压线的方框R1，然后在R1左右各圈出一个大小同R1的方框R2和R3，求出这些方框内区域平均温度（文中没有明确说是哪个高度的温度，但我想应该是500hPa吧）  
![](https://s1.ax1x.com/2020/05/12/YtxKHO.png)

**结果**：
- 发现在1979-2013年间平均每年有53个高原涡产生，其中有6.7个移出高原。此外每年有9.4个高原涡源来自上游。  
- 81%的TPV初期是暖性的
- TPV的高发期是5月到9月（雨季）
- 发现总TPV的频率平均每十年下降2个（没过显著），移出高原的TPV则每十年下降1.4个（过了99%的显著水平），占总TPV数量的百分比下降2.3%

该文最后还提了关于TPV的一系列科学问题：
1. 为什么移出TP的TPV百分比这么低？  
2. 当TPV东移出TP后，其属性和结构发生怎样的变化？  
3. TPV数量和移出高原的TPV数量的年代际变化与背景气候态有什么关系？  
4. 全球变暖引起的高原地表温度上升对TPV的结构、产生、发展有什么影响？  

## 三、张博 2017 ##
**数据**：也是用了NCEP CFSR数据，2001-2010，时间间隔6h，0.5°分辨率
 
![](https://s1.ax1x.com/2020/05/12/YtxlUe.md.png)

**结果**：
- 没有考虑TPV东移出高原后的情况。此外这里的识别标准过于绝对固定，无法更具每一年的环境条件来自动调整识别标准。 
- 该客观识别方法与基于NCEP资料的人工识别数据集的吻合率约为60%，与低涡年鉴的吻合率约为50%。该方法在夏季TPV生成频数、月分布等方面与人工识别方法的统计结果相近，但低涡中心位置的识别精度有待提高。  
- 客观识别出的TPV在6月出现最多。其中生成于高原西部、中部和东部的低涡 分别占33%，39%和28%。  
- 低涡在高原停留12h的占60%，停留24h的不足10%。

## 四、Curio 2018 ##
**数据**：用到了三种数据。两种再分析资料ERA-interim、NCEP-CFSR，一种模式资料an ensemble of HadGEM3 (Hadley Centre Global Environment Model 3) Global Atmosphere 3.0 (GA3; Walters et al. 2011) present-climate atmosphere-only simulations（分辨率25km）。

**识别步骤**：基于 automated objective feature-tracking algorithm, **TRACK**, developed by Hodges (1994, 1995, 1999)    
1. The **spectral filtering** removes total wavenumbers smaller than 40 (large spatial scale, .1000km) and larger than 100 (small spatial scale, ,400km), hence focusing on the TPV spatial scale.  
2. The **spectral coefficients** are also tapered using the method of Sardeshmukh and Hoskins (1984) （Spatial smoothing on the sphere）to further reduce noise in the data such as Gibbs oscillations.   
3. The cyclones are identified as the off-grid maxima greater than **2*10^-5 S^-1** using B-spline interpolation and a steepest-ascent method in the 6-hourly **500-hPa spatially spectrally filtered relative vorticity field**.  
4. 追踪。首先通过使用**最近邻方法**连接最大值来初始化追踪。   
5. 然后，通过最小化一个成本函数来优化这些轨迹，该函数适用于在一个时间步长的轨迹平滑度和位移距离的自适应约束   
6. 初始高度高于3000m且至少持续四个时次（一天）以上的气旋认为是高原涡  
7. 在第二步中，应用了一个位势最小滤波器，这意味着每个TPV轨道至少有一个时间步长中，一个相关的500-hPa位势高度最小值必须发生在轨道点周围的搜索半径2.58(测地线半径)内。  

**与高原有关的降水计算**：每个高原涡特征点周围3°范围内的降水量平均被认为是与该高原涡相关的降水量。这个搜索范围比最小位势高度的搜索范围（2.5°）大，因为一般由高原涡产生的降水量往往会被扯离高原涡中心，而最小位势高度则离涡度中心很近。   
暴雨定义为超过95%降水临界线。  
将每个TPV特征点周围3°以外的降水量抹去，然后再将所有降水量加起来，计算由TPV导致的降水量百分比。   

**结果**：
- 发现多数高原涡在TP的西北处产生，多发区域的面积较小且全年稳定
- 西风急流的位置与强度和TPV东移的距离相联系，影响了TPV是否能移出TP
- 在某些月份，与TPV相关的降水可以解释中国部分区域总降水量的40%
- 研究了TPV产生数量的年际变化与西风急流的关系，发现TPV多年西风急流偏南。但这里用到的样本数较少。
- 该研究结果表明，水平分辨率为25km的全球气候模式可以模拟出TPV。

## 参考文献
1. Feng, X., C. Liu, R. Rasmussen, and G. Fan, 2014: A 10-yr climatology of tibetan plateau vortices with NCEP climate forecast system reanalysis. J. Appl. Meteorol. Climatol., 53, 34–46, https://doi.org/10.1175/JAMC-D-13-014.1.
2. Curio, J., R. Schiemann, K. I. Hodges, and A. G. Turner, 2019: Climatology of Tibetan Plateau vortices in reanalysis data and a high-resolution global climate model. J. Clim., 32, 1933–1950, https://doi.org/10.1175/JCLI-D-18-0021.1.
3. Curio, J., Y. Chen, R. Schiemann, A. G. Turner, K. C. Wong, K. Hodges, and Y. Li, 2018: Comparison of a Manual and an Automated Tracking Method for Tibetan Plateau Vortices. Adv. Atmos. Sci., 35, 965–980, https://doi.org/10.1007/s00376-018-7278-4.
4. 刘自牧,李国平.高原切变线的客观识别与时空分布的统计分析[J].大气科学,2019,43(01):13-26.
5. Lin, Z., 2015: Analysis of tibetan plateau vortex activities using ERA-interim data for the period 1979–2013. J. Meteorol. Res., 29, 720–734, https://doi.org/10.1007/s13351-015-4273-x
6. 张博,李国平.基于CFSR资料的青藏高原低涡客观识别技术及应用[J].兰州大学学报(自然科学版),2017,53(01):106-111+118.

这几篇文章中都有涉及**ERA-interim**和**NCEP-CFSR**这两个高精度再分析数据的详细介绍。

可以看到虽然他们使用的TPV识别方法和条件不同，但最后得到的TPV的特点（尤其是发生频率的年循环、生命期、产生源地分布）几乎差不多，除了平均每年的TPV数量存在较大差异。

发现目前关于高原涡年际变化、年代际变化的研究似乎挺少的。
