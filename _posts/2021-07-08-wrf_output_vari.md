---
layout: post
title: WRF模式默认输出的变量
categories: 模式学习
tags: WRF
author: renql
---

* content
{:toc}

XLAT           1  0  LATITUDE, SOUTH IS NEGATIVE (degree_north)
XLONG          1  0  LONGITUDE, WEST IS NEGATIVE (degree_east)
LU_INDEX       1  0  LAND USE CATEGORY (-)
土地利用类型，一共有24中，不过这里的数值是从2到16，目前只知道16代表水，3代表耕田。

VAR_SSO        1  0  variance of subgrid-scale orography (m2)   
地形次网格的方差，不知道有什么用，但是海洋上都是0，陆地上有一部分是100000—300000

LAP_HGT        1  0  Laplacian of orography (m)
范围：-600—500

U             19  0  x-wind component (m s-1)
V             19  0  y-wind component (m s-1)
W             19  0  z-wind component (m s-1)

PH            19  0  perturbation geopotential (m2 s-2) 
扰动位势：result—p3-21图，不知道是什么东西，但随着高度的升高，其数值逐渐增大，难道是因为高空垂直运动增大吗？奇怪？

PHB           19  0  base-state geopotential (m2 s-2)
基本位势（平均位势）：台风中心始终是低重力势能，随着高度逐渐增大
Z=10的时候全部充满

T             19  0  perturbation potential temperature (theta-t0) (K)
扰动位温，有一个高温中心

MU             1  0  perturbation dry air mass in column (Pa)
干空气柱扰动气压：-3000~1500

MUB            1  0  base state dry air mass in column (Pa)
平均干空气柱气压：55000~95000

NEST_POS       1  0  - (-)
内嵌网格位置，没什么用

P             19  0  perturbation pressure (Pa)
扰动气压

PB            19  0  BASE STATE PRESSURE (Pa)
基本气压，和height的图形不一样，且台风中心气压高

P_HYD         19  0  hydrostatic pressure (Pa) 液体静压力
Q2             1  0  QV at 2 M (kg kg-1)地面2米高度的比湿、温度
T2             1  0  TEMP at 2 M (K)
TH2            1  0  POT TEMP at 2 M (K)
PSFC           1  0  SFC PRESSURE (Pa) 表面气压
U10            1  0  U at 10 M (m s-1)  地面10米分厂的纬向分量、径向分量
V10            1  0  V at 10 M (m s-1)
QVAPOR        19  0  Water vapor mixing ratio (kg kg-1)（0.009~0.019）
QCLOUD        19  0  Cloud water mixing ratio (kg kg-1)（0~0.0018）
QRAIN         19  0  Rain water mixing ratio (kg kg-1)
QICE          19  0  Ice mixing ratio (kg kg-1)
QSNOW         19  0  Snow mixing ratio (kg kg-1)
QGRAUP        19  0  Graupel mixing ratio (kg kg-1)

SHDMAX         1  0  ANNUAL MAX VEG FRACTION (-)
SHDMIN         1  0  ANNUAL MIN VEG FRACTION (-)
SNOALB         1  0  ANNUAL MAX SNOW ALBEDO IN FRACTION (-)

TSLB           4  0  SOIL TEMPERATURE (K)
SMOIS          4  0  SOIL MOISTURE (m3 m-3)
SH2O           4  0  SOIL LIQUID WATER (m3 m-3)
SMCREL         4  0  RELATIVE SOIL MOISTURE (-)

SEAICE         1  0  SEA ICE FLAG (-)
XICEM          1  0  SEA ICE FLAG (PREVIOUS STEP) (-)
SFROFF         1  0  SURFACE RUNOFF (mm)
UDROFF         1  0  UNDERGROUND RUNOFF (mm)
IVGTYP         1  0  DOMINANT VEGETATION CATEGORY (-)
ISLTYP         1  0  DOMINANT SOIL CATEGORY (-)
VEGFRA         1  0  VEGETATION FRACTION (-)
GRDFLX         1  0  GROUND HEAT FLUX (W m-2)
ACGRDFLX       1  0  ACCUMULATED GROUND HEAT FLUX (J m-2)
ACSNOM         1  0  ACCUMULATED MELTED SNOW (kg m-2)
SNOW           1  0  SNOW WATER EQUIVALENT (kg m-2)
SNOWH          1  0  PHYSICAL SNOW DEPTH (m)
CANWAT         1  0  CANOPY WATER (kg m-2)
SSTSK          1  0  SKIN SEA SURFACE TEMPERATURE (K)
COSZEN         1  0  COS of SOLAR ZENITH ANGLE (dimensionless)
LAI            1  0  LEAF AREA INDEX (m-2/m-2) 叶面积指数
VAR            1  0  OROGRAPHIC VARIANCE (-)
MAPFAC_M       1  0  Map scale factor on mass grid (-)
MAPFAC_MX      1  0  Map scale factor on mass grid, x direction (-)
MAPFAC_MY      1  0  Map scale factor on mass grid, y direction (-)
MF_VX_INV      1  0  Inverse map scale factor on v-grid, x direction (-)
F              1  0  Coriolis sine latitude term (s-1)
E              1  0  Coriolis cosine latitude term (s-1)
SINALPHA       1  0  Local sine of map rotation (-)
COSALPHA       1  0  Local cosine of map rotation (-)
HGT            1  0  Terrain Height (m)
TSK            1  0  SURFACE SKIN TEMPERATURE (K)
RAINC          1  0  ACCUMULATED TOTAL CUMULUS PRECIPITATION (mm)，4km以下基本认为对流可分辨，不开对流参数化，RAINC是0
RAINSH         1  0  ACCUMULATED SHALLOW CUMULUS PRECIPITATION (mm)
RAINNC         1  0  ACCUMULATED TOTAL GRID SCALE PRECIPITATION (mm)
SNOWNC         1  0  ACCUMULATED TOTAL GRID SCALE SNOW AND ICE (mm)
GRAUPELNC      1  0  ACCUMULATED TOTAL GRID SCALE GRAUPEL (mm)
HAILNC         1  0  ACCUMULATED TOTAL GRID SCALE HAIL (mm)
CLDFRA        19  0  CLOUD FRACTION (-)
SWDOWN         1  0  DOWNWARD SHORT WAVE FLUX AT GROUND SURFACE (W m-2)
GLW            1  0  DOWNWARD LONG WAVE FLUX AT GROUND SURFACE (W m-2)
SWNORM         1  0  NORMAL SHORT WAVE FLUX AT GROUND SURFACE (SLOPE-DEPENDENT) (W m-2)
OLR            1  0  TOA OUTGOING LONG WAVE (W m-2)
ALBEDO         1  0  ALBEDO (-)
CLAT           1  0  COMPUTATIONAL GRID LATITUDE, SOUTH IS NEGATIVE (degree_north)
ALBBCK         1  0  BACKGROUND ALBEDO (-)
EMISS          1  0  SURFACE EMISSIVITY (-)
NOAHRES        1  0  RESIDUAL OF THE NOAH SURFACE ENERGY BUDGET (W m{-2})
TMN            1  0  SOIL TEMPERATURE AT LOWER BOUNDARY (K)
XLAND          1  0  LAND MASK (1 FOR LAND, 2 FOR WATER) (-)
UST            1  0  U* IN SIMILARITY THEORY (m s-1)
PBLH           1  0  PBL HEIGHT (m)
HFX            1  0  UPWARD HEAT FLUX AT THE SURFACE (W m-2)
QFX            1  0  UPWARD MOISTURE FLUX AT THE SURFACE (kg m-2 s-1)
LH             1  0  LATENT HEAT FLUX AT THE SURFACE (W m-2)
ACHFX          1  0  ACCUMULATED UPWARD HEAT FLUX AT THE SURFACE (J m-2)
ACLHF          1  0  ACCUMULATED UPWARD LATENT HEAT FLUX AT THE SURFACE (J m-2)
SNOWC          1  0  FLAG INDICATING SNOW COVERAGE (1 FOR SNOW COVER) (-)

SR             1  0  fraction of frozen precipitation (-)
固体降水比例

LANDMASK       1  0  LAND MASK (1 FOR LAND, 0 FOR WATER) (-)
LAKEMASK       1  0  LAKE MASK (1 FOR LAKE, 0 FOR NON-LAKE) (-)
SST            1  0  SEA SURFACE TEMPERATURE (K)
SST_INPUT      1  0  SEA SURFACE TEMPERATURE FROM WRFLOWINPUT FILE (K)

pressure      19  0  Model pressure (hPa)，就是那十九层的气压，没有用，删掉
height        19  0  Model height (km)，台风中心高度低，也就是低压中心，到17层时，该高度已不明显，第十层时充满整个画面
tk            19  0  Temperature (K)
tc            19  0  Temperature (C)这两个温度是一样的，就只是单位不一样，且到19层时，台风中心温度低于四周海洋，而在19层以前，台风中心温度高于四周海洋。
