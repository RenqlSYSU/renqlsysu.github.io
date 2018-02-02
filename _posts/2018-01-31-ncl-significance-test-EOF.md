---
layout: post
title:  "20180131 ncl显著性检验函数和EOF函数"
categories: ncl
tags: ncl 整理
author: renql
---

* content
{:toc}

```ncl
    copy_VarMeta(var_from,var_to) ;最常用的一个函数，因为若变量的LAT和LON坐标若没有定义单位等要素，画map图会报错
    time := cd_calendar(time,option) ;将混合日期转换为公历日期，且option=0时，输出数据会多一维
```
# 显著性检验函数 #




## 1、检验相关系数是否显著 ##
    rtest(相关系数r,样本数目n,0) # 用t分布检验相关系数是否显著，t=r*sqrt（（n-2）/（1-r**2））
返回统计概率值prob，当 `prob.lt.0.01` 时，说明其通过99%的显著性检验

## 2、两组样本均值差异是否显著 ##

    ttest(均值1，方差1，样本数1，均值2，方差2，样本数2，iflag，tval_opt)
iflag，为True表示两组样本有相同的总值方差，为False表示有不同的总值方差

tval_opt，为True表示返回统计概率值和student_t值，为False则只返回统计概率

当统计概率值.lt.置信度siglvl（例如0.05），则两组样本差异显著

##3、检验两组样本的方差是否有显著差别  ##
    ftest（方差1，样本数1，方差2，样本数2，0）
返回统计概率值prob


# 计算EOF的函数 #
## 1、计算EOF特征空间模态 ##
    optEOF 		= True
    optEOF@jopt = 1 #1表示用相关矩阵计算EOFs，0表示用协方差矩阵计算EOFs（默认）
    neval		= n #计算前n个EOFs模态
    eof			= eofunc_n_Wrap(data,neval,optEIF,dim) #计算data的前neval个空间模态
若输入的 data 为（time,nlat,nlon),则得到的为 eof(neval,nlat,nlon),且 eof 是标准化变量（每一空间模态的平方和=1），可通过乘上相应特征值的开方去标准化

同时，该函数还会以属性形式返回：**eval** 特征值（一维数组），**pcvar** 特征值方差贡献（一维数组）

用相关矩阵计算EOFs得到的各模态特征值比用协方差矩阵计算得到的小很多，且两者的特征值方差贡献也完全不一样。



- 当用相关矩阵计算EOFs时，相当于用标准化变量进行EOF分析，此时各个点的标准化变量可能相差不大，故能同时反映不同区域标准化变量的异常特征，反映的是变量场不同区域的相关情况



- 当用协方差矩阵计算EOFs时。相当于用距平变量进行EOF分析，此时EOF分析主要反映距平绝对值较大区域的主要异常特征

## 2、计算EOF各模态对应的时间系数 ##
    eof			= eofunc_n_Wrap(data,neval,optEIF,dim)
    optETS		= True
    optETS@jopt = 1 #指使用标准化数据矩阵计算时间序列，默认使用输入的data和eof（此时可设为False）
    eof_ts		= eofunc_ts_n_Wrap(data,eof,optETS,dim) #计算与eof对应的时间序列
若输入的 **data** 为 **(time,nlat,nlon)**, **eof(neval,nlat,nlon)**,则得到 **eof_ts（neval，time）** (减去均值后的值），同时以属性的形式返回 **ts_mean(neval)**,是 **eof_ts** 的均值

## 3、检验各模态的特征值是否显著与其他特征值分离 ##
    sig		= eofunc_north(eval特征值，时间样本数，prinfo) #也可用特征值的方差贡献pcvar做检验
**prinfo = True** 时，打印计算所得的 delta lambda、特征值、最低和最高界限以及分离的显著性

输入的eval或者pcvar只能是一维数组，返回一维逻辑型数组，表示特征值是否显著与其他特征值分离