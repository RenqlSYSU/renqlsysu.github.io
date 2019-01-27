---
layout: post
title: 再分析资料及降水资料
categories: 数据资料
tags: 整理
author: renql
---

* content
{:toc}

# 一、再分析资料 #
## 1.1 NCEP/NCAR reanalysis：NMC reanalysis (1949-now)
A state-of-the-art analysis/forecast system is used to perform data assimilation using data from 1948 to the 
present.

## 1.2 NCEP/DOE reanalysis 2 ：(1979-now)
NCEP-DOE Reanalysis 2 is an improved version of the NCEP Reanalysis I model that fixed errors and updated paramterizations of physical processes.

A state-of-the-art analysis/forecast system is used to perform data assimilation using data from 1979 
through 2003. A large subset of this data is available from PSD (Physical Sciences Division) in its original 4 
times daily format and as daily averages.

NECPI和NECP2 只有起始时间不同，精度都为2.5*2.5，有6h的，也有24小时的，也有月平均的数据，另外NECP2 的数据一般都是short类型。

## 1.3 ERA-Interim
全称：European Centre for Medium-Range Weather Forecasts (ECMWF) interim reanalysis
有subdaily，daily，monthly，   

优点：  
- TP的温度场和风场比**NECP-NCAR reanalysis**和**ERA-40**较准确 (WangMeiRong 2015, QBWO);  
- 全球季风降水的气候态、长期趋势及年际变化的代表性都较好 (WangMeiRong 2015, QBWO);  

数据介绍及批量下载方法：  
http://blog.sciencenet.cn/blog-430991-888904.html  
http://www.clarmy.net/2018/09/16/how-to-download-data-from-ecmwf-in-batch/  

## KNMI气候研究
http://climexp.knmi.nl，可提供各气候系统指数

# 二、降水资料 #
## 2.1 Global Precipitation Climatology Project (GPCP) ##
- 综合了卫星数据和雨量筒数据，海洋和陆地上的数据都有，有各种空间和时间（逐日、逐侯、逐月）分辨率的数据集，daily的数据从1996年10月开始，monthly的数据从1979年1月开始  
- 以往研究表明GPCP的降水数据在中国区域的偏差比CMAP的小(WangMeiRong 2015, QBWO)  
 
## 2.2 Global Precipitation Climatology Centre (GPCC) ##
- 由全球的站点观测数据得到的**逐月**降水数据，只有陆地上的，从1901年1月到现在  
- 看了官网介绍，好像也有**逐日**的数据资料，是2018年刚发布的，时间从1982年1月到2016年12月  
- 在<a href="https://www.dwd.de/EN/ourservices/gpcc/gpcc.html" target="_blank">GPCC Website</a>发现一个有趣的线上软件<a href="https://kunden.dwd.de/GPCC/Visualizer" target="_blank">GPCC Visualizer</a>，可以自己选择时间和月份画降水分布图

The precipitation data are from the Tropical Rainfall Measuring Mission (TRMM) Multisatellite 
Precipitation Analysis

降水数据：Climate Prediction Center (CPC) Merged Analysis of Precipitation (CMAP) dataset

