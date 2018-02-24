---
layout: post
title: ncl常用动力学函数整理
categories: ncl
tags: ncl 动力气象 整理
author: renql
---

* content
{:toc}

# 散度涡度 divergence and vorticity #
```
；以下是用中央差分的方法计算涡度散度
	divg = uv2dv_cfd ( uwnd, vwnd, uwnd&lat, uwnd&lon, scalar-integer )
	vort = uv2vr_cfd ( uwnd, vwnd, uwnd&lat, uwnd&lon, scalar-integer )
	
；以下是用球谐函数 spherical harmonics 的方法计算涡度散度，  
；用球谐函数计算得到的散度和涡度比中央差分计算得到的值更精确。  
；但只有只有当输入的风场是全球风场且无缺测值时方可使用球谐函数计算。  
	uv2vrdvf ( uwnd, vwnd, vort, divg ) ;计算涡度和散度，括号中后两个值是返回值。  
	uv2sfvpf ( uwnd, vwnd, stream_function, velocity_potential )   
	divg = uv2dvF_Wrap( uwnd, vwnd )
	vort = uv2vrF_Wrap( uwnd, vwnd )
```  



# 可降水量 #
```
	flux = wgt_vert_avg_beta ( shum&level, shum, pres_sfc, 0, 0 ) / g ；将比湿垂直积分得到该地区可降水量
```
