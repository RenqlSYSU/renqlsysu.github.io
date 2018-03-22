---
layout: post
title: cesm模式运行流程
categories: 模式学习
tags: 整理 气候模式
author: renql
---

* content
{:toc}

# 一、运行CESM的一般流程 #
## 1. 设置CESM的环境变量，否则有些命令在其他目录下无法使用
```bash
source  ~/.bashrc_cesm
```

## 2. 创建案例
```bash
./create_newcase -case $CASENAME -compset B1850CN -res f19_g16 -mach yellowstone
#-case（案例名称）,-compset（模块设置类型）,-res（精度）,-mach（CESM机器）这四个参数是必须的
#./create_newcase后面可以跟-h（即help），-list（可列出后面可以跟的参数）
#-list后还可加[compsets, grids, machines]以列出相应参数可以有的内容是什么
```
<a href="http://www.cesm.ucar.edu/models/cesm1.2/cesm/doc/modelnl/compsets.html" target="_blank">compset name 网站超链接</a>

运行create_newcase后，生成的有用的文件：
- **README.case** 写有关于你这个案例的所有设置内容
- **CaseStatus** 写有你在何时对案例进行了何种操作，例如 build complete 2017-10-20 19:51:58
- **SourceMods** 若模式的代码有改动，则将改动后的代码放于该目录下

## 3. 修改env_*.xml文件 ##
修改方法：一直接用vi修改该文件，二用命令./xmlchange NTASKS = $NTASKS。  
修改的文件及相应可修改的内容有：  
- **env_mach_pes.xml** 在setup前修改，可修改 ntasks,nthrds,rootpe,ninst
- **env_build.xml** ，在build前修改，可修改 EXEROOT, CALENDAR (NO_LEAP)
- **env_run.xml** 在run前修改，可修改 RUNDIR, RUNTYPE(hybrid,branch,startup), STOP_OPTION, STOP_N, REST_OPTION, REST_N, RESUBMIT, DIN_LOC_ROOT, DIN_LOC_ROOT_CLMFORC，也可设置short term archiving and long term archiving，也可修改SST等强迫的文件路径

## 4. setup ##
```bash
./cesm_setup
```
可修改源代码（如加nudg，修改后的代码放在Sourcemod相应模块下）  
该操作后生成的有用的文件有：  
- **user_nl_xxx** 修改输入模式中的一些常量如CO2浓度、太阳辐射，也可设定输出数据的频率和类型（至于是否修改成功可通过运行preview_namelists来查看，可修改的常量在CaseDocs/xxx_in），在run前修改即可  
- **CaseDocs** 存放有各模块在run时需要用到的变量名，供参考  
- **env_derived** 存放有从其他设置中获得的环境变量，用户不能修改  

## 5. build ##
```bash
./$CASENAME.build
```
若build后又有修改源代码，可以直接build，不需要clean build 

## 6. run ##
```bash
./$CASENAME.run
```
提交作业，该命令实际会通过运行run.pbs来提交作业至集群系统中的多个节点。   
而run.pbs最后主要是通过mpirun运行EXEROOT下面的cesm.exe

# 二、关于两类runtype的解释 #
- **Branch**, 需要设定RUN_REFCASE和RUN_REFDATE, 机制同restart run（当CONTINUE_RUN是TRUE时），当两个case之间的各种参数都一样时，他们跑出来的数据也是一模一样的。常用于敏感性实验。  
- **Hybrid**，同startup，但他的初始化数据来自以往跑的一个算例的restart数据，有点类似branch但该设置的约束较少。也需要设定RUN_REFCASE和RUN_REFDATE ，当其各种参数设置同reference case时，其气候态数据也同reference case，但每一天的数据不一定一样。

# 三、师兄写的create_case.sh脚本 #
该脚本中主要定义了casename，compset，分辨率，运行时间（stop_option，stop_n），计算节点数及所用阵列，然后进行了$./cesm_setup并输出run.pbs文件
