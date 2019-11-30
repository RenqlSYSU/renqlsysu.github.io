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
想要在原来已跑好实验的基础上再积分10年，可以有两种方法。如果是模式跑到一半由于硬件原因（例如停电、服务器重启等原因）而中断，需要接着上一步继续积分，也可以用这两种方法。

- 一、修改 **env_run。xml** 中的 ` CONTINUE_RUN = TRUE ` ，然后 `./$casename.run` ，但这种做法似乎无法修改输出数据的频率，即输出数据的频率和该实验之前一样。这是因为restart的时候，模式不会再读atm_in文件。因此如果要修改atm_in里面的内容，最好用第二种方法continue run。    

- 二、修改 **env_run。xml** 中的 `RUN_TYPE = branch` ，然后再修改 **RUN_REFCASE, RUN_REFDATE**，其中若 **RUN_REFCASE** 等同于 **casename**，那么需要设置 ` BRNCH_RETAIN_CASENAME = TRUE ` ， 然后 `./$casename.run` 

但是上述两种操作，都需要有restart file。restart files的输出用 **REST_OPTION** 和 **REST_N** 来设置。因此如果跑的实验所需时间较长，最好设置这两项。 
**Restart files** allow the model to stop and then start again with **bit-for-bit** exact capability (i.e. the model output is exactly the same as if it had never been stopped).

若在继续积分的同时，需要修改计算的节点数，则需要修改 **env_mach_pes.xml** 中的 **NTASKS**等参数，可以直接从其他case中复制相应的 **env_mach_pes.xml**，但随后需要做如下操作，才会生效  
```bash
./cesm_setup -clean
./cesm_setup
./$casename.build
./$casename.run
```

此外，可以通过查看 **CaseStatus** 文件来查看目前对该case都进行过哪些操作

# 2 Branch Run
