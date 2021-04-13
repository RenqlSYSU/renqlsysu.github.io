---
layout: post
title: shell脚本编程
categories: linux
tags: shell
author: renql
---

* content
{:toc}

Shell 如何定义变量和给变量赋值 https://www.jianshu.com/p/7fd317a45be5   
重点是赋值时，等号左右不能有任何空格。将命令的执行结果赋值给变量时，需要在命令两边加 '' 或者 $()

若有命名字符变量数组时，    
```bash
#!/bin/sh
CASENAME[1]=F2000
CASENAME[2]=CAM5

for ni in {1..1}
do
	echo "${CASENAME[ni]}"
	if [ $ni == 1 ] ; then
		 echo "----------"
	fi
done
```

字符串拼接 http://c.biancheng.net/view/1114.html

字符串分割 https://blog.csdn.net/u010003835/article/details/80750003  
https://blog.csdn.net/dehailiu/article/details/10479527?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&dist_request_id=1328665.18784.16160313276179911&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control

路径分割得到路径和文件名 https://blog.csdn.net/Choice_JJ/article/details/8766335
