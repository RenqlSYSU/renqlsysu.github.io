---
layout: post
title: python的主要结构
categories: python
tags: python
author: renql
---

* content
{:toc}

# python数据结构
Python有五个标准的数据类型：Numbers（数字），String（字符串），List（列表），Tuple（元组），Dictionary（字典）
```py
# 列表是写在方括号 [] 之间、用逗号分隔开的元素列表
list = [ 'abcd', 786 , 2.23, [1,2,3]]
tinylist = [123, 'runoob']
list2 = [i for i in range(30) if i % 3 == 0]
# 得到列表 [0, 3, 6, 9, 12, 15, 18, 21, 24, 27]

names = ['Bob','Tom','alice','Jerry','Wendy','Smith']
new_names = [name.upper()for name in names if len(name)>3]
# 得到列表 ['ALICE', 'JERRY', 'WENDY', 'SMITH']

print (len(list))       # 列表元素个数
print (list[3][0])      # 嵌套列表索引
print (list[1:3])       # 从第二个开始输出到第三个元素
print (list[2:])        # 输出从第三个元素开始的所有元素
print (list[-1::-1])    # 翻转列表
print (tinylist * 2)    # 输出两次列表
print (list + tinylist) # 连接列表
```

元组与列表类似，但元组的元素不能修改。  
元组写在小括号 () 里，元素之间用逗号隔开  
元组的索引及切片方式同list  

```py
# 字典用 {} 标识，它是一个无序的 键(key) : 值(value) 的集合
# 同一个字典中，键(key)必须是唯一且不可变的，因此数字，字符串或元组都可作为键，但列表不行。
dict1 = {}
dict1['one'] = "1 - 菜鸟教程"
dict1[2]     = "2 - 菜鸟工具"

tinydict = {'name': 'runoob','code':1, 'site': 'www.runoob.com'}

dict2 = {x: x**2 for x in (2, 4, 6)} 
# 得到的字典为{2: 4, 4: 16, 6: 36}

print (len(dict2))        # 计算字典元素个数，即键的总数。
print (dict['one'])       # 输出键为 'one' 的值
print (tinydict.keys())   # 输出所有键
print (tinydict.values()) # 输出所有值
del tinydict['Name'] # 删除键 'Name'
tinydict.clear()     # 清空字典
```

# python输入输出  
python列表和元组顺序也是从0开始的

```python
a=input("please input password")
print("password you input is ",password)
print(type(a)) # input variable is usually str

b=int(a)
print(type(b))  

a=2
b='casename'
print('%s month is %03d'%(b,a))
# 格式化输出结果：casename month is 002
```

# python运算
python中除号用/表示，但是和C语言不同的是/得到的值总是浮点数，例如：5 / 5结果是1.0。
python中整除用//表示是，//表示两数相除，向下取整，例如8 // 5 结果是1,，至于数据类型是整数还是浮点数则取决于用到的数据类型。

# python的条件判断语句 
不管是条件语句还是循环，命令最后都有冒号。
```py
if a == 0 and b != 14:
	b = b+a
elif not a <= -1:
	b = b-a
else:
	b = b*a
```

# 几种python的循环语句  
```py
for i in range(-1,-10,-4):  
	print("Number of cycles: %d"%i)  
# 输出结果：
# Number of cycles: -1
# Number of cycles: -5
# Number of cycles: -9

name = 'chengdu'  
for i in name:
	print(i,end='\t') 
# '\t'是转义字符，表示水平制表符，即 Tab 键，一般相当于四个空格
# 输出结果：c	h	 e	n	 g	d	 u

b = [np.arange(d-lagh,d+lagh+1) for d in range(2,10,3)]
# 列表生成式

coins = ["Bitcoin", "Ethereum", "Cardano"]
prices = [48000,2585,2]
for coin, price in zip(coins, prices):
    print(f"${price} for 1 {coin}")

for i, coin in enumerate(coins):
    price = prices[i]
    print(f"${price} for 1 {coin}")

i = 0
while i < 5 :
	print('cycle time now : %d, i = %d'%(i+1,i))
	i += 1
else : 
	print('cycle end, now i = %d'%i)
```

break语句跳出 for 和 while 的循环体  
continue 跳过当前循环，直接进行下一轮循环  
pass 是空语句，一般用作占位语句，不做任何事情  

# python 自定义函数
除了正常定义的**位置参数**（也就是必选参数）外，还可以使用**默认参数**、**可变参数**（传入的参数个数可变）和**关键字参数**，使得函数定义出来的接口，不但能处理复杂的参数，还可以简化调用者的代码。

https://www.liaoxuefeng.com/wiki/1016959663602400/1017261630425888

# python读取nc文件
```python   
import netCDF4 as nc   
f=nc.Dataset("/home/users/qd201969/ERA5-1HR/stat_apr-sep1979-2019.nc") # best to use absolute path  
f.variables.keys() # get the list of the variables   

a=f.variables['mstr'] # get the data and vari info  
a=f.variables['mstr'][:] # only get the data  
lat=f.variables['latitude'][:]  
lon=f.variables['longitude'][:]

indx=np.argwhere((lon<100) & (lon>10))
indy=np.argwhere((lat<50) & (lat>10))   
``` 

从xarray走向netCDF处理: https://www.jianshu.com/p/86f02bc58265   
```py  
import xarray as xr
f = xr.open_dataset('EC-Interim_monthly_2018.nc') 

a=f['mstr'] # get the data and vari info
a=f.mstr    # two method to read the variable

b=a.loc[84.86:90,352.5:360] # use lat and lon read data
c=b.mean(dim=['lon','lat'])  
```  

