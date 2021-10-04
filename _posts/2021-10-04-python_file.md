---
layout: post
title: python文件操作
categories: python
tags: python
author: renql
---

* content
{:toc}

# 三种方法读取
```python
f = open("runoob.txt", "r")
print("文件名为: %s" %f.name)

# 第一种方法
# 从文件读取指定的字节数，如果未给定或为负则读取所有，包括换行符，并返回一个字符串
data = f.read(10)  

# 第二种方法
# 每次读出一行内容，所以，读取时占用内存小，比较适合大文件，该方法返回一个字符串对象。
# 括号内可以指定读取的字节数，包括换行符
f.readline()
while line: # 遍历文件所有行
    print (line.strip())
    print(type(line))
    line = f.readline()

# 第三种方法
# 读取整个文件所有行，保存在一个列表(list)变量中，每次读取一行，但读取大文件会比较占内存。
# 括号内无参数
lines = f.readlines()
for line in lines:
    print (line)
    print(type(line))

# 第四种方法
for line in f:
    print (line)
    print(type(line))

f.close() 
```
参考资料：  
1. https://www.runoob.com/python/file-methods.html
2. https://zhuanlan.zhihu.com/p/42784651

# 两种方法写入
```python
# 只能写入字符串，无法写入list、array，但可以把他们转换为字符串然后写入
ff = open("runoob.txt", "w")
ff.write("*"*50+"\n") # 写入50个*并换行
ff.writelines("lats"+str(lats)+"\nlons"+str(lons)) #同样需要自己加入换行符
```

写入文件时用到的两个主要模式，这两个模式不能同时出现：
- w，打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。
- a，打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。

# linecache模块
如果需要读取文件特定行的内容，可以使用该模块，对于大文件可以提高效率。但读取结束后，记得关闭该文件，否则，如果循环操作中该文件有更新，但linecache模块缓存的文件内容则不会有更新。
```python
import linecache

line = linecache.getline(‘a.txt’,4) # 读取第4行内容
print(line.strip()) # strip函数可移除字符串头尾指定的字符（默认为空格或换行符）或字符序列
linecache.clearcache()
```

# 其他一些实用文件操作
```python
f.seek(offset[, whence]) # 移动文件读取指针到指定位置
# offset，需要移动偏移的字节数
# whence，给offset参数一个定义，表示要从哪个位置开始偏移；0代表从文件开头开始算起，1代表从当前位置开始算起，2代表从文件末尾算起。可选，默认为0.

f.tell() # 括号内无参数，返回文件当前位置

import os
os.path.isfile(filname) # 判断文件是否存在
os.path.exists(test_file) # 判断文件或文件夹是否存在，但无法区分文件和文件夹
# 因此，若是判断文件，还是用 isfile 会比较好
```
