---
layout: post
title: shell的文本操作
categories: linux
tags: awk sed grep
author: renql
---

* content
{:toc}

在用shell脚本批处理文本文件时，可能需要读取或修改ascii文件中的一些信息。在shell中有许多可以处理文本文件的工具，配合正则表达式，可以实现很多功能。现罗列如下：  
- **grep** 适合单纯的查找或匹配文本，也常用于搜索文件  
- **sed** 主要用于编辑文本，但也可以用于搜索
- **awk** 适合对格式化文本进行搜索判断，可以对文本进行较复杂格式处理

上述命令的一些常见用法：
```bash  
# 统计文本文件中某单词出现次数  
cat tr_trs_pos.txt | grep -o "TRACK_ID" | wc -l  
# 竖杠表示管道命令，将前一命令的结果作为下一个命令的输入
# grep -o 表示搜索文本并只显示匹配的部分
# wc [-clw][文件…]可以统计文件（如果没有指定文件，则会从标准输入读取数据）
# 的字符数（-c），字数（-w），行数（-l），这里就是只统计行数

# 统计文件中每一个单词出现的次数，并按照出现频率从大到小排序
sed 's/ /\n/g' file.txt | sort | uniq -c | sort -nr
# 使用sed读取file.txt文件中的所有内容，并将空格替换为换行符，然后将修改后的内容向sort输入
# sed 在不使用 -i 参数时，是不会直接将文件里的内容修改，因此此时file.txt里的内容不会被修改
# sort可以将文本内容加以排序，-n表示按照数值大小排序，-r表示以相反的顺序排序
# uniq 检查并删除文本中重复出现的行列，-c或--count 在每列旁边显示该行重复出现的次数。
# 重复的行并不相邻时，uniq 命令不起作用，因此需要先 sort

sed -i "34s/.*/${fras}/" STATS.latlng_1hr.in
# 将文件中第34行的内容替换为变量fras存储的内容

awk '{if(NF==4 && ($2 > 400 || $3 > 100 )) print FILENAME, $0}' $filname | awk 'END{print NR}'

awk 'NR==4 {print FILENAME, $2}' file1.txt | tee -a file2.txt
```

