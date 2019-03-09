---
layout: post
title: CESM的特殊运行案例
categories: 模式学习
tags: restart branch 计算节点修改
author: renql
---

* content
{:toc}

# 1 Continue Run
想要在原来已跑好实验的基础上再积分10年，可以有两种方法：

- 一、修改 **env_run。xml** 中的 ` CONTINUE_RUN = TRUE `，然后 `./$casename.run`，但这种做法似乎无法修改输出数据的频率，即输出数据的频率和该实验之前一样。    

- 二、修改 **env_run。xml** 中的 ` RUN_TYPE = branch `，然后再修改 **RUN_REFCASE, RUN_REFDATE**，其中若 **RUN_REFCASE** 等同于 **casename**，那么需要设置 ` BRNCH_RETAIN_CASENAME = TRUE `， 然后 `./$casename.run`

若在继续积分的同时，需要修改计算的节点数，则需要修改 **env_mach_pes.xml** 中的 **NTASKS**等参数，可以直接从其他case中复制相应的 **env_mach_pes.xml**，但随后需要做如下操作，才会生效  
```bash
./cesm_setup -clean
./cesm_setup
./$casename.build
./$casename.run
```

此外，可以通过查看 **CaseStatus** 文件来查看目前对该case都进行过哪些操作

# 2 Branch Run
