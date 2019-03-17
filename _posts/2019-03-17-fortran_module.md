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




## public 和 private
程序编写中最常使用的两种编写概念——结构化和面向对象。  
其中**面向对象**对程序编写的要求：  
- 为安全起见，有些数据不应该让外界使用。数据经过封装后，分为两种，一种是可以直接让大家使用的数据，另一种是只能在内部使用的数据。   
- 进过调用函数或子程序来重复使用程序代码  

module中可以通过 **public** 和 **private** 命令来区分公开使用及私下使用的变量、函数、子程序。  
没有特别经过 **public** 和 **private** 命令来赋值时，默认的状态是 **public**  
当module中只写了` private `且后面没有跟任何变量时，表明在这个module里，没有特别赋值的东西都不对外公开，若换成` public ` 也一样。

## use
在module中可以使用另一个module，可以同时使用多个module。  
若遇到两个module中的变量名称或函数名称重复的问题，可以利用 ` use module_name, aa=>va ` 临时把module中的变量名 **va** 改为 **aa** 来使用。  
利用 ` use module_name, only : vc ` 可以只是用module中的某些变量或函数。  

