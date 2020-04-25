---
layout: post
title: ncl常用数学函数
categories: ncl
tags: ncl 随机数 取整 统计 mask
author: renql
---

* content
{:toc}

整理ncl中的常用数学函数，如取整、平均、标准化  
在ncl中进行计算时，注意缺测和小数。例如 `a=1/12344` 得到的结果是整数0，但如果是 `a=1.0/123456` 得到的则是浮点数，结果不为0.




# 1 数学函数
```
a = b^2   ;平方表述
a = fspan(start, finish, number)   ;Creates an array of evenly-spaced floating point numbers
b = ispan(start, finish, spacing)  ;Creates an array of equally-spaced integer, long, or int64 values.

srand(seed)  ;Establishes a seed for the rand function. send is a positive integer value to use as the seed for rand.
c = rand() ;Returns a pseudo-random integral value in the range of 0 <= return_val <= 32766.只能生成一个数

random_setallseed(iseed1, iseed2) ;iseed1 and iseed2 are any integer between 1 and 2,147,483,562 (default is 1234567890).
;Sets initial seeds for random number generators.
c1 = random_normal(av, sd, (/10,100/)) ;Generates random numbers array using a normal distribution.
c2 = random_normal(av, sd, (/10,100/)) ;Generates random numbers array using a normal distribution.
```    
If the user does not explicitly set initial values for seeds via `random_setallseed`, those initial seeds will be set to default values. It is recommended that the user specify these seeds.    

1. 伪随机数并不是假随机数，这里的“伪”是有规律的意思，就是计算机产生的伪随机数既是随机的又是有规律的。   
2. 随机种子来自系统时钟，确切地说，是来自计算机主板上的定时/计数器在内存中的记数值。   
3. 随机数是由随机种子根据一定的计算方法计算出来的数值。所以，只要计算方法一定，随机种子一定，那么产生的随机数就不会变。也就是说，伪随机数也是某种对应映射的产物，只不过这个自变量是系统的时间而已  
4. 如果你每次调用srand()时都提供相同的种子值，那么，你将会得到相同的随机数序列   

# 2 统计函数
## 2.1 相关系数
`esccr(x,y,mxlag) or cova = esccv(x,y,mxlag)` 计算x和y最右边维的交叉时滞相关或协方差，0 <= mxlag <= N/4。如果要算超前滞后相关，需要进行两次运算，如下所示：  
```
mxlag    = 9
x_Lead_y = esccr(x,y,mxlag)
y_Lead_x = esccr(y,x,mxlag)    ; switch the order of the series

ccr = new ( 2*mxlag+1, float)    
ccr(0:mxlag-1) = y_Lead_x(1:mxlag:-1)  ; "negative lag", -1 reverses order
ccr(mxlag:)    = x_Lead_y(0:mxlag)     ; "positive lag"
```
`esacr(x,mxlag)` ，计算时滞自相关系数

`escorc(x,y)`，只能计算Pearson同时线性交叉相关

`run_cor(x,y,time,wSize)`,计算滑动相关。使用该函数需要调用一个脚本：  
```
load "$NCARG_ROOT/lib/ncarg/nclscripts/contrib/run_cor.ncl"
```
<a href="https://renqlsysu.github.io/2018/01/31/ncl-significance-test-EOF/#1%E6%A3%80%E9%AA%8C%E7%9B%B8%E5%85%B3%E7%B3%BB%E6%95%B0%E6%98%AF%E5%90%A6%E6%98%BE%E8%91%97" target="_blank">相关系数的检验</a>

![](https://s1.ax1x.com/2020/04/13/Gvm1nU.jpg)

<a href="https://wenku.baidu.com/view/fdfece05a6c30c2259019eed.html" target="_blank">更详细版相关系数检验临界值表</a>

## 2.2 回归系数
利用 ` regCoef_n ( ts, vars, dim_ts, dim_vars ) ` 函数计算线性回归系数（利用最小二乘法），允许缺测，会将 t 统计量作为属性输出，此时若要对回归系数做显著性检验，就需要根据t统计量计算 a two-tailed probability (prob)，<a href="https://renqlsysu.github.io/2018/01/31/ncl-significance-test-EOF/#0students-t-distribution" target="_blank">关于该检验的具体介绍 </a>。   

该函数会以属性形式返回四个参数：截距 **yintercept**, 用于显著性检验的t统计量 **tval**, 估计回归系数的标准误差 **rstd**， 样本数 **nptxy** 

如果时间序列 ts 的单位为 K， 回归场 vars 的单位为 m，那么回归系数的单位是 m/k。该函数在计算回归系数前不会讲时间序列标准化，如果需要标准化，则需要作者自己处理。

```
; 数据维数介绍：ts(6,neval,nyear), vars(nyear,nlat,nlon), var(6,neval,nlat,nlon)
var := regCoef_n(ts, vars, 2, 0) ;关于时间维做回归
copy_VarCoords(vars(0,:,:), var(0,0,:,:))
printVarSummary(var)

; 回归系数的显著性检验
tval  := onedtond(var@tval ,(/6,neval,nlat,nlon/)) ;t统计量
df    := onedtond(var@nptxy,(/6,neval,nlat,nlon/)) ;样本数
b = tval
b = 0.5
prob  := betainc( df/(df+tval^2), df/2.0, b )
prob  := mask(prob,prob.lt.siglvl,True)
copy_VarCoords(vars(0,:,:), prob(0,0,:,:))
```

## 2.3 方差与标准化
```
;序列标准化
avar = dim_standardize_n(var,opt,dim) ;得到标准化序列，忽略缺测
;opt = 1 用the population standard deviation（除以不包含缺测的样本总数）计算
;opt = 0 用the sample standard deviation（除以不包含缺测的样本总数-1）计算

;计算标准差方差
stdd = dim_stddev_n(var,dim)   ;计算样本标准差，即除以不包含缺测的样本总数-1
vari = dim_variance_n(var,dim) ;计算无偏差估计的方差 the unbiased estimates of the variance，即除以不包含缺测的样本总数-1
```

# 3 取整函数
```
floor(values)  ;Returns the largest integral value less than or equal to each input value.
;values 可以是一个数或一个数组，此外，若输入的是double，则输出的也是double
；若要得到整数，需用  toint(floor(values))

ceil(values)   ;Returns the smallest integral value greater than or equal to each input value.
;values 可以是一个数或一个数组，此外，若输入的是double，则输出的也是double

;上述函数可以用来设置纵坐标的取值范围
  res@trYMinF = toint(floor(min(var)))
  res@trYMaxF = toint( ceil(max(var)))
  
round(values,opt)  ;Rounds a float or double variable to the nearest whole number.类似于四舍五入
;valus可以是任意纬度
;opt=0: return values of the same type as x
;opt=1: return values of type float
;opt=2: return values of type double
;opt=3: return values of type integer

```

# 4 标记函数
```
  x = mask(y, y.lt.100,False)   ;会得到一个和y数组一样大小的x数组，x中相应位置上的y数值若小于100会被设为缺测值，若大于100则是y中该数字。
  x = mask(y, y.lt.100,True )   ;与上例相同，只是此时是数值大于100的被设为缺测值。
```
`mask` 函数最后一个逻辑值为False，表示保留逻辑运算为False的数字。True则为保留逻辑运算为True的数字

