---
layout: post
title: linux远程数据拷贝
categories: linux
tags: scp rsync
author: renql
---

* content
{:toc}

# scp
scp 是 secure copy 的缩写, scp 是 linux 系统下基于 ssh 登陆进行安全的远程文件拷贝命令。  
scp 是加密的，rcp 是不加密的，scp 是 rcp 的加强版。  

该命令好像只能复制文件，若要复制目录及目录下的所有文件，需要加入 -r 表示递归复制整个目录

```bash
scp -r local_file remote_username@remote_ip:remote_folder # 将本地数据复制到远程
scp -r root@www.runoob.com:/home/root/others/music /home/space/music/1.mp3  # 从远程复制数据到本地
```

# rsync
remote sync（远程同步），但它不仅可以远程同步数据（类似于 scp 命令），还可以本地同步数据（类似于 cp 命令）。不同于 cp 或 scp 的一点是，使用 rsync 命令备份数据时，不会直接覆盖以前的数据（如果数据已经存在），而是先判断已经存在的数据和新数据的差异，只有数据不同时才会把不相同的部分覆盖。

使用**rsync 在远程传输数据（备份数据）前，是需要进行登陆认证的**，这个过程需要借助 ssh 协议或者 rsync 协议才能完成。在 rsync 命令中，如果使用单个冒号（:），则默认使用 ssh 协议；反之，如果使用两个冒号（::），则使用 rsync 协议。
ssh 协议和 rsync 协议的区别在于，rsync 协议在使用时需要额外配置，增加了工作量，但优势是更加安全；反之，ssh 协议使用方便，无需进行配置，但有泄漏服务器密码的风险。

```bash
rsync [OPTION] SRC DEST # 仅在本地备份数据
rsync [OPTION] SRC [USER@]HOST:DEST # 将本地数据备份到远程机器上
rsync [OPTION] [USER@]HOST:SRC DEST # 将远程机器上的数据备份到本地机器上

# SRC：用来表示要备份的目标数据所在的位置（路径）；
# DEST：用于表示将数据备份到什么位置；
# USER@：当做远程同步操作时，需指明系统登录的用户名，如果不显示指定，默认为以 root 身份登录系统并完成同步操作。

# 常用的 OPTION 选项 -avzP
# -a相当于-r、-l、-p、-o、-g、-t、-D，表示递归同步目录、保留软连接、保持文件权限、保持文件属主、属组、时间和设备信息
# -v 表示打印一些信息，比如文件列表、文件数量等。
# -z 将会在传输过程中压缩。
# -P 表示在同步的过程中可以看到同步的过程状态，比如统计要同步的文件数量、 同步的文件传输速度等。

# 若只同步DEST中没有但SRC有的文件，则加入 --ignore-existing
# 若只同步DEST中存在的文件，则加入 --existing
# 删除 DEST 中 SRC 没有的文件， 则加入 --delete

# 其他还有很多参数，可以在bash中直接输入 rsync 进行查看。
```

总体来说，感觉rsync功能比scp强大。
