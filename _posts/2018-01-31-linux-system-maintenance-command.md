---
layout: post
title:  "20180131 linux系统维护常用命令"
categories: linux
tags: 压缩 存储空间
author: renql
---

* content
{:toc}

# 压缩包命令 #
```bash
    tar -zxv -f filename.tar.gz -c directory  #将压缩包解压在directory文件夹下
    tar -jxv -f filename.tar.bz2 -c directory #将压缩包解压在directory文件夹下
    tar –xZv -f file.tar.Z  # 解压 tar.Z 包
    tar –xv -f file.tar     # 解压tar包 
    
    # tar参数 -x 表示解压，-c 表示压缩，-t 表示查看内容，-r 表示向压缩归档文件末尾追加文件，-u 表示更新原压缩包中的文件
    # 这五个是独立命令，可以和别的命令连用但只能用其中一个
    tar -cjf all.tar.bz2 *.jpg   # 将所有.jpg的文件打成一个tar包，并用bzip2压缩
    tar -uf all.tar logo.gif     # 更新原来tar包中logo.gif文件
    
    unrar e file.rar  # rar包只能用 unrar解压，据说RAR for Linux不是免费的
    unzip file.zip    # zip包只能用 unzip解压
```
参考：   
https://www.jb51.net/LINUXjishu/43356.html  
https://www.cnblogs.com/yuandonghua/p/10254288.html  




# 源代码软件安装命令 #
```bash
    ./configure --prefix=/usr/local/test
    卸载程序用make uninstall
```

# 查看存储空间 #
```bash
    df -h #将以人类可以阅读的容量格式显示各挂载点的存储空间使用情况
    du -h --max-depth=1 /path # 表示显示 path 路径下只深入到第一层子目录的各文件夹大小
    du -s directory  #查看某一文件夹的大小
    free -h #将以人类可以阅读的容量格式显示内存使用情况
    fdisk -l #查看硬盘及分区情况
```

linux中文件名若有空格的解决方法：在空格前加反斜杠\,例如文件名为“software package”，在Linux中可表示为“software\ package"

恢复成系统缺省的.bashrc: `cp /etc/skel/.bashrc ~`
