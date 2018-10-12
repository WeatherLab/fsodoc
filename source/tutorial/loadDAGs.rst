#################
DAG加载与Airflow启动
#################


DAG加载

.. code::

     cd $AIRFLOW_HOME/dags

将DAG python脚本（fso-prod-v2.0.py,wrf-prod-v2.0.py)放入该目录下

.. code::

     ls -all

     fso-prod-v2.0.py

     wrf-prod-v2.0.py
     

####Airflow启动

     airflow webserver  #启动调度器

     airflow scheduler #启动后端网页

调度器（Scheduler），负责在指定时间运行作业。

管理页面后端服务器（Webserver），负责向前端（浏览器）提供HTML服务。
