---
layout: post
title: CESM模式输出数据种类及频率设置
categories: 模式学习
tags: model namelist
author: renql
---

* content
{:toc}

在 $casename 文件夹下的 **user_nl_cam** 中加入下面三行代码，其中  
- 第一行是：Sets the averaging flag for all variables on a particular history file series.The default is to use the averaging flags for each variable that are set in the code via calls to subroutine addfld. “A”代表平均。
- 第二行是指定输出变量频率
- 第四行代表是指定输出变量的

```
avgflag_pertape = 'A','A'
nhtfrq = 0,-24                                                                            
mfilt  = 1,1                                                                              
fincl2 = 'FLDS','FLNS','FLNT','FLUT','FSDS','FSNS','FSNT','LHFLX','OMEGA','PRECC','PRECL','PSL','PS','RELHUM','Q','SHFLX', 'T','TMQ','TS','U','V','Z3'
```
