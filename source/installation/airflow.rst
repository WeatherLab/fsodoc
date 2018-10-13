################################
Airflow安装
################################

Airflow是一种用编程方式编写以安排和监控工作流程的平台。

安装
======================

.. code-block :: bash

      export AIRFLOW_HOME=/指定路径/airflow #设置环境变量airflow主路径
      pip install airflow #安装

安装完成后

.. code-block :: bash

      cd  $AIRFLOW_HOME
      vim airflow.cfg
      
主要修改以下参数

.. code-block :: bash

      airflow_home = /指定路径/airflow   #airflow主路径
      dags_folder = /指定路径/airflow/dags #dag python文件目录 
      executor = LocalExecutor #先使用local模式
      base_log_folder = /指定路径/airflow/logs #主日志目录
      sql_alchemy_conn = postgresql+psycopg2://airflow:fso2018@localhost #指定元数据存储方式，目前采用Postgresql
      
      [webserver]
      authenticate = True
      filter_by_owner = true
      base_url = http://localhost:8080
      web_server_host = XXX.XXX.XXX.XXX  #web server 机器IP
      base_url = http://XXX.XXX.XXX.XXX:8080  #web server 机器IP:PORT

初始化数据库

.. code-block :: bash

     airflow initdb
     

参考网页
======================

<https://airflow.incubator.apache.org/tutorial.html>


