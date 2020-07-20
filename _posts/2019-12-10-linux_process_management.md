---
layout: post
title: Linux进程管理与后台运行
categories: linux
tags: linux
author: renql
---

* content
{:toc}

# 常用任务管理命令
```bash
jobs      //查看任务，返回任务编号n和进程号
bg  %n   //将编号为n的任务转后台运行
fg  %n   //将编号为n的任务转前台运行
ctrl+z    //挂起当前任务
ctrl+c    //结束当前任务

kill -9  进程号  #立即强制删除一个工作   
kill -15 %n  #以正常的程序方式终止一项工作
```

# 不受HUP影响的后台运行
在Linux中，如果要让进程在后台运行，一般情况下，我们在命令后面加上&即可。
但这样是将命令放入到一个作业队列中了，但当网络断开或本地终端断开连接后，终端会发送hangup（HUP）信号来通知其关闭所有子进程，因此该任务也会终止。
为了使任务不受HUP（hangup）信号影响，<a href="https://www.ibm.com/developerworks/cn/linux/l-cn-nohup/index.html" target="_blank">该博文</a> 记录了好几种方法。
本人觉得最好用的是以下两种，记录如下。

## nohup
在正常命令前加入nohup，就可以让提交的命令忽略 hangup 信号。
```bash
nohup mpirun –np 8 ./wrf.exe

nohup command > myout.file 2>&1 &  
# 指定了输出信息的文件，缺省情况下该作业的所有输出都被重定向到一个名为nohup.out的文件中
```

用 `nohup` 后，可以用 ` jobs ` 来查看任务， 再次登录查看任务可以用 ` top ` 或者 ` ps –a `      
` ps -ef `  可以查看主机所有运行的进程   ` ps -ef | grep ` 过滤条件   
但是，请注意，以上两个命令都只能查看单个节点的运行情况。对于并行运行、集群系统、天河等电脑，则无法使用上述命令来查看任务提交情况，而应该使用 `qstat`（四期）,`yhq`(tianhe)

## screen
通过screen来创建新的虚拟终端，在该终端中运行作业。
关于screen的进一步了解可以参考这篇博文 。<a href="https://www.ibm.com/developerworks/cn/linux/l-cn-screen/" target="_blank">https://www.ibm.com/developerworks/cn/linux/l-cn-screen/</a>

```bash
# 最好给每个会话命名，便于区分
screen -dmS session_name # 建立一个一开始便处于断开模式下的会话（-S 表示创建screen会话时为会话指定一个名字）
screen -r session_name # 重新连接指定会话
screen -d session_name # 断开其他正在运行的screen会话
screen -S session_name -X quit # 删除一个会话

screen -list # 列出所有会话名、状态
screen -wipe # 会清除会话状态为 dead 的会话

# 进入会话后，可用快捷键CTRL-a d 来暂时断开当前会话，此时对话里的任务不会终端
# 进入会话后，若选择输入 exit 来退出当前会话，则该会话就会被删除

screen -h num	 # 可以指定历史回滚缓冲区大小为num行
```
