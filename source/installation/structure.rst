#############
运行目录
#############

FSO目录结构

├── FSO3.4   #FSO主目录

│   ├── be    #背景误差协方差路径

│   ├── fc    #存放分析场（ wrfvar_output）

│   ├── fsoplot  #数据库处理及绘图

│   ├── ob  #观测前处理后观测资料存放路径

│   ├── plot  # 额外的绘图脚本

│   ├── rc   #初始场（背景场）和边界场、真实场路径

│   └── run  #FSO运行路径,及wrapper_run_fso_v3.4.ksh参数设置脚本

├── china_static # wps\wrf所需namelist、解码表等存放目录

├── china_working #初始场、边界场生成，及观测前处理

├── scripts  #所有步骤对应的外部脚本
