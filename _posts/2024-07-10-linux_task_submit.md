github博客的开头必须为：

---
layout: post
title: linux任务投递系统
categories: linux
tags: shell
author: renql
---

* content
{:toc}

# sge任务调度系统
任务状态：    
**qw **  表示等待状态
**Eqw ** 投递任务出错
**r**   表示任务正在运行
**dr**  节点挂了之后，删除任务就会出现这个状态，只有节点重启之后，任务才会消失

`qdel -u username` ： 删除某用户名下的所有任务
`qstat -u \*` ： 查看所有用户的任务
`for ((i=316893; i<=316907; i++)); do rm LW_OC.chr*.o${i}; done` 删除文件

```bash
#!/bin/bash
#$ -N meth_matrix  #任务名称
#$ -pe smp  4  # 作业请求使用一个具有共享内存并行（smp）环境的计算节点，并指定作业可以使用该节点上的 4 个处理器（或核心）进行并行计算。
#$ -l mem_free=20G # 作业请求了至少 20GB 的可用内存
#$ -l vf=20G # 作业请求了 10GB 的虚拟内存
#$ -cwd # 作业将在提交时的当前工作目录中执行
#$ -j y
#$ -o ~/stdout/

```

虚拟内存是指系统为了扩展物理内存而使用的一种技术，通常是物理内存加上硬盘空间。这意味着即使系统中没有足够的物理内存，作业也可以通过虚拟内存来执行，但性能可能会受到影响。

# sbatch任务投递系统
```bash
sbatch job.sh

sinfo # 查看资源状态
# idel为空闲，mix为节点部分核心可以使用，alloc为已被占用; 
# down表示该节点当前不可用，通常是由于硬件故障、网络问题或其他维护需要。节点处于这种状态时，无法分配给新的作业。

squeue # 查看作业队列

scancel 123 # 取消作业ID为123的作业
scancel -t PENDING -u `whoami` # 取消自己账号下所有状态为pending的作用
```

job.sh的脚本可以这样编写
```bash
#!/bin/bash
#SBATCH -J job.$sample # 作业名
#SBATCH -o job.$sample.%j.out 
#SBATCH --exclude=node8
#SBATCH --nodes=5
#SBATCH --ntasks-per-node=20
#SBATCH --cpus-per-task=1
#SBATCH --mem=6G

mpirun -np 100 python test.py

```
