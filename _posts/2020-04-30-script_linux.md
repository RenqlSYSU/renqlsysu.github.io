---
layout: post
title: Linux记录程序交互过程
categories: linux
tags: linux
author: renql
---

* content
{:toc}

平时安装或调试一个软件时，总会需要记录程序输出信息或交互过程以便后期查看学习。

```bash
# 重定向
ls ./ > ./file1   #将ls程序的标准输出写到file1文件中
ls ./ 2> ./file1  #将ls程序的错误输出写到file1文件中
ls ./ &> ./file1  #将ls程序的标准输出和错误输出都写到file1文件中
ls ./ 1> ./file1 2> ./file2 #将ls程序的标准输出写到file1文件中，将错误输出写到file2文件中

#单箭头>，表示以覆盖的方式输出到文件中
#双箭头>>，表示以追加的方式输出到文件中，不会覆盖之前的内容
```

然而常用的重定向功能只能记录程序的标准输出或错误输出，不能记录用户与程序的交互过程，此时发现一个比较好用的命令 `script output_file.txt ` 。加入参数`-a`会把会话记录附加到output_file.txt文件后面，保留先前的内容。

该命令会启动一个子shell，并将用户键入的所有内容、运行的任何程序的所有输出以及这些程序产生的任何错误保存到一个输出文件中。最后通过键入`exit`命令退出 script 模式并关闭输出文件。  

script 命令产生的文件通常包含控制字符，即退格、回车、用于显示某些提示的特殊字符以及您编辑前一个 shell 命令时使用的字符等等。可以使用文本编辑器清理script输出文件，网上有各种清理脚本可用。

参考：https://www.ibm.com/developerworks/cn/aix/library/au-screenshots1/index.html
