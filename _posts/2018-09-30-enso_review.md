---
layout: post
title: ENSO review
categories: 文献笔记
tags: ENSO impact change
author: renql
---

* content
{:toc}

最近看了两篇2018年发表的ENSO综述文章，其中一篇是老板和师兄师姐他们一起写的**《El Niño–Southern Oscillation and Its Impact in the Changing Climate》**，主要侧重于ENSO在过去和未来对全球其他地区天气气候的影响，非常系统，光看其文章标题即可大致了解ENSO对全球的影响有哪些，非常有利于发散思维。但鉴于我主要研究**ENSO-monsoon**（目前而言主要关注**Asian monsoon**），因此若要细读的话，可以主要看有关这一part的，至于对其他地方的影响，结论太多不好记忆。

另外还有一篇是刊登在nature上的一篇论文，估计有30多个共同作者，且都是这一领域的大牛（不过没有老板）。这篇文章则主要集中于ENSO的多样性及其物理机制，还有ENSO的预报。和老板的关注点不同。   
> Timmermann, A., et al. (2018). "El Nino-Southern Oscillation complexity." Nature 559(7715): 535-545.   

在看这两篇综述文献时，发现其引用的一些参考文献我都曾看过，但现在却完全想不起来他的研究方法和结论。看来一些经典的文章还是需要多读呀。比如老板1992年的文章，还有WangBin 2000的文章（讲ENSO通过怎样的遥相关影响东亚）。

# 一 Bjerknes Stability Index
![](http://wx4.sinaimg.cn/mw690/006fa9Xlgy1fw13oqmlotj30qp0i2dnq.jpg)    
图中红色的为正反馈，蓝色的为负反馈。奇怪的是，已知四种正反馈，但这里少了Bjerkness Feedback。当然这里的两种负反馈也从未听说过。  

The BJ index is used to assess the growth rate of ENSO in models and observations.   
Assessed using coefficients representing processes in ENSO and variable (e.g. h, Q, T…) mean states.   
**I**<sub>BJ</sub> < 0 the leading ENSO mode is damped, and for **I**<sub>BJ</sub> > 0 the leading mode is unstable.

一般认为1997/98的EINino是最强的，其次是1982/83。

# 二 Timmermann 2018 El Nino-Southern Oscillation complexity
非常喜欢这篇文章的构图，很新颖。且每一幅图的信息量都比较大。  
此外，这篇文章在第二页中有一个表格，罗列与ENSO有关的术语，个人感觉非常有用，可以说是扫盲了。现将其中一些翻译如下：

- **东太平洋冷舌Eastern Pacifc cold tongue**：指气候态下，东太平洋海温因上升流而较冷，但在EINino年会异常偏暖   
- **西太平洋暖池Western Pacifc Warm Pool**：气候态下，西太平洋海温较高，一般高于28摄氏度。西太暖池的南北季节性移动对EINino的结束有重要作用   
- **ENSO skewness（倾斜）**：指EINino和LaNina海温变化幅度的不对称，一般情况下EINino的幅度大于LaNina。这种倾斜也表明了ENSO循环的非线性  
- **西风事件Westerly wind event（WWE）**：太平洋西部中部的天气系统往往与赤道信风的突然减弱有关，从而产生下传的开尔文波，使暖池向东扩展  
- **Equatorial Kelvin wave**：发生在海洋表面暖水层和次表冷水层交界面、向东传播的海洋内部波动。赤道异常西风能产生向下的东传Kelvin波，使得东太平洋温跃层变厚，表层海水增暖。赤道异常东风能产生向上的东传Kelvin波，使得东太平洋温跃层变浅，表层海水变冷。   
- **Z20**：20摄氏度等温线深度，可以表征温跃层厚度。   
- **Combination tones/C-mode**：ENSO被季节年循环非线性调节后产生的9个月或15-18个月的谱能量。或者说是**I**<sub>BJ</sub>的季节年循环和ENSO海温信号的年际变化相互作用产生的9个月或15-18个月的周期。c-mode（combination mode）在EINino的季节转变中起到重要作用。  

EINino和LaNina之间的转换是全球气候系统中最强的年际波动。本文主要介绍了目前关于其时空复杂性的研究情况。

EINino的观念已经从以往其典型的由爆发到成熟再到消亡的发展过程过渡到现在解释其时空复杂性和变化的气候影响。ENSO的复杂性体现在模态、振幅、时间演变的多样性。   
古气候学者重构了过去一万年的ENSO现象，依然表明有很大的振幅变化，从而强调了内部气候过程在调节ENSO复杂性中的重要作用。   
ENSO现象的重构也表明ENSO在工业革命后有加强的趋势，于是人们开始研究外部强迫（全球变暖）对ENSO演变及其强度的影响。   

## 1. A conceptual view of ENSO dynamics  
![](http://wx2.sinaimg.cn/mw690/006fa9Xlgy1fw42bgb1kjj30j104974r.jpg)   
从ENSO再充电机制出发，认为当**I**<sub>BJ</sub>为常数时，东太平洋海温**T**<sub>e</sub>和纬向平均温跃层厚度**h**应是线性关系，但从图2发现两者明显不是线性的。**对于为什么是线性的，不太理解，或许需要去看一下下面的出处文章**   
> Jin, F.-F. (1997). "An Equatorial Ocean Recharge Paradigm for ENSO. Part I: Conceptual Model." Journal of the Atmospheric Sciences 54(7): 811-829.    
> Jin, F.-F., et al. (2006). "A coupled-stability index for ENSO." Geophysical Research Letters 33(23).

当**I**<sub>BJ</sub>包含大气或海洋的非线性过程或多元随机强迫时，该模式即可描述ENSO的skewness以及从中等强度到强的快速发展过程。   
由此强调了非线性动力和热力过程在耦合气候系统中的作用。当上述模型只能模拟ENSO发展过程中的一些特点，无法解释其空间分布及遥相关类型的不同。   

## 2. Space–time complexity of ENSO   
![](http://wx2.sinaimg.cn/mw690/006fa9Xlgy1fw42onvcrnj310j08lwit.jpg)   
为抓住ENSO的时空变化特征，对赤道海温做EOF（从左边的功率谱分析单位为年，推断此处是用冬季平均海温做的EOF），得到两个主要模态。第一模态为EP型，呈现准四年周期。第二模态呈现准两年周期。  

## 3. Seasonal ENSO dynamics  

## 4. ENSO predictability  

## 5. A unifying framework  

## 6. Outlook

# 三 YangS 2018 El Niño–Southern Oscillation and Its Impact in the Changing Climate
## 1. Introduction  
## 2. Fundamentals of ENSO  
### 2.1 ENSO characteristics  

### 2.2 Conventional views of ENSO dynamics   
主要介绍了以下四种结束ENSO现象的负反馈现象。

- **2.2.1 The delayed oscillator** 有西风异常时，冷的罗斯贝波（西传）和暖的开尔文波（东传）的传播角度出发   

- **2.2.2 The discharge/recharge oscillator** 赤道中太平洋西风异常及对应的（向极地的）斯韦尔德鲁普输送异常导致赤道太平洋热容量出现负异常  

- **2.2.3 The western Pacific oscillator** 在正位相时，赤道外西太平洋局地海洋-大气相互作用形成反气旋，赤道有异常东风，激起东传冷的开尔文波  

- **2.2.4 The advective-reflective oscillator** 认为与海洋波动对应的海洋环流的热平流效应会影响暖池东边界的移动，进而发生ENSO位相转换（与之相关的文章发在1997年的Science上） 

另外，还有四种激发ENSO现象的正反馈过程（这在另一偏综述文章中有介绍），其情况如下图所示，其中被广泛认可的是 **Bjerkness Feedback**。  
![](http://wx1.sinaimg.cn/mw690/006fa9Xlgy1fvm4epj5j6j311f0l9tjq.jpg) 

### 2.3 View on ENSO diversity  

- **2.3.1 Displacement of the thermocline dynamics** 认为，由于赤道太平洋区域的温跃层压扁，使温跃层的上升区由太平洋东部转移到太平洋中部，从而出现CP型EI Nino。该观点认为CP型的出现并不是因为ENSO动力过程的变化，只是发生区域的转换 

- **2.3.2 Zonal advective feedback (favoring CP type) vs thermocline feedback (favoring EP type)**  

- **2.3.3 Subtropical forcing mechanism** 先在美国的加利福尼亚地区产生海温异常，随后这个副热带地区的海温异常向西南方向传播来到赤道太平洋，随后赤道太平洋局地海气相互作用以及海洋水平平流作用是该异常海温最后成长为CP  

## 3. The ENSO teleconnection mechanisms  
### 3.1 ENSO teleconnections within the tropics  

- **3.1.1 Atmospheric bridge and tropical tropospheric mechanisms** 能使ENSO影响印度洋和大西洋的两大机制。  
一是与Walker环流有关的大气桥，赤道太平洋强对流活动的东移减弱了Walker环流在西太平洋的上升支，在赤道印度洋东部产生异常下沉支，并通过太阳辐射和潜热通量加热印度洋，对大西洋的作用类似，。可以看一下这篇参考文献  
> Alexander, MA, Bladé, I, Newman, M et al. The atmospheric bridge: The influence of ENSO
teleconnections on air-sea interaction over the global oceans. J Clim 2002; 15: 2205–31.   

二是赤道对流层加热/冷却机制激发西传Rossby波和东传的Kelvin波，此处可以看参考文献  
> Chiang, JCH, Sobel, AH. Tropical tropospheric temperature variations caused by ENSO and their influence on the remote tropical climate. J Clim 2002; 15: 2616–31.。  

- **3.1.2 Additional mechanisms for the tropical Atlantic Ocean** EINino期间，北大西洋赤道（TNA）变暖   
EINino在赤道大西洋激起异常下沉运动，再通过Walker环流在大西洋副热带地区引起异常上升运动。于是大西洋副热带高压减弱，东北信风减弱，从而使北大西洋赤道海温有正异常。该正异常从ENSO次年春季达到顶峰并可维持到夏季。    
除上述从纬圈环流和经圈环流出发的解释外，还有从中纬度波列出发的解释。认为由EINino激发的**太平洋—北美遥相关**在美国东南部有一异常中心，该异常中心可以扩展至大西洋并减弱大西洋副高，从而导致TNA增暖。

- **3.1.3 Additional oceanic mechanisms for the tropical Indian Ocean**  
ENSO可以激发印度洋整个海盆的变暖（冷）或IOD，这里主要介绍了激发IOD的可能物理机制。  
ENSO正位相激发IOD正位相（印度洋西部比东部暖）  
随着CP型EINino发生次数的增加，ENSO对印度洋的影响也发生了变化（激发的印度洋SSTA可能会减弱）  

### 3.2 Downstream ENSO teleconnections to the Northern and Southern Hemispheres  

- **3.2.1 The PNA and TNH wave train mechanisms in the Northern Hemisphere**  
- **3.2.2 The PSA wave train mechanism to the Southern Hemisphere**  
CP对南半球的影响更剧烈  

- **3.2.3 Jet stream displacement mechanisms**  
EINino期间，赤道对流层变暖加强并缩小了Hadley环流，使得副热带急流位置向赤道偏移同时影响斜压涡旋的中心位置，在中纬度激起异常上升运动 

### 3.3 Upstream ENSO teleconnections to western Pacific and East Asia  
在赤道冷源或热源西边能激发一对西传的罗斯贝波，但这还无法解释ENSO在次年夏季对西北太平洋以及东亚的影响。为解释该影响有两种机制提出。  
一是WangBin等人2000年提出的局地海气相互作用，通过两次Gill响应在西北太平洋产生异常反气旋，加强西太副高，从而影响东亚的天气和气候。  
二是谢尚平等人2009年提出的印度洋电容器机制。在EINino成熟期，印度洋变暖，通过局地海气相互作用，印度洋的暖信号能维持到次年夏季。此外，印度洋变暖能在大气中激发向东传播的暖Kelvin波。由于地面摩擦，Kelvin波的北支在副热带产生辅散，进而加强西太副高。  
此外，EINino也能通过赤道大西洋的海温异常影响次年夏季的西太副高。  
此外，Jin F-F等人2013年提出的由ENSO和西太年循环非线性相互作用形成的C-mode模型也能影响西太副高的强度  

**question：为什么我记得之前看介绍ENSO和东亚季风相互作用的文章时有介绍到很多种影响机制呢？为什么这里只涉及了四种呢？**

## 4. The changing ENSO and its climate impact  
### 4.1 Long-term changes in ENSO  
在年代际尺度上，ENSO自1970年以来，正面临振幅增大和时间延长的趋势。有学者认为这与温室气体浓度有关，但也有学者不认同。因为在CMIP5中，即便是相同的温室气体浓度序列，ENSO在不同模式中的表现不同。

### 4.2 The changing impact of ENSO  
大气对西太海温异常或海温梯度的变化非常敏感。但对东太海温的变化则不是那么敏感，这或许是因为东太的气候态海温低于发生对流的临界值。随着CP发生次数的增多，中太平洋的海温高于东太平洋，因此尤其引发的降水和温度影响也将发生巨大变化。 
 
- **4.2.1 The changing impacts on tropical oceans**   
ENSO和IOD的变化在1950年代前相对独立，但在1970年后，由于赤道印度洋东部温跃层加深，两者的关系变得紧密。  
此外，CP对赤道北大西洋增暖的影响不如EP来得强烈，但EP和CP对赤道南大西洋增暖的影响强度是一致的。  

- **4.2.2 The changing impacts on North America climate**  
EP能使北美北部（加拿大和美国北部）异常变暖，北美南部异常变冷。但在CP情况下，美国西北部（暖）和东南部（冷）的温度对其比较敏感。  
此外，在CP情况下，在美国西部，易呈现出北干南湿的状况，但在EP型时，美国西部整体偏湿。

- **4.2.3 The changing impacts on Asian and Australian monsoons**  
发现两篇老板的文章
有学者指出CP在东亚三极型降水形成过程中的重要作用
大多数模式结果表明，在全球变暖的背景下，ENSO和南亚季风间的关系减弱，只有四个模式表明这种关系没有减弱。

- **4.2.4 The changing impacts on tropical cyclones**  
一般情况下，EINino时期的台风会比LaNina时期的弱。CP下，西北太平洋台风频率和强度会比EP高。而在EP情况下，由于西太副高位置的变动，使得台风更易在中国登陆。

- **4.2.5 The changing impacts on midlatitude and polar climate**  


## 5. ENSO in the future
5.1 Changes in intensity and frequency  

- 5.1.1 Model consensus  

- 5.1.2 Diversity in ENSO intensity and frequency 
 
5.2 Change in the type of ENSO  

5.3 Changes in ENSO impacts  

## 6. Summary and discussions
