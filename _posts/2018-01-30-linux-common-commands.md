---
layout: post
title:  "20180130 linux常用命令整理"
categories: linux
tags: vim 文件操作 进程管理 grep
author: renql
---

* content
{:toc}

![](http://wx1.sinaimg.cn/large/006fa9Xlgy1fwuse5urh5j30mo0w0jst.jpg)


# 关于文档与目录的命令 #
	
	ls -alh # 可以将所有文件（包括隐藏文件）容量以GB,KB等列出来

    ls -al | grep "^l" #通过管道命令和正则表达式，可以只显示链接文件，^l表示以l开头，l$表示以l结尾




# 链接文件 #
    cp -l source destination # 创建硬连接，用ls -al查看时，无箭头指向源文件，当源文件被删除时，该链接仍然有效

    cp -s source destination # 创建软连接，这是最常用的，当源文件被删除时，该链接失效

    ln source destination    # 创建硬连接，写目标目录时，注意写成 `./data` 而不是 `/data`，因为直接 `/` 意味着根目录  

    ln -s source destination # 创建软连接  
    
    rm destination  #删除软连接目录时，目录名后不能有/，否则将删除原目录下的文档
    

# vim中的常用命令 #
    ：n1,n2s/word1/word2/gc # 在n1到n2行之间，用word2替换word1

# 删除文件或文件夹的命令 #
    rm -fir filename # f 可以删除不存在的文件且不会出现警告信息；i 在删除前会询问用户； r 可以递归删除，最常用在目录的删除
    
    rmdir filename #只能删除一个空的目录，加上-p，会连同上层空的目录也删除

# 关于进程管理与后台运行 #
1. 在Linux中，如果要让进程在后台运行，一般情况下，我们在命令后面加上&即可，实际上，这样是将命令放入到一个作业队列中了，但当远程客户端关机后该任务就会终止。使用nohup则不会如此。
```bash
nohup mpirun –np 8 ./wrf.exe
```
用`nohup`后，再次登录查看任务可以用` top `或者` ps –a `    
` ps -ef `  可以查看主机所有运行的进程   ` ps -ef | grep ` 过滤条件   
但是，请注意，以上两个命令都只能查看单个节点的运行情况。对于并行运行、集群系统、天河等电脑，则无法使用上述命令来查看任务提交情况，而应该使用 `qstat`（四期）,`yhq`(tianhe)

如果使用nohup命令提交作业，那么在缺省情况下该作业的所有输出都被重定向到一个名为nohup.out的文件中，除非另外指定了输出文件
` nohup command > myout.file 2>&1 & `

2. 常用任务管理命令
```bash
jobs      //查看任务，返回任务编号n和进程号
bg  %n   //将编号为n的任务转后台运行
fg  %n   //将编号为n的任务转前台运行
ctrl+z    //挂起当前任务
ctrl+c    //结束当前任务
```
3. 终止后台运行的删除脚本：  
```
kill -9  进程号  #立即强制删除一个工作   
kill -15 %n  #以正常的程序方式终止一项工作
```

# 模式课上学的几个命令 #
```bash
tree -d    	  //可查看各目录下的文件分布情况
tail -f run.log   //可刷新查看输出结果
qstat -u usename  //可只看到我们提交的任务
grep -ir snow ./* //可搜索当前目录下包含“snow”的文件，-i忽略大小写，-r递归
```
