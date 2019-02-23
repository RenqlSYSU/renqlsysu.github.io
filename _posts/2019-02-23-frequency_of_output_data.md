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
- 第二行是指定输出变量频率，第一个数字为0，表示用默认的输出频率，即输出月平均数据，第二个数字小于0，表示每隔24小时输出一个文件
- 第三行指定一个输出文件中包含几个时次的数据
- 第四行指定第二个输出频率对应需要的输出变量，而第一个逐月的数据文件则采用默认的输出方式。
- 在这四行代码中，模式一共会输出两种频率类型（逐月，逐日）的数据文件。

更具体的变量名解释可以在以下网址找到：<a href="http://www.cesm.ucar.edu/cgi-bin/eaton/namelist/nldef2html-cam5_3" target="_blank">http://www.cesm.ucar.edu/cgi-bin/eaton/namelist/nldef2html-cam5_3</a>

```
avgflag_pertape = 'A','A'
nhtfrq = 0,-24                                                                            
mfilt  = 1,1                                                                              
fincl2 = 'FLDS','FLNS','FLNT','FLUT','FSDS','FSNS','FSNT','LHFLX','OMEGA','PRECC','PRECL','PSL','PS','RELHUM','Q','SHFLX', 'T','TMQ','TS','U','V','Z3'
```

这一步需要在 build 前修改，若已经build过了，可以在 **user_nl_cam** 修改过后再重新 build 一下，或者直接修改 exe/ 文件夹中的 **atm_in**。
