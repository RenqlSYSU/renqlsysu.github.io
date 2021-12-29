---
layout: post
title: ERA5和ERA-interim差异
categories: 数据资料
tags: ERA
author: renql
---

* content
{:toc}

翻译自：https://www.ecmwf.int/en/newsletter/159/meteorology/global-reanalysis-goodbye-era-interim-hello-era5

2020年第一季度时，ERA5被发布，以替代自2006年开始发布的ERA-Interim。ERA5基于4D-Var data assimilation using Cycle 41r2 of the Integrated Forecasting System (IFS)，该系统于2016年开始在ECMWF运行。

相比于ERA-Interim， ERA5的优势在于模式物理、动力核、数据同化的改进，且分辨率从ERA-Interim的79km提高到31km。此外，ERA5可以提供逐小时输出及一个不确定性估计。The uncertainty information is obtained from a 10-member ensemble of data assimilations with 3-hourly output at half the horizontal resolution (63 km grid spacing).且ERA5输出的气象变量更丰富，例如多了100m风。

现在已经到了逐步淘汰ERA-Interim的时候了，因为ERA-Interim使用几种新的重要观测数据的能力有限，越来越难以维持，也不会迁移到欧洲中期天气预报中心在Bologna的未来数据中心。

### 使用的观测数据
在ERA5中使用的观测数据从1979年0.75MB/day增长到2018年24MB/day。其中，卫星辐射是最主要的增长数据。2009年后的降水数据中还同化了雷达观测。

相比于ERA-Interim，ERA5利用all-sky方法同化对湿度敏感的卫星频道。这可以在多云和降水地区提供新的信息，也纠正了早期在多雨条件下辐射同化技术导致20世纪90年代全球海洋ERA-Interim异常降水的一个问题。

传统数据和卫星数据的特征描述、相互校准和处理的改进逐步改进了历史观测的质量，并扩大其地理和时间覆盖范围。ERA5利用了几个再处理的卫星数据集，这些数据来自欧洲、美国和日本的空间机构和研究所。其中包括大气运动风矢量;臭氧、无线电掩星和测高数据;来自散射计的土壤湿度和风数据;以及对海洋湿度敏感的卫星数据的SSMI记录。

ERA-Interim无法吸收来自最新卫星仪器的观测数据（例如IASI和CrIS的高光谱数据）和地表雷达数据。此外，由于某些仪器和通道的失灵，ERA-Interim使用的观测数据逐渐减少。ERA5还可以处理自2013年以来越来越多地被地面压力、高空风和温度数据所采用的BUFR格式。而ERA-Interim无法处理这种形式，因此，它所吸收的观测数量急剧减少。在2018年底，ERA5每天使用约2400万次观测，大约是ERA-Interim的5倍。总得来说，**ERA5使用的观测数据比ERA-Interim多很多**。

### 模型输入强迫
ERA5使用的模型输入强迫包括太阳总辐照度强迫、臭氧、温室气体和为世界气候研究计划(WCRP) CMIP5倡议开发的一些气溶胶，包括平流层硫酸盐气溶胶。这是对ERA-Interim的一个重大改进，例如，ERA-Interim没有考虑到主要火山爆发造成的平流层硫酸盐气溶胶。

海表温度(SST)和海冰覆盖的演变基于不同时期的若干产品:英国气象局哈德利中心的海温和海冰HadISST2产品，EUMETSAT OSI-SAF再分析海冰数据，以及英国气象局的海温和海冰OSTIA产品，该产品也用于ECMWF的业务预报系统。细节可以在Hirahara et al.(2016)中找到。使用这些数据的目的是产生一个合并的数据集：  
1. 在每个时刻都尽可能准确，  
2. 没有明显的不连续，  
3. 可以可靠地接近实时更新。  
所有这些输入数据集每天都在变化。全球平均海温显示了20世纪70年代中期以来全球变暖的影响，以及El Niño事件(例如1997/98年和2015/16年)和大型火山爆发的影响。随着时间的推移，北极海冰总体上呈下降趋势，尤其是在夏季。

### ERA5不确定性估计
**再分析**是将模式信息与观测信息混合在一起的数据同化系统的结果，可以提供随时覆盖全球的数据。再分析数据总体上比前卫星时代更准确，因为当时的观测相对稀疏。ERA5使用的10个集合的4D-Var系统提供了对数据不确定性的估计。这些估计取决于数据同化中使用的短期预测中与流体相关的不确定性。它们还很大程度上取决于观测覆盖范围。

### 提高天气和气候数据质量
从ERA5再分析开始的再预测显示，相比于ERA-Interim，在技术范围内增加了大约一天的提前预报天数。此时，可以更好地模拟热带气旋地中心气压和降水量。逐小时地时间分辨率使我们能够更精确地观察每日天气系统的演变。
