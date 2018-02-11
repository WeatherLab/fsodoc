#############
安装
#############

实况分析系统采用Singularity容器技术进行封装，可以有效隔离依赖软件环境的搭建、环境变量的配置等细节。

系统环境配置
------------

业务工作站推荐安装Linux操作系统，以Ubuntu发行版本为例。需要安装`Sigularity <http://singularity.lbl.gov/all-releases>`_：

工作站中应该存在FSO系统的Singularity镜像文件。

.. code:: 

   > ls -al fso3.simg


准备运行环境
------------

需要创建/data目录，用来存放原始观测数据（/data/raw）、中间输入数据（/data/input）、静态数据（/data/geog）、业务运行（如/data/gfs-5km-prod-v1.0）。其中静态数据是需要提前准备好的，其它三个会在运行中创建。

.. toctree::
    :hidden:
    :titlesonly:

    airflow
    singularity
    structure
