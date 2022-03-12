---
layout: post
title: python的主要结构
categories: python
tags: python
author: renql
---

* content
{:toc}


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

