---
layout: post
title: The Atmospheric Bridge:The Influence of ENSO Teleconnections on Air–Sea Interaction over the Global Oceans
categories: 文献笔记
tags: ENSO ocean teleconnection review
author: renql
---

* content
{:toc}

这是老板2018年ENSO综述中引用的一篇介绍ENSO影响印度洋和大西洋的两大机制之一——**大气桥**的类似于综述性的文章。  
> Alexander, M. A., et al. (2002). "The atmospheric bridge: The influence of ENSO teleconnections on air-sea interaction over the global oceans." Journal of Climate 15(16): 2205-2231.

文章真的好长，竟然有27页，感觉他关于海洋的内容比较多一些。其中有以下内容是之前不了解的：
1. **混合层厚度MLD**的定义（1、观测是用的温度比表面温度低1度的厚度；2、模式数据是通过湍流动能方程计算出的）和我之前了解的不一样，之前好像是用20摄氏度等温线的高度代表混合层厚度，如果我没有记错的话。  
2. **Reemergence of SST anomalies**  
3. 强表面净辐射通量分解为四个部分：短波、长波、感热、潜热。作者认为净辐射通量是大气影响海温的主要机制。  
4. **multiple bridge**  
5. 大气影响海温的几种途径：沿岸上升流，Ekman抽吸，表面热通量，Ekman输送，淡水通量  
6. ENSO期间其他海域的海温变化  
7. 模式的实验设计：可以部分海域有海气相互作用，但只是海气之间有动量、热量的交换，并没有海洋动力过程   
8. Ensenmble之间用标准差来衡量其模式间的variance  

此外，这是一篇02年的文章，距今已过去16年，感觉有些老了，不知道看这些老文章是否有意义。不过这篇文章还是有利于树立全球概念的

## Abstract
ENSO事件中，大气对赤道太平洋SSTA的响应影响着全球其他海区状况, 其他海区海温的变化又会影响大气桥

观测和建模研究现已明确了赤道太平洋SSTA和北太平洋、北热带大西洋和北印度洋冬季和春季SSTA之间的联系。  
与ENSO相关的SSTA在夏季北太平洋西部和秋季印度洋也表现出明显的异常。  
![](https://journals.ametsoc.org/na101/home/literatum/publisher/ams/journals/content/clim/2002/15200442-15.16/1520-0442%282002%29015%3C2205%3Atabtio%3E2.0.co%3B2/production/images/large/i1520-0442-15-16-2205-f02.jpeg)

- 虽然表面热通量是大气桥驱动SSTA的关键组成部分，但埃克曼输运也在北太平洋中部造成了海温异常，尽管其影响程度还需进一步研究。

- 大气桥不仅影响SST的年际变化，还影响混合层深度(MLD)、盐度、上层海洋温度的季节演化及北太平洋SST的低频变化。

- 模式结果表明，北太平洋低频(>10年)SST变化的主导模式中有相当一部分与热带强迫有关。

- AGCM实验表明，中高纬度海洋对ENSO响应的反馈是复杂的，但幅度不大。

- 热带太平洋外的大气-海洋耦合略微改变了太平洋-北美(PNA)区域的大气环流异常，但这些变化似乎取决于北太平洋内外的季节周期和海气相互作用。

## 1. Introduction
Here the ENSO index is SST anomalies averaged over 5N–5S, 172E–120W 

此处大气桥指ENSO期间**赤道太平洋-大气-其他海域**间的联系。这之所以值得研究有以下五点原因：  
1. 这对于预报**赤道大西洋**及其他海域海温是必要的  
2. 对北太平洋和印度洋亚洲季风区的**SST年际变化**甚至更长时间变化有贡献  
3. 为**模拟**全球大气对ENSO的响应提供严格的检验  
4. 使得模式实验可以清楚地**分离大气强迫**（此处指对ENSO的遥响应和海洋反馈)  
5. 会影响赤道太平洋外的**海洋生态系统**  

- 从1975年开始，科学家将赤道太平洋的SSTA与其他海区的SSTA相联系

- ENSO的峰值在NDJ，而其他海区与ENSO相关的SSTA发生在ENSO峰值后2-6个月。因为大气需要2周左右的时间去响应赤道太平洋SSTA，然后在剩下的几个月里去影响其他海区海温

- 尽管赤道太平洋SSTA和其他海区的关系大多在1990年以前被确认，但这种遥相关SSTA的产生及其对大气环流的反馈尚未明确。

- GFDL的宗旨是通过AGCM研究赤道及赤道外海温对全球气候的影响

本文利用最新的观测资料和模式结果**回顾**了以往对大气桥的理解，同时说明过去取得的进展和尚未解决的问题。    
特别地，我们将评估PNA区域海气反馈对响应于ENSO的原始大气的影响，这与以往的模式研究不同  
同时考察在**低频变化中赤道和北太平洋SSTA间的关系**等新出现的问题以及**大气桥对上层海洋状况的影响程度**。  

## 2. Model simulations
设置了三组模式实验。所有实验中，赤道东太平洋SST的变化同实际观测一致。  
1. **Control**：其他海域的SST的变化同气候态的SST年循环，即每年都一样
2. **MLM**：mixed layer model，赤道太平洋外且无海冰的海域运行柱形海洋模式
3. **NP-MLM**：只在北太平洋（21.24N以北）海域运行海洋模式，其他海域依然用气候态的SST年循环

NP-MLM 和 Control 的差值代表北太平洋局地海气相互作用的影响  
MLM 和 NP-MLM 的差值代表其他海域的海气相互作用的影响

![](https://journals.ametsoc.org/na101/home/literatum/publisher/ams/journals/content/clim/2002/15200442-15.16/1520-0442%282002%29015%3C2205%3Atabtio%3E2.0.co%3B2/production/images/large/i1520-0442-15-16-2205-f12.jpeg)  
> Regression coefficients of monthly mean 500-mb height anomalies vs the Jan ENSO index from the previous Dec to the following Mar, for the MLM, NP–MLM, and control experiments. Contour interval is 10 m; positive (negative) contours are red (blue). The shading indicates two-tailed 95% statistical significance of the difference between coupled and uncoupled regressions.

MLM由一个独立的**柱形网格模式**组成，其中包括一个多层系统之上的混合层，多层系统表示密度跃层的状况  
该模式包括局地海气通量、穿透太阳辐射以及扰动夹带的进入混合层的水，但没有垂直运动和水平过程，因此可以认为这个海洋模式是没有海洋动力过程的  
混合层下面，热量通过翻转对流、垂直扩散及穿透的太阳辐射重新分布  

由于洋流缺失及模式误差，为了使海洋模式的平均季节循环同观测，实现了表面温盐通量的订正。  
但某些地区的长期月平均数据中依然存在SST偏差。  
因此用MLM的长期月平均SST作为Control和NP-MLM模拟中规定的SST域中的海洋边界条件，以确保三组实验均采用相同的SST基态。  

模式结果和观测的一些差异可能是由大气-海洋的内部变率造成，这一点从整体成员之间的传播就可看出。  
ensemble之间的差异可以通过标准差衡量，所有点的标准差都小于0.2，在相关显著区域的标准差小于0.1  

## 3. Response to ENSO: Precipitation and upperatmospheric circulation 
> 猜测研究方法是合成分析。看论文后，发现是用ENSO index回归的风场和降水场，但这和合成分析也差不了多少。

- 赤道和赤道外的动力学联系包括由**赤道对流**和**强的涡度梯度造成的辐散流**激发的Rossby波。  
传到赤道外的扰动受纬向平均流的非对称性和中纬度风暴轨迹间的相互作用的影响

- 赤道中太平洋降水异常多的**两侧200hPa有反气旋**，这与大气对赤道的**非绝热加热响应**类似  

- MLM模拟的西太降水异常比观测**弱**。且赤道两侧的反气旋位置**偏西**  

- EINino期间，中纬度西风急流增强，在东北太平洋、加拿大、美国东部、中国南部有波状特征  

![](https://journals.ametsoc.org/na101/home/literatum/publisher/ams/journals/content/clim/2002/15200442-15.16/1520-0442%282002%29015%3C2205%3Atabtio%3E2.0.co%3B2/production/images/large/i1520-0442-15-16-2205-f04.jpeg)  
>  Regression values of precipitation and 200-mb streamfunction regressed on DJF ENSO index for DJF (1951–99). Positive (negative) extremes are associated with anomalous clockwise (counterclockwise) flows.

## 4. ENSO-related SST anomalies ##
介绍了North Pacific, Tropical Atlantic, Indian Ocean的ENSO-related SSTA， 并着重介绍了North Pacific年际和年代际时间尺度上与ENSO相关的SSTA

> 猜测研究方法是滤波后算相关系数场,实际答案是滤波后做EOF分析

- 20S以北的低通滤波的模态与未滤波的模态类似，只是在赤道东太平洋范围更广，且北太平洋相对于热带地区的权重更大。  
使用多通道奇异谱分析，Zhang等人发现准四年和年代际的变率在赤道和北太平洋都有很强的特征  
有人认为PDO是ENSO低频分量的结果，也有人认为PDO是赤道外海域的固有特征

- EINino期间，大西洋赤道以北海域SST偏暖

- EINino年，印度洋海盆变暖，且开始变暖的时间早于大西洋。印度洋的两类海温模态都与ENSO有关。一是EINino结束期间，印度洋**整个海盆的增暖**。二是EINino成熟前期秋季，**印度洋偶极子**（西暖东冷）的发展

## 5. SLP–SST relationships: The bridge revealed ##
> 利用合成分析看ENSO发展过程中，SLP和SST的演变。合成分析是基于9个EINino和9个LaNina事件

- 1985年，Emery综合了有关大尺度ENSO-SST关系的研究，提出赤道太平洋和北太平洋可能通过大气桥进行相互作用。他们认为EINino期间强的阿留申低压可以解释东北太平洋海温的异常增暖。作为推论，当EINino期间北太平洋SLP与经典的ENSO信号不同，相关的SST模态也必然不同。**但我个人觉得这也有可能是与ENSO相关的SST模态与以往不同，从而导致SLP不同**

- 虽然赤道太平洋和北太平洋通过大气进行联系的关系早已被证明，但直到1994年才提出大气桥的概念

- 冷暖事件的SLP差异在赤道地区几乎保持不变。与此同时，北大西洋海温开始升高，并在次年春季达到峰值，而印度洋的海温在第一年的夏秋季节呈现IDO分布，后期整个海盆（包括中国南海）增暖

- EINino期间，阿留申低压增强，气旋增强，北太平洋中部吹西北风（冷），北太平洋东部吹南风（暖），从而形成北太平洋冬暖西冷的SSTA分布。

> question：SLPA最强发生在次年冬季，但在那之前北太平海温就已经有东暖西冷模态产生了，所以怎么能说是大气桥的作用呢？

- 模式数据结果的不同可能是因为大气变率，也可能是由模式误差和海洋动力学缺失造成的

![](https://journals.ametsoc.org/na101/home/literatum/publisher/ams/journals/content/clim/2002/15200442-15.16/1520-0442%282002%29015%3C2205%3Atabtio%3E2.0.co%3B2/production/images/large/i1520-0442-15-16-2205-f06.jpeg)

## 6. Processes that generate SST anomalies ##
分North Pacific, Tropical Atlantic, Indian Ocean三个大洋介绍**与ENSO相关的大气环流异常**如何通过**表面热通量**、**地下水卷入地表混合层**、**Ekman输运**产生SSTA

很强但意外的1982/83 El Nino事件迫使研究人员不仅需要重新考虑ENSO的根本动力,还要研究赤道外太平洋海洋异常的发展过程。    
而1982/83年EINino事件之前，研究人员认为沿岸Kelvin波是ENSO期间联系赤道和赤道外SSTA的动力学机制，但Kelvin波只是被局限在一个近岸的狭长通道里。

- The net surface heat flux is composed of shortwave (Qsw) and longwave (Qlw) radiation and sensible (Qsh) and latent (Qlh) heat flux.  

- ENSO次年JFM期间，热带5N-20N之间减弱的信风使得向上的潜热通量也减弱，也有研究表明更热更湿的大气温度也能减弱蒸发，使得北大西洋增暖

- 与Walker环流的异常下沉使得云量减少，以及太平洋北美地区的大气环流异常，增加了短波辐射，使得副热带北大西洋变暖

- 也有人认为ENSO可以通过Ekman抽吸和海洋动力影响北大西洋海温

- Klein 1999年只利用异常的表面热通量和一个线性衰减项就模拟出了与观测一致的ENSO次年春季北大西洋增暖现象，表明了净表面热通量是ENSO期间影响海温的主要原因

- ENSO也会通过海洋动力学也会影响印度洋海温。ENSO发展年秋季，异常东风通过Ekman抽吸使印度洋东部海域变冷。由异常风在印度洋东南部激发的Rossby波导致印度洋整个海盆的增暖。

- 海洋动力学的缺失使得模式模拟的ENSO期间印度洋增暖幅度弱于观测

## 7. Other ENSO-induced ocean changes ##
认为与ENSO有关的异常大气也会影响海洋的盐度、混合层厚度、下表层海温结构。

- EINino期间，海洋性大陆的盐度增加（因为降水减少），加勒比海的盐度也增加了。

- 南美北部的P-E减少。有人认为P-E的变化会影响温盐环流

- 1991年Lukas等人认为赤道西太平洋的盐度会影响密度垂直廓线，从而影响西风爆发时由于夹带而产生的冷却量。 他们推测，盐度依赖的夹带作用对暖池地区海温的调节可能在ENSO循环中起重要作用。

- 混合层厚度的季节变化可能会影响从一个冬天到下一个冬天的上层海洋温度。1970，Namias发现冬季中纬度SSTA可能在下一个冬季再次出现，但跳过了中间的夏季

**冬季**，SSTA在地表形成并扩散到整个混合层。  
在**春季**混合层变浅时，该SSTA存在于混合层下方。  
该热异常被纳入稳定的**夏季**季节温跃层(30-100 m)，从而与表面通量绝缘，这些表面通量通常起到抑制原始海温异常的作用。  
当混合层在随后的**秋季**再次加深时，异常被重新带入表层并影响海表温度。    
这是**SSTA再次出现的可能机制**，研究人员发现这种现象主要发生在远离强洋流作用的海区  

## 8. Oceanic feedback on the atmospheric bridge ##
这一节似乎只是用NP-MLM,MLM,Control模式结果说明了局部耦合和全球耦合的效果，但并没有说其他地区的海气相互作用如何影响PNA的大气环流。    
此外，这里还用到一种之前没有见过研究方法————**influence function**，虽然看懂了它的介绍，但还是不清楚这要怎么计算。    
> The influence function (**g**) can be thought of as an **inverse Green’s function**. That is, rather than showing how the response at all locations is affected by a specified source of forcing, **g** shows how the forcing from all locations affects a specified response.  

此处，**g**表示目标大气响应(指定为北太平洋中部正压大气的高度异常)对先前全球海温异常的敏感性，该敏感性用滞后的多元线性回归确定。下面是该方法的计算结果  
![](https://journals.ametsoc.org/na101/home/literatum/publisher/ams/journals/content/clim/2002/15200442-15.16/1520-0442%282002%29015%3C2205%3Atabtio%3E2.0.co%3B2/production/images/large/i1520-0442-15-16-2205-f15.jpeg)     
> **Sensitivity map**, or influence function, of a negative height anomaly over the North Pacific to **anomalous SSTs 60 days earlier** in the MLM. The influence function is contoured at an interval of 0.002 K m 21; the zero contour is removed for clarity and positive (negative) values are red (blue). The target height response at 200 mb is indicated by gray shading with a 0.25-m interval.

- 非局地的海气相互作用可以通过**多个大气桥**影响与ENSO有关的大气环流。例如印度洋、西太平洋及其他海域与ENSO有关的SSTA可以影响太平洋北美区域的大气。

- 由于海洋会通过表面热通量阻碍大气环流，使得热带外大气对ENSO的响应由于海洋的存在而减弱  
当SST被允许向上层大气调整时，这种阻碍会减弱，因此耦合大气海洋模式中底层的低频热变化比单独大气模式强  
弱化的热阻碍会增加大气环流的变率，但同时也会使某些特定的模态得以长时间维持，维持的原因目前还不清楚  

- 粗糙的分辨率低估了赤道降水和风暴轨迹的变率，这常常导致大气对赤道和中纬度SSTA的响应减弱

- 50m厚的平板海洋不足以描述冬季的海洋状况，因为北太平洋中部和北大西洋冬季的混合层厚度超过100m

- 印度洋与ENSO有关的SSTA倾向于在EINino期间增强亚洲夏季风的降水和环流，这与太平洋的暖SSTA的直接效果相反。 **不过不清楚这里说的是ENSO发展年还是衰弱年？**

## 9. Outstanding issues ##  
关于热带海温异常的大气响应尚未解决的问题的详细讨论可以在下面这篇文章的第6部分找到（截止2018年11月被引1233）   
> Trenberth, K. E., G. W. Branstator, D. Karoly, A. Kumar, N-C. Lau, and C. Ropelewski, 1998: Progress during TOGA in understanding and modeling global teleconnections associated with tropical sea surface temperatures. J. Geophys. Res., 103, 14291–14324.

- 最重要的可能是提高云量的代表及其对太阳辐射的影响，以提高对ENSO相关的SSTA的模拟。

- 大多数研究都集中在冬季北半球与ENSO相关的海温异常。而相对较大的与enso相关的冬季南半球海温异常和夏季北半球海温异常受到的关注较少。尤其是印度洋偶极子在秋季的发展

