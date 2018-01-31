--
layout: post
title:  "20180130 linux常用命令整理"
categories: linux
tags: linux 命令整理
author: renql
---

* content
{:toc}

#关于文档与目录的命令#
	
	ls -alh # 可以将所有文件（包括隐藏文件）容量以GB,KB等列出来

    ls -al | grep "^l" #通过管道命令和正则表达式，可以只显示链接文件，^l表示以l开头，l$表示以l结尾






# 链接文件 #
    cp -l source destination # 创建硬连接，用ls -al查看时，无箭头指向源文件，当源文件被删除时，该链接仍然有效

    cp -s source destination # 创建软连接，这是最常用的，当源文件被删除时，该链接失效

    ln source destination    # 创建硬连接

    ln -s source destination # 创建软连接

# vim中的常用命令 #
    ：n1,n2s/word1/word2/gc # 在n1到n2行之间，用word2替换word1

# 删除文件或文件夹的命令 #
    rm -fir filename # f 可以删除不存在的文件且不会出现警告信息；i 在删除前会询问用户； r 可以递归删除，最常用在目录的删除
    
    rmdir filename #只能删除一个空的目录，加上-p，会连同上层空的目录也删除

