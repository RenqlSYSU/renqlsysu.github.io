---
layout: post
title: WRF的编译、运行、namelist
categories: 模式学习
tags: WRF
author: renql
---

* content
{:toc}

# WRF的安装与编译 
由于跑理想实验，不需要前处理WPS，因此此处不记录关于 WPS 的内容

将 WRF的整个安装包拷贝至准备跑case的目录下，然后输入以下命令

```bash
./configure  #安装
./compile case_name >& log.compile  #编译，花费时间较长
# 若运行真实数据，则 case_name 为 em_real
```

For any of the `./configure` commands, a list of choices for your computer should appear. These choices range from compiling for a single processor job (serial), to using OpenMP shared-memory (smpar), distributed-memory parallelization (dmpar) options for multiple processors, or a combination of shared-memory and distributed-memory options (dm+sm). When a selection is made, a second choice for compiling nesting will appear. 

`compile` 后得到的运行程序 real.exe or ideal.exe and wrf.exe 在 `main/` 目录下(这也是检验编译是否成功的标准），并在 `test/case_name` 或 `run/` 目录下产生运行程序的链接文件，即可以在上述两个目录下运行模式。  

如果编译失败，请先回到 WRFV3 目录下，输入 `./clean –a` ，再重新查找问题，重新安装




# WRF的运行
没有包括WPS的运行  
If there is a **run_me_first.csh** script in the directory - RUN IT (this will link in extra data files needed during the run).

```bash
# if you want to run the idealized case
./ideal.exe  # produce wrfinput_d01 file for wrf model
./wrf.exe    # start to run

# if you want to run the real-data case
# place files from WPS (met_em.*) in the appropriate directory
./real.exe  # produce wrfbdy_d01 and wrfinput_d01
./wrf.exe

# if you use mpich
mpirun -np number-of-processors wrf.exe
```

一般理想实验不需要边界条件，因为它的边界条件一般都是周期边界

# namelist.input的介绍
或者可以看官网发布的 <a href="https://github.com/RenqlSYSU/project/blob/master/2018homework/mesoscale/README.namelist" target="_blank">README.namelist</a>，里面的选项与介绍更齐全

```bash
&time_control
run_days = 0
run_hours = 12,
run_minutes = 0,
run_seconds = 0,
start_year = 2000, 2000, 2000,
start_month = 01, 01, 01,
start_day = 24, 24, 24,
start_hour = 12, 12, 12,
start_minute = 00, 00, 00,
start_second = 00, 00, 00,
end_year = 2000, 2000, 2000,
end_month = 01, 01, 01,
end_day = 25, 25, 25,
end_hour = 12, 12, 12,
end_minute = 00, 00, 00,
end_second = 00, 00, 00,
interval_seconds = 21600, 					#观测数据输入的时间间隔，默认单位s
input_from_file = .true.,.true.,.true.,		#逻辑值，确定嵌套网格的初始场是否从文件输入
history_interval = 180, 60, 60,				# Frequency at which to write data to the history (wrfout) file. The default values are in minutes
frames_per_outfile = 1000, 1000, 1000,		# How many time periods will be written to each history file
restart = .false.,
restart_interval = 5000,
io_form_history = 2,
io_form_restart = 2,
io_form_input = 2,
io_form_boundary = 2,
debug_level = 0,
/

&domains
time_step	= 180,  		# 积分时间间隔，单位秒，在真实案例中建议用格距dx的6倍
time_step_fract_num	= 0,
time_step_fract_den	= 1,
max_dom	= 1,				# number of domains - set it to > 1 if it is a nested run
e_we	= 74, 112, 94
e_sn	= 61, 97, 91,
e_vert	= 30, 30, 30,
p_top_requested = 5000,
num_metgrid_levels	= 27
num_metgrid_soil_levels	= 4
dx	= 30000, 10000, 3333.33,
dy	= 30000, 10000, 3333.33,
grid_id	= 1, 2, 3,
parent_id	= 0, 1, 2,
i_parent_start	= 1, 31, 30,
j_parent_start	= 1, 17, 30,
parent_grid_ratio = 1, 3, 3,
feedback	= 1,
smooth_option	= 0,
/

&physics
mp_physics = 3, 3, 3,
ra_lw_physics = 1, 1, 1,
ra_sw_physics = 1, 1, 1,
radt = 30, 30, 30,
sf_sfclay_physics = 1, 1, 1,
sf_surface_physics = 2, 2, 2,
num_soil_layers = 4,
bl_pbl_physics = 1, 1, 1,
bldt = 0, 0, 0,
cu_physics = 1, 1, 0,
cudt = 5, 5, 5,
isfflx = 1,
ifsnow = 1,
icloud = 1,
surface_input_source = 3,
num_land_cat = 21,
sf_urban_physics = 0, 0, 0,
sf_ocean_physics = 0,
/

&dynamics
w_damping = 0,
diff_opt = 1, 1, 1,
km_opt = 4, 4, 4,
diff_6th_opt = 0, 0, 0,
diff_6th_factor = 0.12, 0.12, 0.12,
base_temp = 290.,
damp_opt = 0,
z_damp = 5000., 5000., 5000.,
dampcoef = 0.2, 0.2, 0.2,
damp_opt = 0, 0, 0,
damp_opt = 0, 0, 0,
non_hydrostatic = .true., .true., .true.,
moist_adv_opt = 1, 1,1,
scalar_adv_opt = 1, 1,1,
/

&bdy_control
spec_bdy_width = 5,
spec_zone = 1,
relax_zone = 4,
specified = .true., .false., .false.,
nested = .false., .true., .true.,
/
```
