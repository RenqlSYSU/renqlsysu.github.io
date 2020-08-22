---
layout: post
title: 无法访问github.io的解决办法
categories: 杂学
tags: 博客
author: renql
---

* content
{:toc}

不知为何，最近几个月 github.io 一直打不开。根据网上的说法是域名解析的问题。

一般来说，访问网址时先搜索hosts文件，如果有网址对应的ip则不需要dns域名解析，因此可以将网址的ip配成静态ip，减少解析过程，提高访问速度。

修改过程如下：
1. 利用该网站 https://ipchaxun.com 查找网站对应的ip，如果搜不到，可以多刷新一下  
2. hosts文件（位置为C:\Windows\System32\drivers\etc）最下面增加（该文件的修改需要管理员权限，可以复制该文件到其他文件夹下修改，改完后再复制过来）：
```
185.199.108.153 xxxxx.github.io
185.199.109.153 xxxxx.github.io
```
3. 打开dos窗口，执行：ipconfig /flushdns，来刷新网络DNS缓存。

然后就可以访问了。但如果要访问别人的github.io，就需要再添加相应的ip地址。感觉还是不太方便，不知道什么时候可以正常访问任意的 github.io 呢？
