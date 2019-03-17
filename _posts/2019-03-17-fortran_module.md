---
layout: post
title: Fortran中的模块
categories: Fortran
tags: module
author: renql
---

* content
{:toc}

Module 用来封装程序模块，通过` use module_name `来使用，且要在开始声明之前就使用。  

module中的变量若不声明成**全局变量**，这些变量被函数使用时，只会是函数中的局部变量。若想要函数之间通过module中的变量来传递数据，要把这些变量声明成**全局变量**，或者在声明变量时加上**SAVE**.
在声明中加入 **SAVE** 可以增加变量的生存周期，保留住所保存的数据，这些变量会在程序执行中永久记住上一次函数调用时所被设置的数值。

module中在 ` contains `后开始写作函数。  
同一个module中的函数可以直接使用同一个module中的所声明的变量，不需要再次声明。  
同一个module中的函数调用也在其中的函数时，不需要声明这个函数就可以直接使用。
