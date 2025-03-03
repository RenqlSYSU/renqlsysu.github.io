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

# 查看文本文件第一列的去重信息
awk '!seen[$1]++' hg38.all.cpgSite.bed  # 输出第一次遇到的第一列，而忽略后续的相同项
awk '{ print $1 }' hg38.all.cpgSite.bed | uniq # 去重，若后面加-c，则会显示每一个元素的重复次数， 但重复行不相邻时，该命令不起作用
awk '{ print $1 }' hg38.all.cpgSite.bed | sort -u # 对第一列去重并排序

# 将文本文件按第一列特定字符串及第二列排序
sort -k 1,1V -k 2,2n ${file} | awk '{ if($1=="chr1"||$1=="chr2"||$1=="chr3"||$1=="chr4"||$1=="chr5"||$1=="chr6"||$1=="chr7"||$1=="chr8"||$1=="chr9"||$1=="chr10"||$1=="chr11"||$1=="chr12"||$1=="chr13"||$1=="chr14"||$1=="chr15"||$1=="chr16"||$1=="chr17"||$1=="chr18"||$1=="chr19"||$1=="chr20"||$1=="chr21"||$1=="chr22"||$1=="chrX"||$1=="chrY") { print } }' > ${file}.sort
# -k 1,1V: 指定按照第一列进行排序，-k1,1 表示只考虑第一列，V 表示按照版本号进行排序（版本排序，例如，10会排在2的前面而不是后面）。
# -k 2,2n: 如果第一列相同，则按照第二列进行数值（numeric）排序，-k2,2 表示只考虑第二列，n 表示按照数值进行排序。
# 详细解释可以参照该网站 https://www.cnblogs.com/51linux/archive/2012/05/23/2515299.html 
```

