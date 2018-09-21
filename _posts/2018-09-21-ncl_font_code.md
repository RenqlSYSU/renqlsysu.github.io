---
layout: post
title: ncl字体种类、上下标、大小的设置
categories: ncl
tags: ncl 字体 整理
author: renql
---

* content
{:toc}

找到一篇归纳ncl字体设置的一篇博文，供参考。
<a href="http://bbs.06climate.com/home.php?mod=space&uid=6970&do=blog&id=1773" target="_blank">NCL写字符串时的函数代码</a>
比较常用的会有

# 字体选择
NCL有0-22号、25-26号、29-30号、33-37号、121-137号字体，具体字号样式查询可以在以下网站查看  
http://www.ncl.ucar.edu/Document/Graphics/font_tables.shtml  
其中22号是我常用来加粗字体的字号

选用字号的方法：
1. 用`res@gsnStringFont = 22`
2. 若只取用其中的某些特殊字符，可以使用“~Fn~”选择字体，n表示字体号。如需表示位温θ，可以用“~F33~q”。  

常用字体有：希腊字符33号，数学符号34号，台风标记在35号里，天气现象符号36~37号。
其中需要转换到Roman font时，可以直接用“~R~”。
大于100号的字体多为空心字体。

# 上下标
以“~B~”开始下标、“~S~”开始上标，以“~N~”结束。

# 字的大小微调
第一类：用“~XnQ~”（字宽）、“~YnQ~”（字高）、“~ZnQ~”（整体），n表示调整后的大小是正常的n%。n省略或取0时，默认n=100，即为正常大小。
Q表示调整后的字符与前面输出的字符保持低端对齐。  
第二类：“~P~”：正常大小，“~I~”：索引字符的大小。

# xy图中横纵坐标标题方向的调整
```
res@tiYAxis  = True   ;显示纵坐标标题
res@tiYAxisFont  = 22 ;设定纵坐标标题字号
res@tiYAxisString  = "month" 
tiYAxisAngleF    = "90" ;纵坐标标题的方向，由水平方向逆时针旋转，默认为 90 即竖直放置，若为 0 则为水平
```
