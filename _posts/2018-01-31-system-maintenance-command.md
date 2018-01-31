---
layout: post
title:  "20180131 linux系统维护常用命令"
categories: linux
tags: linux 整理
author: renql
---

* content
{:toc}

# 压缩包命令 #
    tar -zxv -f filename.tar.gz -c directory  #将压缩包解压在directory文件夹下
    tar -jxv -f filename.tar.bz2 -c directory #将压缩包解压在directory文件夹下






#源代码软件安装命令#

./configure --prefix=/usr/local/test
卸载程序用make uninstall

# 查看存储空间 #
    df -h #将以人类可以阅读的容量格式显示各挂载点的存储空间使用情况
    free -h #将以人类可以阅读的容量格式显示内存使用情况
    fdisk -l #查看硬盘及分区情况

linux中文件名若有空格的解决方法：在空格前加反斜杠\,例如文件名为“software package”，在Linux中可表示为“software\ package"

恢复成系统缺省的.bashrc: `cp /etc/skel/.bashrc ~`
