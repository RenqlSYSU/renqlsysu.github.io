---
layout: post
title: Namelist Variables
categories: 模式学习
tags: 整理 气候模式
author: renql
---

* content
{:toc}

**dtime**：动力与物理耦合时间间隔，以秒为单位，取决于精度和动力核  

**ext_frc**:external forcings, 属于chem_inparm   
**sol_facti_cloud_borne**：In-cloud scav for cloud-borne aerosol tuning factor   
**srf_emis**：the surface emissions data   
**tracer_cnst**：the prescribed chemical constituents data  

**bnd_topo**:Full pathname of time-invariant boundary dataset for topography fields   
**bndtvo**：Full pathname of time-variant ozone mixing ratio boundary dataset.   
**bndtvghg**：Full pathname of time-variant boundary dataset for greenhouse gas surface values.    
**bndtvaer**：Full pathname of time-variant boundary dataset for aerosol masses   
**bndtvs**：Full pathname of time-variant sea-surface temperature and sea-ice concentration boundary dataset.    
**bndtvs_domain**:Full pathname of grid file for time-variant sea-surface temperature and sea-ice concentration boundary dataset.   

**cldfrc**:cloud fraction   
**cldsed**:cloud sedimentation（云沉降）  
  
**water_refindex_file**：Full pathname of dataset for water refractive indices used in modal aerosol optics   
**iceopticsfile**：filepath and name for ice optics data for rrtmg   
**liqopticsfile**：filepath and name for liquid cloud (gamma distributed) optics data for rrtmg     
