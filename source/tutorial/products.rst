################
产品的输出和绘图
################

FSO输出结果位于作业目录下的FSO/west3.4/run/ccyymmddhh/obsimpact/gts_omb_oma_01, 为了易于解释FSO的结果，目前使用NCL语言编写了绘制多种要素的图形在fsoplots子目录。以下是主要的产品输出:

.. note:: 负值代表该观测减小预报误差;正值代表该观测增加预报误差

.. figure:: ./images/map_sound_all.png
   :align: center

   探空观测对12小时预报误差的贡献

.. figure:: ./images/map_surface_all.png
   :align: center

   地面观测对12小时预报误差的贡献

.. figure:: ./images/fso_all.png
   :align: center

   观测类型对12小时预报误差的贡献

.. figure:: ./images/var_all.png
   :align: center

   变量类型对12小时预报误差的贡献

.. figure:: ./images/lev_all.png
   :align: center

   不同层次变量类型对12小时预报误差的贡献
