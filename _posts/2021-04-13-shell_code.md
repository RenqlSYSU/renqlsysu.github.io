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

在 Bash shell 中，每一个变量的值都是字符串，无论你给变量赋值时有没有使用引号，值都会以字符串的形式存储。 这意味着，Bash shell 在默认情况下不会区分变量类型，即使你将整数和小数赋值给变量，它们也会被视为字符串，这一点和大部分的编程语言不同。

以**单引号' '包围变量的值时，单引号里面是什么就输出什么**，即使内容中有变量和命令（命令需要反引起来）也会把它们原样输出。

以**双引号" "包围变量的值时，输出时会先解析里面的变量和命令**。这种方式比较适合字符串中附带有变量和命令并且想将其解析后再输出的变量定义。

shell数组：  
```shell
a=(3 6 9 10)
echo ${a[0]}
echo ${a[*]} #print all variable
```

Shell 和其它编程语言不同，Shell 不能直接进行算数运算，必须使用数学计算命令  
```shell
b=$((a[0]+1)) # Assign the result of the calc to b, 4
c=$((b+1))    # 5
# (()) only can be used for integer calc
# do not need to use $ in parentheses
```

若有命名字符变量数组时，    
```bash
#!/bin/sh
CASENAME[1]=F2000
CASENAME[2]=CAM5

for ni in {1..1}
do
	echo "${CASENAME[ni]}"
	if [ $ni == 1 ] ; then  
	# 注意括号及双等号两边都需要有空格，否则运行失败
		 echo "----------"
	fi
done
```

字符串拼接 http://c.biancheng.net/view/1114.html

字符串分割 https://blog.csdn.net/u010003835/article/details/80750003  
https://blog.csdn.net/dehailiu/article/details/10479527?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&dist_request_id=1328665.18784.16160313276179911&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control

路径分割得到路径和文件名 https://blog.csdn.net/Choice_JJ/article/details/8766335

## 交互式运行程序
想要在bash脚本中实现交互式运行命令，主要借助输入重定向操作符 << 来实现，举例如下
```bash
for nl in {0..2};do
	utils/bin/box << EOF
n
y
EOF
	mv output.file output.nc
done
# 此处 n 和 y 是传递给 utils/bin/box 的两个参数
```
Shell中通常将EOF与 << 结合使用，表示后续的输入作为子命令或子Shell的输入，直到遇到EOF为止，再返回到主调Shell。

此处，EOF是一个分界符，在该分界符以后的内容都被当作输入（包括空格），直到shell又看到该分界符(位于单独一行的开头)。这个分界符可以是你所定义的任何字符串。
