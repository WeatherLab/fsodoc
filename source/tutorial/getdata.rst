############
数据准备
############

FSO系统所需数据有观测数据、初始数据和真实场数据。目前已有的观测数据为中国观测站点资料，初始场和真实场均来自0.25°× 0.25°全球系统预报和分析资料（GFS）。

GFS数据
======================

至少需要每日UTC00时和UTC12时的GFS数据，且每个时刻至少存放该时刻分析场(*.f000)及其12、24、36、48、60（f012,f024,..,f060)时效的预报场。

GFS存放路径：GFS_PATH /gfs.yyyymmddhh
 
.. code:: bash

   cd GFS_PATH
   
   > gfs.2018080112  gfs.2018080200  gfs.2018080212 gfs.2018080300

   cd gfs.2018080112
   
   > gfs.t00Z.pgrb2.0p25.f000   gfs.t00Z.pgrb2.0p25.f012  gfs.t00Z.pgrb2.0p25.f024  
     gfs.t00Z.pgrb2.0p25.f036   gfs.t00Z.pgrb2.0p25.f048  gfs.t00Z.pgrb2.0p25.f060
     
观测数据
======================
  
观测数据需存储为WRFDA可识别的little_r格式ob.ascii或prebufr格式ob.bufr。

观测数据存放路径：OBDATA_PATH/yyyymmddhh

.. code:: bash

   cd OBDATA_PATH
   
   >2018080112 2018082000 2018080212 2018080300
   
   cd 2018080112
   
   > ob.ascii
   
   
   






