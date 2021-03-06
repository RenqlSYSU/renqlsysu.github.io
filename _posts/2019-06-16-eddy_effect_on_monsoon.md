---
layout: post
title: 定常涡旋对季风的影响
categories: 文献笔记
tags: eddy monsoon
author: renql
---

* content
{:toc}

由于我的工作中需要强调瞬变扰动对东亚季风的影响，因此最近抱着目的再次重读 Schneider 2008年的两篇文章。虽然他的文章更强调空间尺度上的中尺度涡旋对季风爆发以及Hadley环流转变的作用，但我觉得**中尺度涡旋**只要不是定常的，只要他在移动，他就是**瞬变扰动**的一部分，两者应该是相通的。

## Eddy对Hadley环流季节转变的作用 ##

> Schneider, T. and S. Bordoni (2008). "Eddy-mediated regime transitions in the seasonal cycle of a Hadley circulation and implications for monsoon dynamics." Journal of the Atmospheric Sciences 65(3): 915-934.  

### Abstract ###
在一个没有水循环、有纬向对称边界条件的理想干实验模拟中，发现Hadley环流在一年中有两个明显不同的阶段，根据大尺度扰动动量通量的强度划分。  
- 夏半球和春秋分时期的Hadley环流中心位于一个上层有西风急流、有明显涡旋动量通量辐散的纬度带，涡旋动量通量对环流强度的影响很强。  
- 跨赤道冬半球Hadley环流中心位于上空有东风的纬度，不受中纬度涡旋能量的影响;涡旋动量通量对环流强度的影响较弱。  

经**涡旋通量**、**高层平均纬向风**以及**平均经圈环流**三者之间的相互作用调节，Hadley环流中心的**纬向动量平衡**由夏季涡旋主导动量通量过渡到冬季由平均经圈环流主导  
在过渡期间，包括**底层温度平流强度变化**以及**冬夏季环流边界的纬度变化**间的反馈影响着冬季越赤道环流的强度  
这个转变有些类似于季风的爆发与衰退。  
因此模拟实验中这种与**海陆对比及其他纬向不均一**无关的动力机制或许与大气大尺度季风动力学有关

看完摘要后，希望在文中了解到的问题：  
1. 为什么夏半球Hadley环流是涡旋主导动量通量，冬半球Hadley环流是平均经圈环流主导动量通量？（夏季时，夏半球就是北半球，东半球就是南半球） 
2. 如何计算涡旋动量通量？  
3. 看摘要的意思是说，涡旋动量通量的调节作用使季风的爆发与衰退存在突发性？




### 1. Introduction ###
In Earth’s atmosphere, large-scale eddy momentum fluxes strongly influence the strength of the summer Hadley cell but less strongly influence the strength of the cross-equatorial winter Hadley cell. 

在环流的上支，摩擦过程以及动量的垂直输送可以忽略，因此流线水平，其统计定常状态下的纬向平均动量方程表明**Hadley环流的强度**（垂直积分的经向质量输送）与**科氏常数、局地Rossby数、涡旋动量通量辐散**有关。局地Rossby数衡量了涡旋动量通量辐散对Hadley环流强度的影响程度，  
- 当局地Rossby数趋于0时，角动量等值线趋于垂直分布，经向环流强度与涡旋动量通量散度密切相关。  
- 当局地Rossby数趋于1时，角动量等值线趋于水平分布，经向环流强度与涡旋动量通量散度无关。  
- 夏半球Hadley环流上支的局地Rossby数小于0.2，冬半球的则大于0.5。根据再分析资料计算，亚洲夏季风反气旋内的局地Rossby数可以达到 0.7

Hadley环流对热源驱动力的响应取决于涡旋动量通量对它强度的影响。当Hadley环流强度由涡旋动量通量主导时，他对热力驱动变化的响应不直接，他只能通过对涡旋动量通量变化或Hadley环流范围变化来间接响应热力驱动的变化。局地Rossby数的季节转变意味着，Hadley环流对热力驱动响应的季节变化

这篇文章主要是利用理想干模式研究Hadley环流动力形态发生季节转变的可能机制

### 2. Idealized GCM ###
利用辐射平衡温度的牛顿松弛方法来代表辐射加热与冷却。辐射平衡温度随着高度下降，直到大气顶的200k。  
大气内部的牛顿松弛时间为50天，地表的牛顿松弛因子则从太阳直射点的7天逐渐增大为50天。这主要是为了补偿模式地表热惯性的缺失  
尽管由牛顿松弛方法制造的辐射加热率与真实的有出入，但为了简便，还是称其为辐射加热率。

当大气内部的牛顿松弛时间为25天时，Hadley环流的下支占据了半个对流层，这与实际不符。我个人觉得这可能是因为牛顿松弛因子的缩小，地表对大气的加热率放大，大气升温快，因此大气流动增强？  

另外还介绍到模式中关于边界层湍流混合、层结稳定度等内容的处理。

### 3. Statistically steady states ###
冬半球的越赤道Hadley环流强度与太阳直射点间的关系：当太阳直射点的纬度小于9度时，强度随纬度的变化较弱。当太阳直射点的纬度大于9度时，强度随纬度的变化变得明显。这与其之前的工作结果类似。

### 7. Implications for monsoon dynamics ###
包含波流相互作用、非线性平均流过程的反馈或许可以作用于大尺度亚洲夏季风的爆发与衰退。（北美季风属于小尺度季风系统，由其他动力机制所控制）  
由于上述动力机制可以在没有海陆对比或其他表层不均一的情况下发生作用，如果这个猜想正确，就表明副热带的地形在季风转变过程中所起的作用是提供一个低的热惯性，使得上述反馈得以在季节内尺度作用，从而使得地表温度大值区、冬夏半球Hadley环流边界迅速向极移动。

### 8. Open questions ###
上述研究都是定性分析，还存在以下这些定量问题亟待解决：  
1. 当黄赤交角为多少度时，会发生这种转变？  
2. 在这两种情况下，Hadley环流的经向范围及强度如何依赖于外部因素，如太阳辐射的强度及半球间的不对称？  
3. 低层辐合带的强度和位置如何依赖于外部因素和大规模环流?非线性动量平流和边界层内湍流应力的非线性和显式剪切关系在控制辐合区的强度和位置方面的定量作用是什么?  
4. 是什么决定了Hadley环流的总稳定性(经向质量通量的垂直结构)及其随纬度的变化  

基于夏半球Hadley环流中eddy通量所起的重要作用以及区域转变过程中波流相互作用的重要性，问题1与2无法用轴对称环流理论解决。  
可以利用在浅水方程或两层模式中考虑依赖于平均环流的涡旋通量来研究上述两个问题。  

## Prive,Plumb,2007, Monsoon Dynamics with Interactive Forcing. Part I: Axisymmetric Studies
季风形成的经典理论认为它是由海陆热力对比产生的海陆风。**但这一理论无法解释季风的某些特征，如延迟爆发、活跃与中断期**，对于这个大尺度环流而言，这个理论也没有考虑地球旋转的效应。另一种看法认为季风是ITCZ季节性移动的结果，而这正是该文的关注点。

观测到的纬向平均季风环流描述了一个在季风区上升，高层大气流向冬半球，随后在冬半球热带下沉并在底层回流的全球径向环流圈。Gill (1980)利用一个线性浅水模式发现热带赤道外的一个局地强迫能驱动出一个类似季风的跨赤道环流。然而，Held and Hou (1980), Lindzen and Hou (1988)以及Plumb and Hou (1992)发现轴对称的Hadley环流是非线性的，并基于自由对流层角动量守恒对其进行了预测。**该文的目的是探讨定常Hadley环流的非线性及轴对称理论在描述季风动力学时的有效性**。

Held and Hou(1980)扩展了Hide(1969)和Schneider(1977)的工作，利用角动量守恒概念来解释年平均Hadley环流的发展。Lindzen and Hou
(1988)则探究了单个Hadley环流对至日强迫的动力响应的优势。**Plumb and Hou (1992)探究了干、轴对称大气对局地副热带强迫的响应，发现角动量守恒经向环流发展的临界条件是——热平衡状态中存在角动量极值。**Emanuel(1995)在假定一个湿绝热温度垂直递减率的情况下，利用Maxwell关系推导出了这个临界值。Zheng(1998)用一个由固定的局地副热带SST扰动区域的湿、轴对称水球证实了这个临界行为。

**很多学者认为可以用临界行为理论来解释季风的某些特征，例如季风的突然爆发**。Eltahir and Gong (1996)发现云下湿焓的副热带径向梯度与西非季风的强度存在正相关。

但现存Hadley环流的非线性理论存在一些局限性。**第一个局限性是Held and Hou (1980), Lindzen and Hou (1988)以及Plumb and Hou (1992)的工作都是基于具有指定辐射平衡温度分布的干大气模式。**但在干大气中，强迫激发的环流不会改变强迫场，但在真实大气中，强迫高度依赖于环流。在Emanuel(1995)和Zheng(1998)的湿实验中，用给定的海温扰动强迫大气，用满足湿绝热的辐射对流平衡温度与地表强迫交流。在由地表通量驱动的干大陆上，垂直气柱接近于干绝热，且上层温度可能会相对比较冷即便底层温度很高。这提出了一个问题：**干大陆上的强感热通量是否足以驱动出一个季风环流。即便假设环流与强迫之间存在相互作用，也无法仅从辐射对流平衡来预报季风的位置与强度**

**第二个缺陷是，这些非线性理论主要都关注定常环流，而不是随时间变化的季风。**轴对称模式中的环流若要达到定常状态需要几百天，远远超出了与季风相关的季节长度。Fang and Tung (1999)发现当定常强迫移出赤道外时观测到的环流强度突然增加在使用瞬变强迫时没有出现。

除了Hadley环流的理论和模式外，轴对称已专门应用于季风环流，例如Webster(1983)和Goswami and Shukla(1984)。这些研究都关注于季风的季节内变化，并发现季风动力与地表热通量的相互作用对季风的瞬变行为有贡献。**这篇文章利用与前人类似的方法，但关注点在于定常的季风**。

为了解决Hadley环流的非线性轴对称理论在交互式季风中的适用性，该文希望**利用一个轴对称大气环流模式**来解决以下问题：  
1. 有交互式强迫的副热带大陆对季风环流的影响？  
2. 如何确定季风的位置和范围？  
3. 定常季风环流是否能代表瞬变季风的动力学？

该文将轴对称模拟作为理解大尺度季风环流的第一步。**观测到的季风是非对称的，因此严格的轴对称理论的适用性存在问题**。非对称环流的问题会在另一篇文章中解决，现在的工作主要解决纯粹轴对称的例子。

在用理想轴对称理论模拟季风和基于真实物理过程的综合GCM模拟季风间存在很大的差距。虽然轴对称理论在理解驱动和影响季风的物理机制上很有用，但目前不清楚哪些简化会限制该模式对季风的适用性。另一个方面，综合GCM中丰富反馈的存在使得季风动力学的诊断异常困难。**该工作的目的是在理想轴对称理论和更为复杂、交互式的季风间搭桥梁。**该文利用具有简化的物理过程及理想陆地的模式来实现中等复杂性。这可以对可能是季风本质的过程进行一个相对合理与真实的刻画，同时减少反馈，使分析更可控。

**实验第一步是描述全水球中Hadley环流对定常局地副热带强迫的响应**。该全水球实验是一个基准实验，主要是与后面带有副热带大陆的、更为复杂的实验做对比。**副热带强迫以海温扰动的形式出现，其形式旨在模拟陆地的存在，以便与大陆实验进行直接比较。**在这个全水球实验中也发现了以往研究所预测的临界行为。随着强迫向极移动，环流强度减弱。

**第二步，用持续夏季强迫驱动、有副热带大陆的实验同全水球模式做对比，有助于理解大陆物理特性对季风环流的影响。**尽管环流呈现出一个从局地到全球尺度的转变，如非线性理论所预测的那样，但环流强度的临界行为没有全水球实验中那么明显。**发现季风环流的零线往往与云下湿静力能最大处吻合，表明边界层热力学可以控制季风的范围和位置。**在海洋上，湿静力能与海表温度密切相关，但在陆地上，湿静力能受大尺度平流和地表热通量的控制。

**最后一步是用陆地上季节变化的强迫进行模拟，并于持续夏季强迫的实验进行对比，来探究定常解对瞬变季风的适用性。**瞬变响应在夏季中后期达到持续夏季强迫驱动的环流，但夏季早期的状态与定常解不太一样。瞬态响应的时间尺度是热带对流层上层大规模翻转环流沿角动量线折叠所需要的时间尺度。

## Prive,Plumb,2007, Monsoon Dynamics with Interactive Forcing. Part II: Impact of Eddies and Asymmetric Geometries
上一篇文章表明角动量守恒环流的深厚上升支的位置与云下湿静力能的分布密切相关。**如果副热带局地强迫足够强，能引起这样一个径向环流，环流边界层的分离流线（此处在自由对流层没有水平平流）应位于纬向风垂直切变为0的地方。**在垂直方向湿绝热的热成风关系内，纬向风没有垂直切变的唯一区域是云下湿静力能径向梯度为0的地方。因此，在给定局地云下湿静力能的最大值后，环流向极一侧的边界同云下湿静力能最大值位于同一地方，而大尺度上升和最大降水则会发生在最大云下湿静力能向赤道一侧。在一系列轴对称模式研究中，季风位置与该理论有很好的一致性。

在第一篇文章中，Hadley环流的非线性理论在大尺度季风动力学中的适用性在一个轴对称模式中得到研究。其关注点在于**交互式强迫对季风动力学的影响**，发现**经圈环流导致的云下湿静力能平流能影响季风位置和强度。轴对称研究由于没有考虑纬向非对称和水平涡旋的影响因而存在局限性**，故无法解释观测到的季风非对称性。这一篇文章研究了三维环流中的季风行为。

一些研究试图通过探究**环流对特定局地热源的动力响应来了解季风环流**。这些研究强调了热带波动在决定大尺度环流上的作用。线性Gill模式（1980）就描绘了大气对赤道外局地热源的响应，以Kelvin波和Rossby波的形式。Hoskins and Rodwell(1995)利用一个相似的模式发现与特定非绝热加热有关的大尺度环流同观测环流类似，表明大气对热源响应的动力学基本上是线性的。Rodwell and Hoskins(1996)认为季风区域内产生的Rossby波会抑制季风西北侧的对流，从而造成东西不对称。轴对称模式下忽略了Rodwell-Hoskins效应及Gill类型的环流。**这些研究的一个重要局限性是缺少强迫和环流间的相互作用**。事实上，非绝热加热高度依赖于环流，其本身也是对外部强迫动力响应的一部分。

**湿空气被大尺度环流平流进入季风区是决定季风位置和强度的一个重要因子。**水汽提供和季风分布间的关系在很多允许环流与强迫相互作用的研究中得到强调。利用一个简单的矩形大陆，Cook and Gnanadesikan (1991) 发现由于地表水文的负反馈，降水很难出现在大陆内部。Dirmeyer (1998)发现位于有限纬向范围的副热带大陆上的季风主要由沿着东海岸的东风来提供水汽。当大陆纬向覆盖360度时，来自海洋的东风水汽输送缺失，季风减弱。Xie and Saiki (1999)则发现沿海岸线的底层东风急流内产生的斜压波动，通过在大陆上激发降水，在季风爆发中起到重要作用。他们的结果表明，如果没有这些斜压涡旋，季风爆发会变得更加困难甚至不可能。他们还发现大陆底层得气旋性环流通过抑制大陆西边的对流、促进大陆东边的降水，造成了季风的东西不对称。Chou等人(2001)发现来自冷的中纬度海洋的低湿静力能空气平流会抑制大陆西部对流，限制季风的向极扩展。而在第一篇文章中，作者发现来自热带海洋相对低湿静力能的空气平流对季风位置有一个重要影响。 

该文使用一个中间复杂度的模式，从而在简单模式和全三维交互式季风间建立过渡桥梁。由于完整的GCM中丰富的反馈过程使得诊断季风特征的难度增大，因此这里用的方法是从简单的框架开始，一步步增加模式的复杂度，从而揭示单一物理机制对季风的影响。可理解性是通过在一个完整的GCM中使用简单的大陆几何和理想化的物理参数来维护的。

第一篇文章用轴对称模式研究了交互式强迫对季风动力学的作用。虽然轴对称理论在理解驱动和影响季风的基本物理机制方面很有用，但不清楚这些简化会对结果有何影响。因此，该文探究了季风环流的三维结构，使用的模式同第一篇文章，都是MIT的GCM。实验有三组：  
1. 有副热带地形的二维模式  
2. 有纬向均一副热带地形的三维模式，同第一组实验对比可以得到涡旋对季风动力学的作用；  
3. 只有一部分经度有副热带地形的三维模式，可以探究纬向非对称强迫在驱动大尺度环流系统中的作用。
有两种海温分布：一是均一分布，二是有夏季海温梯度的分布。

**结果发现涡旋对纬向平均的季风有一个弱的减弱效应。涡旋可以强烈地影响环流的动量收支，但季风环流的定性表现不会有本质改变**。来自中纬度海洋的低云下湿静力能不利于季风环流的向极扩展。如果想要强降水发生在副热带大陆区域，那么低湿静力能平流需要被大地形所阻挡或者低湿静力能的源头被去掉。
