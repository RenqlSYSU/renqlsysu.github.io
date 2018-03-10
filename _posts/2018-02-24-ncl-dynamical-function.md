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
	;scalar-integer设为0，边界点都将设为缺测值；
	;1，则uwnd和vwnd在经度上刚好围城一个圆，此时设置上边界和下边界为缺测值；
	;2，边界点用单向差分法估计；
	;3，uwnd和vwnd在经度上刚好围成一个圈，无重复点，此时上边界和下边界分别用单向差分法估计。
	
；以下是用球谐函数 spherical harmonics 的方法计算涡度散度，  
；用球谐函数计算得到的散度和涡度比中央差分计算得到的值更精确。  
；但只有只有当输入的风场是全球风场且无缺测值时方可使用球谐函数计算。  
	uv2vrdvf ( uwnd, vwnd, vort, divg ) ;计算涡度和散度，括号中后两个值是返回值。  
	uv2sfvpf ( uwnd, vwnd, stream_function, velocity_potential )   
	divg = uv2dvF_Wrap( uwnd, vwnd )
	vort = uv2vrF_Wrap( uwnd, vwnd )
``` 




虽然官网说用球谐函数计算散度和涡度比用中央差分法更精确，但我在用乳源地区的日降水量与涡度散度算相关时，
却发现用球谐函数计算得到的散度和涡度不是很靠谱。  
![](http://wx3.sinaimg.cn/large/006APL3qgy1fosp01jvhkj31j60t14qp.jpg)  
![](http://wx3.sinaimg.cn/large/006APL3qgy1fosp033kxoj31j60ub4qp.jpg)  

# 可降水量 #
```
	flux = wgt_vert_avg_beta ( shum&level, shum, pres_sfc, punits, opt ) / g ；将比湿垂直积分得到该地区可降水量
	;punits = 0表明shum&level和pres.sfc的单位为hPa或mb；1表明单位为Pa
	;opt = 0 计算各气压层之和；1则计算平均值
```
