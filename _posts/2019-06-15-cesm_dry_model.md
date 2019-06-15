---
layout: post
title: CESM干模式
categories: 模式学习
tags: 干模式
author: renql
---

* content
{:toc}

由于实验需要，最近想跑一个有地形的干模式。然后发现CESM刚好有两种理想干模式实验，<a href="http://www.cesm.ucar.edu/models/simpler-models/dry-dynamical-core.html" target="_blank">这是其官网介绍</a>。

首先，这两种干动力核模式只有在 **2018年发布的CESM2** 中可以运行，均属于**欧拉谱变换动力核**（不知道谱模式的代码该如何修改呢？）  
 
## 干绝热斜压不稳定模式
**Dry Adiabatic Baroclinic Instability (DABI) test case**。  
该算例的编写是依据下面这篇文献：  
> Polvani, L. M., et al. (2004). "Numerically converged solutions of the global primitive equations for testing the dynamical core of atmospheric GCMs." Monthly Weather Review 132(11): 2539-2552.

它的目的是通过对一个微扰动、斜压不稳定的中纬度急流进行12天的短积分，得到一个干燥、绝热、原始方程的收敛解。其初始条件包括简单的纬向流和中纬度的局域温度扰动，每一个都是解析指定的。   

该算例有三种精度设置，T42L30, T85L30 and T85L60，第一个跑得比较快，但其结果难以收敛，适用于快速检查动力核是否正常运行；后两种的运行时间较长。  
 
该算例的初始状况是用ncl代码生成的，可以利用该代码修改初始状况。

运行流程与其他算例类似：  
```bash
./create_newcase --compset FDABIP04 --res T42z30_T42_mg17 --case $CASEDIR 
./xmlchange --file env_run.xml --id STOP_N --val 12
./case.setup
./case.setup
./case.submit
```

## Held-Suarez ##
在该算例下，CAM的动力包被以下过程所替代，一个简单的牛顿松弛法使温度场趋于纬向均一的辐射平衡温度场，在边界层采用简单线性拖曳力。该设置与下面这篇文章类似。感觉这个实验是没有年循环的。  

> Held, I. M. and M. J. Suarez (1994). "A proposal for the intercomparison of the dynamical cores of atmospheric general circulation models." Bulletin of the American Meteorological Society 75(10): 1825-1830.

该算例的默认初始场是等温、静止的状态，并通过在温度场中加入扰动来引入不稳定。生成初始场的脚本与上面那个算例的脚本写在了同一个ncl文件中。可以通过修改该文件来修改初始文件。  
T42L30, T85L30 and T85L60 当采用这三种默认精度之一时，初始条件会自动设置。  
但当采用其他精度时，则需要自己通过修改ncl文件来生成初始文件。  
然后在 **$CASEDIR/user_nl_cam** 中加入初始文件的地址：  
```
ncdata='myfilepath' 
```

该设置的常用精度同上述干绝热斜压不稳定算例，但官网说他也适用于其他精度，同时也可以用有限体积和谱元动力核。但并没有介绍怎么修改为这个。

It is recommended that an initial simulation of length 1200 days be performed to ensure the model is set up correctly. 

```bash
./create_newcase --case $CASEDIR --compset FHS94 --res T42z30_T42_mg17
./xmlchange STOP_OPTION=ndays,STOP_N=1200
./xmlchange STOP_OPTION=ndays,STOP_N=300,RESUBMIT=3 #可以没有
./case.setup
./case.setup
./case.submit
```

默认情况下，该模式会输出月平均和逐6小时的资料。其中一些变量的注意点：  
- QRS（Solar heating rate，k/s）is the temperature tendency associated with the relaxation toward the equilibrium temperature profile  
- 存在一个与水平扩散相关的非零的温度倾向值（DTH，不过我在CESM1.2的模式输出结果中没有找到这个变量），该倾向值包含**摩擦加热率**，该加热率与由动量水平扩散造成的动能耗散有关，另外还包含一个**修正加热率**，用以解释水平扩散应用于模型高度（不是气压高度）的这一事实。  
- 逐6小时的瞬时场中似乎只包含了UVT三个变量

官网还提供了NCL脚本来画 eddy temperature variance, northward eddy momentum flux and northward eddy heat flux，可以下载下来学习一下他们是怎么计算**涡旋通量**的。

此外，在这个算例下面还介绍了很多如何修改默认设置的方法，竟然有动力核、地形的修改方法。
![](http://wx1.sinaimg.cn/mw690/006fa9Xlgy1g41p04tpk8j30gz07twer.jpg)

### 水平扩散系数的选择 ###
当选用欧拉谱模式动力核，必须考虑水平扩散系数的选择。  
默认设置是用了四阶超扩散，最小尺度上的阻尼时间标度为0.5天。选择这个时间尺度是因为它被发现是在水平分辨率为T42和T85的涡度场中仍然能产生光滑结构的最弱阻尼强度之一。  

决定水平扩散的阶数与强度的参数是 **eul_hdif_order** 和 **eul_hdif_coef**。这两个参数与阻尼时间标度之间的关系是：  
`eul_hdif_coef = (1/tau)(a^2/(n(n+1)))^(eul_hdif_order/2.)`   
where tau is the required damping timescale, a is the radius of the Earth and n is the total wavenumber of the smallest scale

该参数的修改是在 **$CASEDIR/user_nl_cam** 文件中

### 动力核的修改 ###
可以通过修改精度来修改干模式的动力核。

```bash
#  run the finite volume dynamical core at 2 degree resolution
./create_newcase --case $CASEDIR --compset FHS94 --res f19z30_f19_mg17 --mach $MACH --run-unsupported

# run for a 1 degree with the spectral element dynamical core
./create_newcase --case $CASEDIR --compset FHS94 --res ne30z30_ne30_g16 --mach $MACH --run-unsupported
```

如果希望将垂直分辨率更改为不受官方支持的分辨率，只需要一个包含垂直级别的初始条件文件。

在CESM2.0版本中，当使用**有限元FV**或**谱元素SE**动力核时，需要关闭 **the energy fixer（能量固定器或调整器）**，在CESM2.1及后续版本中，当采用上述两个动力核时，会默认关闭该功能。     
the energy fixer是用来保证能量守恒的，因为在干模式的物理过程不能像完整的大气环流模式GCM那样使能量保持守恒，因此需要关闭该功能。

手动关闭**the energy fixer**的方法：
```bash
cp $CESM/components/cam/src/physics/simple/physpkg.F90  $CASEDIR/SourceMods/src.cam/physpkg.F90
vi $CASEDIR/SourceMods/src.cam/physpkg.F90
```  

修改**physpkg.F90**中下面这部分代码, To turn off the energy fixer, the call to physics_update must be commented out 
```fortran
    !===================================================
    ! Global mean total energy fixer
    !===================================================
    call t_startf('energy_fixer')

    if (dycore_is('LR') .or. dycore_is('SE')) then
      call check_energy_fix(state, ptend, nstep, flx_heat)
      call physics_update(state, ptend, ztodt, tend) ! it should be commented out to turn of the energy fixer
      call check_energy_chng(state, tend, "chkengyfix", nstep, ztodt, zero, zero, zero, flx_heat)
      call outfld( 'EFIX', flx_heat    , pcols, lchnk   )
      call physics_ptend_dealloc(ptend)
    end if
```

### 在干模式中加入地形 ###
在 **$CASEDIR/user_nl_cam** 文件中加入下面两句话即可，使用的地形文件中必须包含变量 **PHIS（surface geopotential）in units of m2/s2** ，使用与模式相同的精度。如果使用的是真实的地形，可以直接使用CESM的地形资料（文件地址可能是 **$INPUTDIR/atm/cam2/topo/**）    

```
use_topo_file = .true.
bnd_topo      = "location_of_your_topo_file"
```
