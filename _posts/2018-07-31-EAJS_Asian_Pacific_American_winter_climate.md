---
layout: post
title: 东亚急流与亚洲-太平洋-北美冬季气候异常的关系
categories: 文献笔记
tags: monsoon Jet-stream ENSO
author: renql
---

* content
{:toc}

师兄建议我多看看老板的论文，这才发现自己好像没怎么读过老板的文章，除了那篇非常著名的《Monsoon and ENSO: selectively interactive》（1992）外就没有看过其他文章。于是上网去搜了老板有哪些文章。   
<a href="http://atmos.sysu.edu.cn/teacher/357" target="_blank">老板简历</a>，从中挑选高引用文章看。  

先看了下面这一篇讲亚洲-太平洋-北美冬季风的文章，感觉格局非常的大。且该文是2002年发表的，看到那时老板的归属部门还是 NOAA/NWS/NCEP Climate Prediction Center, Camp Springs, Maryland      
> Yang, S., et al. (2002). "Variations of the East Asian jet stream and Asian-Pacific-American winter climate anomalies." Journal of Climate 15(3): 306-325.

因为文章比较长，因此下面主要记录了我认为比较有意思的内容，至于具体的图片可以上官网查看。

### abstract ###
通过东亚急流来描述亚洲-太平洋-美洲的气候关系，主要强调北半球冬季及年代际变化   
分析了EAJS的变化及其与ENSO、中高维度北太平洋海温的关系，评估了EAJS及ENSO与异常大气环流、表面温度、降水的相对关系   

发现强的东亚急流通过加深东亚槽、阿留申低压、加强东亚冬季风使得亚洲天气和气候变得剧烈。   
同时，他还与东亚的更干冷状态及赤道亚洲澳洲的强对流有关。  
此外，他还通过静止波的变化与北美温度及降水相关联  
虽然EAJS与赤道中东部海温的关系不大，但与中高纬度北太平洋海温显著相关。  




### 1. Introduction   
科学问题：  
1. EAJS与气候异常（例如ENSO）在年际尺度上的关系未被揭示  
2. 造成EAJS年际变化的物理机制还不清晰  

在本文中，  
首先会描述ENSO与EAJS之间的关系；   
其次，描述与ENSO和EAJS相关的大气及海洋特征   
接着，评估EAJS和ENSO在连接大尺度和区域气候中的重要性  
同时，调查EAJS和北太平洋海温在赤道外的关系  

### 2. Datasets   
### 3. EAJS and ENSO associated teleconnection patterns  
首先利用东亚急流（即冬季西风急流）大值区的分布区域，定义了一个基于区域（30–35N，130–160E）平均U200的EAJS指数，用以描述西风急流的强度fig2   

随后利用SOI指数及EAJS指数分别与DJF的U200空间场做相关，发现两者的相关模态显著不同。fig1，3   
且这两个相关模态分别与U200的EOF第一第二空间模态相对应，表面两者的正交性。 fig5  
利用强EAJS、弱EAJS及EINino、LaNina年做合成得到的U200异常场也与上述空间场类似。fig4   
此处觉得特别神奇，用了三种不同的方法，但最后得到的结果是一致的

### 4. EAJS and Asian–Pacific–American climate   
#### 4.1 Broadscale circulation patterns      
对比了强EAJS、弱EAJS年和EINino、LaNina年冬季的H500差值场，发现EAJS对应的H500变化幅度更大fig6   
随后还计算了准静止波通量（基于<a href="https://journals.ametsoc.org/doi/pdf/10.1175/1520-0469%281985%29042%3C0217%3AOTTDPO%3E2.0.CO%3B2" target="_blank">Plumb，1985</a>），这个就完全不懂了，打算有时间学习一下,fig7   

#### 4.2 Regional-scale features 
(low level circulation systems, surface temperature and precipitation)    
利用回归与合成的方法研究了EAJS与底层风场、地表温度和降水的关系，期间还定义了一个东亚冬季风指数    
In this study, we measure the monsoon’s variability by constructing a time series from
the DJF V850 that is averaged over the domain of 20–40N, 100–140E, the core region of the monsoon.  

发现冬季西伯利亚高压和EAJS的相关性较好，和ENSO的相关性不高   
亚洲冬季风指数与EAJS的相关性（-0.67）比SOI的相关性（-0.32）好。EAJS强的时候，亚洲冬季风也强。EINino年，冬季风弱，但是LaNina年变化不明显   
利用合成的方法，发现EAJS强年，东亚偏冷偏干，北美洲西部偏暖偏干、东部偏冷偏干，海洋性大陆对流增强

由于数据有限，相关性或许不能说明什么，但从上面这所有相关图中可以表面一个特征，即EAJS在中高纬度地区的信号要强于ENSO   

dynamical：EAJS强年，亚洲大陆高压增强，冬季风环流增强，因而使得Hadly环流增强，海洋性大陆对流增强。**这个似乎与我要做的Indian-Australian monsoon有关，即东亚冬季风增强时，Australian summer monsoon也增强**   
此外，EAJS强年，北太平洋东部异常南风使暖空气得以到达北美西部，同时组织风暴从西部入侵北美，因此北美偏暖偏干。

### 5. Linkage between EAJS and North Pacific SST   
因为EAJS和TS的相关图中，在北太平洋区域有很好的相关性，因此猜想EAJS和北太平洋海温之间存在关系。**不过不能理解的是，就算两者之间存在相关性，为什么要通过EOF来分析两者之间在模态上的相关性呢？**   
对北太平洋海温做EOF，发现PC1和SOI的相关性非常好，PC2和EAJS的相关性非常好，以此说明NPSST第一模态主要反映ENSO信号。  
同时再用PC1和PC2分别和DJF U200做回归，发现分别与用SOI和EAJS做的回归场类似  
随后又用合成方法查看了和EAJS相关的冬季DJF及前期秋季SON的NPSST变化的幅度，但是这里存在一个问题，即这样变化的海温究竟会对接下去冬季的EAJS产生怎样的影响，或许可以通过加了上述异常海温信号的GCM模拟来揭示。   

### 6. Summary and discussions
