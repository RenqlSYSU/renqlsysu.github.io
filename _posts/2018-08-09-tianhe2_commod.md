---
layout: post
title: 天河登录注意点与作业提交方式
categories: 模式学习 linux
tags: 天河
author: renql
---

* content
{:toc}

## 关于远程登录天河2号VPN

最近在香港远程登录天河VPN，之前一直断线，后来使用Teamviewer远程办公室台式机再连天河VPN会好一些，但非常卡，很影响编程体验。
不过，WP用苹果电脑则不容易断线，猜想是否是有线网和无线网的原因。而WT在美国使用无线网连天河也不容易断线，不过他用的是putty。

于是我也将远程软件换成putty，并每隔2s时间ping一下，于是也不容易断网了,于是猜想是和远程软件有关，
但LZN用shell设置每隔2s时间ping一次后，也不容易断了。由此得出结论是与信跳信号的发送时间间隔有关。

顺利解决天河VPN的问题后，用天河ssh团队服务器，再ssh学校四期平台，再也不卡了，使用体验一级棒。以下是putty及ssh的一些教程。

在putty里面怎样选中、复制粘贴：http://www.phperz.com/article/16/0131/188674.html  

SSH原理与运用（一）：远程登录：http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html


## tianhe2的计算资源

天河二号共有16,000个运算节点，每节点配备两颗Xeon E5 12核心的中央处理器、三个Xeon Phi 57核心的协处理器（运算加速卡）。即一个节点共有12*2=24核，按照每个核的计算时间计价。

## tianhe2关于作业的常用命令  
天河上关于提交任务的常用命令：   
```bash
  yhrun -n 1 -N 1 -c 1 -p work -J index ncl ./calc_sf_index.ncl  # 交互式提交作业  
# 需要运行一个任务，请分配一个节点一个处理器，在work分区工作，任务名为index  
# 注意：在登录节点不能运行大程序，否则系统会将他kill，此时需要用提交作业的方式运行   
# 但由于该命令是交互式的，因此如果登录界面断了的话，该工作也会断，解决办法即将这句话写到一个sh文件中，然后用yhbatch命令   

  yhbatch -p work -N 3 -n 64 -J pSSTclim /WORK/cesm/F/pSSTclim/pSSTclim.sh   # 提交后台批处理作业
#批处理作业的脚本为一个文本文件（只能是sh或bash的支持），而sh文件中只有三句话，如下    
		#!/bin/bash   
		cd /HOME/sysu_hjkx_ys/WORKSPACE/L_Zealot/cesm/F/pSSTclim/run
		yhrun -p work -N 3 -n 64 -J lzn_pSSTclim --cpu_bind=rank ./pSSTclim/bld/cesm.exe >& cesm.log

  yhcancel $jobid  # kill a job 
  
  yhi    # query the situation of all nodes  
# "idle" mean it is free, "alloc" mean it is working
         
  yhq    # query the situation of jobs   
# "R" mean it is running, "CG" mean it is killed, "PD" mean it is waiting
```
## 四期提交CESM作业的命令：   
四期的计算节点为曙光 TC4600 双路 CB60-G10 刀片， 共 72 片， 每块刀片均配备 2 颗主频为 2.6GHz 的 Intel 8 核 CPU， 64GB 内存； 其它节点为曙光 I620r-G10， 配备 2 颗主频为 2.6GHz 的 Intel 8 核 CPU， 32GB 内存； 文件系统采用曙光 Parastor200 并行文件系统，并行文件系统采用双副本，裸容量为 330TB。  
所以每个计算节点有16核

```bash
./$CASENAME.run   #该脚本会通过呼叫 run.pbs 来最终提交任务

# 命令提交后删除的方法
qdel [-W delay|force] job_id
```
