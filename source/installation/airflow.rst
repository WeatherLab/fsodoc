################################
Airflow安装
################################

Airflow是一种用编程方式编写以安排和监控工作流程的平台。

安装
======================

.. code-block :: bash

      >export AIRFLOW_HOME=/指定路径/airflow #设置环境变量airflow主路径
      >pip install airflow #安装

安装完成后

.. code-block :: bash

      cd  $AIRFLOW_HOME
      >vim airflow.cfg
      
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

     >airflow initdb
     
Airflow基本概念
======================

DAG (Directed Acyclic Graph)
-----------------------------

它展示的是任务的集合，并描述了任务之间的依赖关系，以及整个DAG的一些属性，如起止时间、执行周期、重试策略等等。通常一个.py文件就是一个DAG。也可以理解为这就是一个完整的shell脚本，只是它可以保证脚本中的命令有序执行。

task 任务
-----------------------------

它就是DAG文件中的一个个Operator，描述了具体的操作步骤。

Operator 执行器
-----------------------------

airflow定义了很多的 Operator，通常一个操作就是一个特定的Operator，比如调用shell命令要用BashOperator，调用python函数要用PythonOperator，发邮件要用EmailOperator，连SSH要用SSHOperator。社区还在不断地贡献新的 Operator。

ds 日期
-----------------------------

前面的脚本里用到了{{ ds }}变量，每个DAG在执行时都会传入一个具体的时间（datetime对象），这个ds就会在 render 命令时被替换成对应的时间。

.. important:: 这里要特别强调一下，对于周期任务，airflow传入的时间是上一个周期的时间（划重点），比如你的任务是每天执行，那么今天传入的是昨天的日期，如果是周任务，那传入的是上一周今天的值。

Macros
-----------------------------

脚本里如果需要不同的时间格式或者不同的时间段怎么办，这时候就到Macro出场了，airflow本身提供了几种时间格式，比如ds_nodash，顾名思义就是不带短横-的时间格式，而且还会有一些相关的函数可以直接调用，比如ds_add可以对时间进行加减。

     

参考网页
======================

<https://airflow.incubator.apache.org/tutorial.html>


