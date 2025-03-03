---
layout: post
title: Xshell的terminal修改
categories: linux
tags: Xshell
author: renql
---

* content
{:toc}

## Terminal Size
最近用Xshell远程linux服务器时，发现使用screen命令后会改变terminal窗口大小，令人感觉很不爽。之前使用putty时就没有遇到这种情况，于是上网搜解决方案，希望terminal窗口大小不会随screen的使用而改变。

<a href="https://blog.csdn.net/dreamer2020/article/details/101858976" target="_blank">linux禁止screen打开会话时改变窗口大小</a> 搜到了这个和我问题接近的答案，但依然无法解决我的问题。于是开始自己摸索。

通过如下菜单项进行配置
```
File -> Properties -> Terminal -> Advanced -> Miscellaneous -> 勾选 Disable terminal size change upon request
```

## Terminal Type
在探索过程中还发现Xshell可以修改 Terminal Type，可以有的选项：xterm Linux vt100 vt102 vt220 vt320 ansi scoansi

<a href="https://blog.csdn.net/taiyangdao/article/details/53166266" target="_blank">连接Linux服务器的终端仿真软件的termianl type详解</a>

不同的 termnial type 相当于不同的协议，主要控制 color ， tab ， keycode 这些的东西。 

其中最常用也是我目前在用的是Xterm，据说它是 X Window System 自带的 termnial ，支持最广。一般来说设置 terminal type 没什么卵用。毕竟我们不是从上古控制台时代过来的人。

如果选用linux的终端类型的话，使用vi，screen等命令查看后再关闭，所有信息都依然会保留在终端界面上，会使得终端界面上的内容很多，因此感觉不太好用。

## 复制粘贴快捷键设置
Xshell中复制粘贴文本时需要右键选择复制，再右键选择粘贴，有点麻烦。想到Putty可以**选中即复制，右键即粘贴**，不知道Xshell可不可以也设置成这样。上网一搜，发现有很多人都写了这个教程，例如这个 https://www.cnblogs.com/flyxuxi/p/11676083.html

但这些教程针对的Xshell大都都是中文版本的，键盘和鼠标的设置窗口很容易找到，但我的是英文版本，找了半天才找到。方法如下：

鼠标在Xshell空白界面处右键调出菜单栏，选“Options”，即出现有
“Keyboard and Mouse”的界面，然后选中以下地方，即可实现快速复制粘贴。

![](https://s3.ax1x.com/2021/03/18/6gdJaT.png)
