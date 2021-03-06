---
layout: post
title: 利用Fortran读写nc文件
categories: Fortran
tags: F90编译
author: renql
---

* content
{:toc}

发现用Fortran读写nc文件时的编译方法和一般的不一样，因为需要调用netcdf的静态库。

首先Fortran代码中要包含下面这一句话，需要加在 `implicit none` 后面：
```fortran
include '/usr/local/netcdf/include/netcdf.inc'
```

然后编译时分两步走
```bash
　　ifort -c -I/usr/local/netcdf/include test.f90
　　ifort -o test test.o -L/usr/local/netcdf/lib -lnetcdff
```
其中`-c`是编译，产生后缀为o的文件，`-o`是连接，产生可执行文件。如果需要编译的文件较多，也可以写 Makefile 文件进行编译。

若是没有调用netcdf库的话，在linux中直接对fortran编译的操作如下：
```fortran
ifort 1910-iterative_monthly.f90 -o iteration -mcmodel=medium
!可产生名为 iteration 的可执行文件。
!当该程序运行时运到的内存很大时，可在编译时加上最后那句话 -mcmodel=medium
```
