#################
DAG加载
#################


DAG加载
======================
.. code:: bash

     cd $AIRFLOW_HOME/dags

将DAG python脚本（fso-prod-v2.0.py,wrf-prod-v2.0.py)放入该目录下

.. code:: bash

     ls -all

     > fso-prod-v2.0.py   wrf-prod-v2.0.py
     
     
DAG基本构架
================================

以wrf-prod-v2.0.py为例：

.. code:: bash
    
    vim wrf-prod-v2.0.py
    
    >default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'start_date': datetime(2018,8,01),  #任务开始执行的日期#
    'end_date': datetime(2030, 12, 31),  #任务开始终止的日期#
     }
     
.. code:: bash

    > dag = DAG(
    'wrf-prod-v2.0', #dag_id
    default_args=default_args, 
    user_defined_macros={ 'npe': 12 },  #运行该DAG所占节点数
    schedule_interval='00 06,18 * * *') #任务启动时间：每天北京时间06时，18时
    
.. code:: bash

    > check_gfs_command ="""    
      ulimit -s unlimited  \      
      && cd /home/FSO \    #FSO主目录
      && SINGULARITYENV_CURR_DATE={{ ts_nodash }} \     
      singularity exec -e -B china_FSO:/FSO3.4 -B china_working:/gjx_working -B china_static:/gjx_static -B /data1/raw/gfs:/gfs fso3.simg ./wrf_check_gfs.py""" # 将主机路径与容器路径绑定，冒号前是主机目录路径，冒号后面是容器目录路径；运行wrf_check_gfs.py

.. code:: bash
    >t0 = BashOperator(
     task_id='check-gfs', # task_id
     bash_command=check_gfs_command, #执行定义的任务
     dag=dag)
 ........    
 
参考网页
================================ 

<http://airflow.incubator.apache.org/tutorial.html>

