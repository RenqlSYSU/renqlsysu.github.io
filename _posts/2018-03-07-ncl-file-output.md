---
layout: post
title: ncl文件的操作函数、输入与输出
categories: ncl
tags: ncl 整理
author: renql
---

* content
{:toc}

# 文件操作函数
```
f1 = addfile("ghg_hist_1765-2005_c091218.nc","r")
  
fatts = getfileatts(f1)     ;返回文件的全局变量名称，只返回名称
  do na=0,dimsizes(fAtts)-1
    print ("f@" + fAtts(na) + " = " + f@$fAtts(na)$) ；可查看各全局变量的具体内容
  end do
  
dnames = getfiledimnames(f1) ;返回一维字符数组
dsizes = getfiledimsizes(f1) ;返回一维整型数组，顺序同dnames
print(dSizes+"   "+dNames)   ;输出查看

vnames = getfilevarnames(f1) ;返回一维字符串数组
vatts  = getfilevaratts(f1,vname(0))  ;返回一维字符型数组
vtype  = getfilevartypes(f1,vname(0)) ;返回一维字符型数组
vdname = getfilevardimnames(f1,vname(0))
vdsize = getfilevardimsizes(f1,vname(0))
```




# 输出数据到ASCII文件
1. write_matrix 输出二维数据，data数组中好像不能有字符串   
```
	opt 		= True
	opt@fout 	= "文件路径"
	opt@title 	= "输出内容的标题"
	opt@tspace  = "标题左边的空格数"
	opt@row 	= True 			;表示会打印行数，若为False则不打印行数
write_matrix(data,fmtf,opt)		;data只能是二维的，fmtf是打印的格式如"9f12.6"
```

2. write_table 输出规则列表，可以有字符串
```
	write_table(filename,option,alist,fmtf)
	;option有两种，"w"指重新写，如之前有内容，会覆盖；"a"是接着之前的内容往下写
	;alist是要写的数据，若有a = (/"ab","bc","cd"/),b = (/1,2,3/),alist = [/a,b/],会输出三行两列的数据
	;fmtf必须对输出的每一行数据进行格式规定，不能用"7f12.6"这样的方式重复，且表述方式也与上述不同，如"%d%16.2f%s%d%ld"表示输出整数、小数、字母、整数、整数
```

# 输出数据到二进制文件，可用Fortran读取

关于ncl、Fortran、grads对二进制文件的处理区别介绍博客：<a href="http://bbs.06climate.com/home.php?do=blog&id=3487&mod=space&uid=12776" target="_blank"> http://bbs.06climate.com/home.php?do=blog&id=3487&mod=space&uid=12776 </a>

最近发现这篇博文在介绍跨平台数据传输也说得挺好的 <a href="https://ncllearning.blogspot.com/2015/03/binary.html" target="_blank"> https://ncllearning.blogspot.com/2015/03/binary.html </a>。  

总结一下，在要跨平台应用数据时，存储时都统一用直接存取方式 **direct access**。

ncl输出dat文件，类似于fortran中的"form=binary,access=direct"
```xml
etfileoption("bin","WriteByteOrder","LittleEndian")
system("rm -f " + fileout(nf))

do nv = 0, nvar-1, 1
do nt = 0, ntime-1, 1
do nl = 0, nlev-1, 1
    fbindirwrite(fileout(nf),forc(nv,nt,nl,:,:)) ；若写入的数据文件之前就存在，新写入的数据将写在后面，而不是覆盖
end do
end do
end do
```
一条数据的长度为 precision*nlat*nlon，如果是单精度浮点，为4字节，如果为双精度浮点，为8字节。可以通过查看输出的dat文件大小来检查输出是否正确，例如这里输出的dat文件大小应该为（假设是双精度浮点）：`8*nlat*nlon*nlev*ntime*nvar/1024/1024/1024 GB`

用ncl读取上述dat文件
```xml
etfileoption("bin","ReadByteOrder","LittleEndian")
irec = 0
do nv = 0, nvar-1, 1
do nt = 0, ntime-1, 1
do nl = 0, nlev-1, 1
    dzdt(nv,nt,nz,:,:) = fbindirread(filedat(nf),irec,(/nlat,nlon/),"double")
    irec = irec + 1
end do
end do
end do
```

用Fortran读取上述dat文件，并重新输出。
```fortran
    program text1
	 parameter(nx=144,ny=73,nz=17,nt=12)
	 real u(nx,ny,nz,nt)
	 real v(nx,ny,nz,nt)    
	 open(unit=1,file='E:\ftp\GrADS\uwnd.dat',status='old',form="binary",convert='LITTLE_ENDIAN',access="direct",recl=4*nx*ny)
	 irec=1
	 do it=1,nt
	 do iz=1,nz
	   read(1,rec=irec) ((u(i,j,iz,it),i=1,nx),j=1,ny)
	   irec=irec+1
	 end do 
	 end do 
	 
	 open(unit=3,file='E:\ftp\GrADS\u.dat',status='replace',form="binary",convert='LITTLE_ENDIAN',access="direct",recl=4*nx*ny)
	 irec=1
	 do it=1,nt 
	 do iz=1,nz
	   write(3,rec=irec) ((u(i,j,iz,it),i=1,nx),j=1,ny)
	   irec=irec+1
	 end do 
	 do iz=1,nz
	   write(3,rec=irec) ((v(i,j,iz,it),i=1,nx),j=1,ny)
	   irec=irec+1
	 end do 
	 end do
	 end 
```
对应dat的ctl文件书写例子：
```
dset d:\grads\uvwnd.dat
title monthly longterm mean u wind from the NCEP reanalysis
undef -9.96921e+36
xdef 144 linear 0 2.5
ydef 73 linear -90 2.5
zdef 17 levels 1000 925 850 700 600 500 400 300 250 200 150 100 70 50 30 20 10
tdef 12 linear 00z01jan1948 1mo
vars 2
uwnd 17 99 monthly longterm mean of u-wind
vwnd 17 99 monthly longterm mean of u-wind
endvars
```

