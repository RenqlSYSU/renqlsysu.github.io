---
layout: post
title: ncl维度与垂直坐标
categories: ncl
tags: 数组 垂直坐标
author: renql
---

* content
{:toc}

# 数组维度命名、取用
```
var(0:12:3, {lats:latn}, ::-1)     ;大括号内是变量的坐标值,将最后一维倒序    
var({lat|:}, {lon|:}, {time|:})    ;用维度名调换维度顺序，注意此时必须每一个维度都有名字，否则报错  
var(lat|:, lon|:, time|:)          ;同上  
var(lat|2:5:2, lon|:, time|:)      ;调用某一维度中某几个量
var((/0,3,5/),:,:)                 ;取用某几个坐标的值   

var@units  = "mm/day"    ;获取/创建变量属性   
var!0  = "time"          ;获取/创建维度名   
var&time = ispam(1,12,1) ;获取/创建坐标变量
```
nc文件中数据存储纬度是 **（时间，高度，纬度，经度）**   




# 改变数组的维数
```
dpC = conform (x, dp, (/0,1/))
;表示将二维数组dp(time,lev)扩展成和x(time,lev,lat,lon)一样维数的数组dpC，最后一个参数表示dp与x中的哪几维相同。
;注意dp的维数必须小于x，即dp必须是x的子集
;若dp是一个数，此时最后一维可以写-1

x = (/1,2,3,4,5/)
xc1 = conform_dims((/3,5/),x,1)
xc2 = conform_dims((/5,3/),x,0)
;该函数用法同conform，只是把第一参数改为维数而不是一个数组

nyears = ntim/12
x4d  = reshape(x,(/nyears,12,nlat,nlon/))
xjfm = reshape(x4d(:,0:2,:,:),(/nyears*3,nlat,nlon/))
;reshape可以把一个多维数组转变成另一个多维数组
;在该例子中，x(ntim，nlat，nlon)的多维数组，该例子提取出了每年1-3月的数据并组成一个序列

nyears = ntim/12
x1d     = ndtooned(x) ;将多维数组转换成一维数组，这里x依然是(ntim，nlat，nlon)的多维数组
x4d     = onedtond(x1d,(/nyears,12,nlat,nlon/)) ；将一维数组转换成多维数组
;将ndtooned和onedtond配合使用的效果同reshape
```
多用于ncl加减乘除时。

# 垂直坐标
模式的垂直坐标——atmosphere_hybrid_sigma_pressure_coordinate，假设垂直分层30层，则有：

- **lev（30）**：hybrid level at midpoints (1000*(A+B))，每一层的中间点
- **hyam（30）**：hybrid A coefficient at layer midpoints
- **hybm（30）**：hybrid B coefficient at layer midpoints

- **ilev（31）**：hybrid level at interfaces (1000*(A+B))，每一层的上下界面，故有31层
- **hyai（31）**：hybrid A coefficient at layer interfaces
- **hybi（31）**：hybrid B coefficient at layer interfaces

## Interpolates hybrid coordinates to pressure coordinates
```
new_var = vinth2p(var, hbcofa, hbcofb, plev, ps, intyp, p0, 1, extrp) ;1没有特殊用途
;var的最右边三维必须是（level，lat，lon）,level必须从上到下
;hbcofa, hbcofb是混合坐标系的一维系数，一般对应的是hyam，hybm，即hybrid A，B coefficient at layer midpoints，必须从上到下
;plev,需要转换为的一维气压坐标，单位为mb（或hPa），可以从下到上，也可从上到下
;ps,地面气压，单位Pa，与var有相同的维度，CESM输出的PS的单位正好为Pa
;intyp,代表插值方法，1=linear，2=log，3=loglog，一般取为2
;p0，参考地面气压，单位mb，一般为1000mb
;extrp为False时，当plev超出ps时不采用外推插值。为True时，则会将地表以下的数值也插值。

new_var = vinth2p_ecmwf(var, hbcofa, hbcofb, plev, ps, intyp, p0, 1, extrp, varflg, tbot, phis) 
;当extrp=False时，该函数同vinth2p，都是将CESM模式的混合坐标插值到气压坐标上。
;当extrp=True时，会利用ECMWF的公式来插值地表以下温度和气压，而其他变量则同模式最底层的值。
;比vinth2p多了三个参数varflg, tbot, phis，用来设置插值地表以下数值时需要用到的变量
;varflg, 1 表明插值的变量是温度, -1是位势高度, 0 表示插值的是其他变量。
;tbot维数同地表气压ps，表示最底层的温度 T(:,0,:,:)。只有当 varflg=-1时才会用到该变量，但任何情况下都要提供该变量
;phis，地表位势高度（m^2/sec^2）最右边两维同地表气压ps
```
但之前在用这个函数时，好像并没有特别注意方向问题，var，hyam，hybm都是读出来就直接用于计算了，并没有检查其方向，plev也是从下到上。  
目前没有出现过问题说明这个应该没有问题。  

注意地面气压PS模式输出单位为Pa，且PS会随时间变化，而hyam，hybm，p0等参数不随时间变化

## 垂直气压坐标差分
```
  dp   = dpres_hybrid_ccm (ps,p0,hyai,hybi)  
  ;Calculates the pressure differences of a hybrid coordinate system Pa [kg/(m s2)]   
  ;the return array will have an additional level dimension compare to PS  
  ;The size of the level dimension is one less then the size of hyai
  ;ps and p0 should have the same unit, Pa or hPa
  
  lev = (/  1,  2,  3,  5,   7, 10, 20, 30, \
           50, 70,100,150, 200,250,300,400, \
          500,600,700,775, 850,925,1000 /)
   psfc= f-PS   ; PA    (time,lat,lon)
   lev = lev*100
   lev@units = "Pa"    ; to match PS
   ptop= 0             ; integrate 0==&gt;psfc at each grid point
   dp  = dpres_plevel_Wrap(lev, psfc, ptop, 0)  ;dp(time,lev,lat,lon)
;Calculates the pressure layer thicknesses of a constant pressure level coordinate system
;lev, psfc 及 ptop 的单位必须一致
```
计算各层气压厚度主要用于垂直积分。

## 几类ncl的垂直积分函数
ncl垂直积分的几种函数：
1. <a href="https://www.ncl.ucar.edu/Document/Functions/Built-in/wgt_vert_avg_beta.shtml" target="_blank">wgt_vert_avg_beta (plev,data,psfc,punits,opt)</a>，利用气压厚度及beta因子计算data（3维或4维）的垂直积分（opt=0）或垂直平均（opt=1），若opt=（/0，650，900/）表示计算650hPa到900hPa之间的垂直积分。但**若data底层数据有缺测，会导致整层积分的结果也缺测**。  
2. <a href="https://www.ncl.ucar.edu/Document/Functions/Contributed/wgt_vertical_n.shtml" target="_blank">wgt_vertical_n (data,dp,iopt,dim)</a>，可以计算垂直积分（iopt=1）或垂直平均（iopt=0），方法同方案4，此处data维数不限，**但不能有缺测**。  
3. <a href="https://www.ncl.ucar.edu/Document/Functions/Built-in/vibeta.shtml" target="_blank">vibeta (plev,data,linlog,psfc,pbot,ptop)</a>, 利用beta因子计算data的在ptop到pbot或psfc之间的垂直积分。根据官网的例子，该函数的计算结果同方案4。  
4. 先利用 `dpres_hybrid_ccm (psfc,p0,hyai,hybi)` 或`dpres_plevel_Wrap(plev, psfc, ptop, 0)` 计算各层气压厚度，在利用`intEKE = dim_sum_n(EKE*dp,dim_lev)`计算垂直积分，`EKE = dim_sum_n(EKE*dp,dim_lev)/dim_sum_n(dp,dim_lev)`计算垂直平均。目前来看，这一种是最常用的。

# 返回特定的坐标位置 indices
```
select_time = ind( time(:,1).ge.6 ) ;ind只能用于一维数组，可以返回一个值或一维数组
```

若要对多维数组进行逻辑运算并返回位置坐标，则使用ind_resolve
```
a1D      = ndtooned(a) ;将多维数组转化为一维数组，与其功能相反的函数是 onedtond(a1D, dsizes_a)
dsizes_a = dimsizes(a)
indices  = ind_resolve( ind(a1D.gt.5), dsizes_a )
;返回的indices是一个二维数组N*M，N代表满足逻辑运算的个数，M代表a的总维数

print(indices(0,:)) ;则会返回第一个满足逻辑关系的数的坐标位置(0,1,1)

返回结果如下所示：
Variable: indices
Type: integer
Total Size: 108 bytes
            27 values
Number of Dimensions: 2
Dimensions and sizes:   [1] x [3]
Coordinates: 
Number Of Attributes: 1
  _FillValue :  -999
(0,0)   0
(0,1)   1
(0,2)   1
```

对一维数组挑出特定值的坐标
```
year      = ispan(1870,2006,1)
year_want = (/1870,1900, 1948, 1957, 1964, 1965, 1989, 2005, 2006/)
i         = get1Dindex(year, year_want) ;i的个数与year_want的个数相同
```
