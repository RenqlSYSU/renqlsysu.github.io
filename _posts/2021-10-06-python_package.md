---
layout: post
title: python简介
categories: python
tags: 气象包
author: renql
---

* content
{:toc}

最近开始转战python。虽然之前做过python课的助教，但真正要用的时候，还是有些不知所措。

作为解释型语言的python，相比于编译型语言Fortran，C+，速度比较慢，运行效率较低，不能脱离解释器独立运行，但可读性高。

相比于matlab，python免费。相比于ncl，同为解释型语言，python的优点在于各种开源库、机器学习框架、方便开发整合。

python的变量不需要提前申明，直接赋值就可以了，且可以随时改变变量的值和类型。在这一方面，python比fortran这些语言要方便些

# 气象常用python软件包
本人一开始拒绝使用python，也是因为他的包实在太多了，选择一多就容易选择困难，不如ncl来得简单方便，毕竟就那么几个函数。

但真的开始用python后，发现他虽然有很多软件包，但把每个包的主要功能了解清楚后，好像也没有那么难了。加上python的网上教程非常多，遇到什么问题，上网一搜就有答案。这一方面还是很好的

绘图：   
- **Cartopy**：地图投影、经纬度坐标、地图信息，搭配Matplotlib使用。 https://scitools.org.uk/cartopy/docs/latest/  
- **Matplotlib**：最常用的主要绘图包。 https://matplotlib.org/stable/gallery/index.html  
- **pillow**: 图像处理库，可以打开一张图片，对其进行裁剪、缩放、旋转、像素值处理等操作，我常用该函数制作gif动画。  
- **cmaps**: 提供ncl色标. https://github.com/hhuangwx/cmaps  

数据处理：   
- **Numpy**（数组与矩阵运算）：https://www.runoob.com/numpy/numpy-tutorial.html  
- **WRF-python** https://wrf-python.readthedocs.io/en/latest/basic_usage.html  
- **Pandas**（基于Numpy的结构化数据分析工具，可以CSV、JSON、SQL、Microsoft Excel 导入数据，主要数据结构是 Series （一维数据）与 DataFrame（二维数据，是一个表格型的数据结构））  
- **Xarray** (主要数据结构 Variable, DataArray, Dataset)  

另外一些比较小众的气象软件包：
- https://scitools-iris.readthedocs.io/en/latest/index.html  
- https://scitools.org.uk/iris/docs/v2.4.0/userguide/index.html  
- https://ajheaps.github.io/cf-plot/  
- https://ncas-cms.github.io/cf-python/tutorial.html  

尝试了一下cfplot，他在存图的时候竟然不能有路径，而且在什么路径下运行程序，图就存在什么路径下，且存成pdf时不能多页存储，我也是惊了
而且这个怎么画河流山地等信息呢？
缺点：比较小众，网上关于这方面的教程也比较少
优点：出图方便，代码简洁
cfplot：查看文件变量的方法 cfa

# 网上的学习例子
matplotlib简要介绍 https://blog.mazhangjing.com/2018/02/28/learn_matplotlib/#1-matplotlib%E7%AE%80%E8%A6%81%E4%BB%8B%E7%BB%8D
