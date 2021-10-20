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
- **时间戳**：以自 1970 年 1 月 1 日午夜（历元）后经过的浮点秒数来表示  
- **时间元组**：time.struct_time(tm_year=2016, tm_mon=4, tm_mday=7, tm_hour=10, tm_min=28, tm_sec=49, tm_wday=3, tm_yday=98, tm_isdst=0)，一共9组数字，分别表示年、月、日、小时（0~23）、分钟、秒、一周第几日（0~6，0是周一）、一年第几日（1~366）、是否为夏令时（1夏令时、0不是夏令时、-1未知，默认-1）

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

# 参考资料：  
- https://www.runoob.com/python3/python3-date-time.html  
- https://pandas.pydata.org/docs/reference/api/pandas.date_range.html  
- https://blog.csdn.net/qq_36387683/article/details/84766610
