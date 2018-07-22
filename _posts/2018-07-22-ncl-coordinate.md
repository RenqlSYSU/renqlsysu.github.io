---
layout: post
title: ncl数组坐标命令
categories: ncl
tags: ncl 数据处理 整理
author: renql
---

* content
{:toc}

nc文件中数据存储纬度是 **（时间，高度，纬度，经度）**   
```
var(0:12:3, {lats:latn}, :)        ;大括号内是变量的坐标值    
var({lat|:}, {lon|:}, {time|:})    ;用维度名调换维度顺序，注意此时必须每一个维度都有名字，否则报错  
var(lat|:, lon|:, time|:)          ;同上  
var((/0,3,5/),:,:)                 ;取用某几个坐标的值   

var@units  = "mm/day"    ;获取/创建变量属性   
var!0  = "time"          ;获取/创建维度名   
var&time = ispam(1,12,1) ;获取/创建坐标变量
```
