---
layout: post
title: ncl维度与坐标
categories: ncl
tags: 数组 维度 坐标
author: renql
---

* content
{:toc}

# 数组维度命名、取用
nc文件中数据存储纬度是 **（时间，高度，纬度，经度）**   
```
var(0:12:3, {lats:latn}, :)        ;大括号内是变量的坐标值    
var({lat|:}, {lon|:}, {time|:})    ;用维度名调换维度顺序，注意此时必须每一个维度都有名字，否则报错  
var(lat|:, lon|:, time|:)          ;同上  
var((/0,3,5/),:,:)                 ;取用某几个坐标的值   

var@units  = "mm/day"    ;获取/创建变量属性   
var!0  = "time"          ;获取/创建维度名   
var&time = ispam(1,12,1) ;获取/创建坐标变量
```
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
;extrp为False时，当plev超出ps时不采用外推插值，一般设为Fasle
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
  
  
  lev = (/  1,  2,  3,  5,   7, 10, 20, 30, \
           50, 70,100,150, 200,250,300,400, \
          500,600,700,775, 850,925,1000 /)
   psfc= f-PS   ; PA    (time,lat,lon)
   lev = lev*100
   lev@units = "Pa"    ; to match PS
   ptop= 0             ; integrate 0==&gt;psfc at each grid point
   dp  = dpres_plevel_Wrap(lev, psfc, ptop, 0) 
;Calculates the pressure layer thicknesses of a constant pressure level coordinate system,dp(time,lev,lat,lon)
```
