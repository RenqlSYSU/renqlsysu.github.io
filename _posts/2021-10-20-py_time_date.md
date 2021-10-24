---
layout: post
title: python日期与时间的处理函数
categories: python
tags: time calendar
author: renql
---

* content
{:toc}

# time & calendar
关于时间的处理，和ncl很不一样的是，Python 提供了一个 time 和 calendar 模块可以用于格式化日期和时间，想处理成任何格式的日期都可以。

python中的日期有两种类型：  
- **时间戳 timestamp**：以自 1970 年 1 月 1 日午夜（历元）后经过的浮点秒数来表示。某些编程语言（如Java和JavaScript）的timestamp使用整数表示毫秒数，这种情况下只需要把timestamp除以1000就得到Python的浮点表示方法。使用timestamp的好处在于，其值与时区无关。timestamp一旦确定，其UTC（Universal Time Coordinated）时间就确定了，转换到任意时区的时间也是完全确定的，这就是为什么计算机存储的当前时间是以timestamp表示的，因为全球各地的计算机在任意时刻的timestamp都是完全相同的（假定时间已校准）.  
- **时间元组**：time.struct_time(tm_year=2016, tm_mon=4, tm_mday=7, tm_hour=10, tm_min=28, tm_sec=49, tm_wday=3, tm_yday=98, tm_isdst=0)，一共9组数字，分别表示年、月、日、小时（0\~23）、分钟、秒、一周第几日（0\~6，0是周一）、一年第几日（1~366）、是否为夏令时（1夏令时、0不是夏令时、-1未知，默认-1）

```python
import time

# 格式化成 2016-03-20 11:45:39 形式
print (time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()))
# time.localtime([secs])可获得当前时间的本地时间元组，也接受时间戳，并返回当地时间下的时间元组
# time.strftime(fmt[,tupletime])只接收时间元组，并返回以字符串表示的时间


# 将格式字符串转换为时间戳
a = "Sat Mar 28 22:24:24 2016"
print (time.mktime(time.strptime(a,"%a %b %d %H:%M:%S %Y")))
# time.strptime(str,fmt)根据fmt的格式把一个时间字符串解析为时间元组  
# time.mktime(tupletime) 接受时间元组并返回时间戳  


time.sleep(secs) # 推迟调用线程的运行，secs指秒数。
time.process_time() # 返回当前进程执行 CPU 的时间总和，不包含睡眠时间。由于返回值的基准点是未定义的，所以，只有连续调用的结果之间的差才是有效的。


calendar.isleap(year) # 是闰年返回 True，否则为 false。
calendar.leapdays(y1,y2) # 返回在Y1，Y2两年之间的闰年总数。
```

# pandas的date_range  
pandas的 `pd.date_range(start*, end*, periods*, freq)`函数可以生成任意间隔的时间序列。带*的参数表示可选参数    
- freq参数由数字和英文(M月，D天，H小时，Min分钟...)组成。如20D表示间隔20天，5M表示间隔5个月  
- start和end日期字符串,可以是"20171011","2021-09-25","1/30/2018"
- periods生成数据的时间长度，因此可以通过只给定 start和periods生成时间序列。

举例如下：  
```python
import pandas as pd

ftime  = pd.date_range(start='2021-09-25 00',end='2021-09-25 12', freq='1H' \
      ,closed=None).strftime("%Y-%m-%d_%H:00").to_list() 
'''
若没有后面转换格式的命令.strftime("%Y-%m-%d_%H:00").to_list()，得到的结果如下：
DatetimeIndex(['2021-09-25 00:00:00', '2021-09-25 01:00:00',
               '2021-09-25 02:00:00', '2021-09-25 03:00:00',
               '2021-09-25 04:00:00', '2021-09-25 05:00:00',
               '2021-09-25 06:00:00', '2021-09-25 07:00:00',
               '2021-09-25 08:00:00', '2021-09-25 09:00:00',
               '2021-09-25 10:00:00', '2021-09-25 11:00:00',
               '2021-09-25 12:00:00'],
              dtype='datetime64[ns]', freq='H')
'''
```
# datetime
datetime是Python处理日期和时间的另一个标准库，pd.date_range(start*, end*, periods*, freq)生成的时间就是这个格式的。 字符串与datetime之间的相互转换和time模块类似

```python
from datetime import datetime, timedelta, timezone


now = datetime.now() # 获取当前datetime
print(now.strftime('%a, %b %d %H:%M')) 
# 将datetime以自定义格式转换为字符串打印


dt = datetime.strptime('2015/6/1 18:19:59', '%Y/%m/%d %H:%M:%S') 
# 把str转换为datetime，只能一个时间一个时间地转换


dt = datetime(2015, 4, 19, 12, 20) # 用指定日期时间创建datetime
# print得到的结果会是 2015-04-19 12:20:00
print(dt.year) 
# 也可以单独查看 month, day, hour, minute, second, microsecond, tzinfo


# 但无法通过dt.hour=13修改datetime的时间，只能通过timedelta对日期时间进行加减，得到新的时间
now = datetime.now() # 获取当前datetime
a1 = now + timedelta(hours=10) #时间向后推移10个小时
a2 = now - timedelta(days=1)   #日期向前推移1天


dt.timestamp() # 把datetime转换为timestamp
dt = datetime.fromtimestamp(time.time()) # 把时间戳转为本地时区的datetime
dt = datetime.utcfromtimestamp(time.time()) # 把时间戳转为UTC的datetime
```

# 对于nc文件的时间轴
以ERA5为例，其时间坐标是以自1900年1月1日午夜零时以来的小时数表示，和python的时间戳不一样。  
```
        int time(time) ;
                time:units = "hours since 1900-01-01 00:00:00.0" ;
                time:long_name = "time" ;
                time:calendar = "gregorian" ;
```

当用xarray.open_dataset打开nc文件读取时间维，好像是会自动将该时间坐标转为datetime.  
但若是用netCDF库的Dataset打开nc文件，则需要使用num2date将时间坐标转为python时间戳（根据ECMWF给出的python例子),如下所示：

```python
from netCDF4 import Dataset, date2num, num2date

with Dataset(f_in) as ds:
    var_time = ds.variables['time']
    time_avail = num2date(var_time[:], var_time.units,
            calendar = var_time.calendar)


import xarray as xr
ds = xr.open_dataset("ERA5_NH_t_1989.nc")
t = ds['time']

'''
print(t)的结果:
<xarray.DataArray 'time' (time: 1460)>
array(['1989-01-01T00:00:00.000000000', '1989-01-01T06:00:00.000000000',
       '1989-01-01T12:00:00.000000000', ..., '1989-12-31T06:00:00.000000000',
       '1989-12-31T12:00:00.000000000', '1989-12-31T18:00:00.000000000'],
      dtype='datetime64[ns]')
Coordinates:
  * time     (time) datetime64[ns] 1989-01-01 ... 1989-12-31T18:00:00
Attributes:
    long_name:  time
'''

from datetime import datetime
strt=["1989120206","1989120312"]
tim=[]
for str1 in strt:
    tim.append(datetime.strptime(str1, '%Y%m%d%H'))
    
var = ds['t'].sel(level=250,time=tim)
```


# 参考资料：  
- https://www.runoob.com/python3/python3-date-time.html  
- https://pandas.pydata.org/docs/reference/api/pandas.date_range.html  
- https://blog.csdn.net/qq_36387683/article/details/84766610
- https://www.liaoxuefeng.com/wiki/1016959663602400/1017648783851616
