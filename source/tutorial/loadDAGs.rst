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
     
     
脚本修改
================================

wrf-prod-v2.0.py和fso-prod-v2.0.py脚本中，有关时间和路径的设置需进行自定义修改。以wrf-prod-v2.0.py为例：

.. code:: bash
    
    vim wrf-prod-v2.0.py
    
    >....
    default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'start_date': datetime(2018,8,01), 
    ....
     }
     
.. note:: 'start_date'表示任务开始执行的日期

    > dag = DAG(
    'wrf-prod-00Z-v1.0', 
    default_args=default_args, 
    user_defined_macros={
        'npe': 12
    },
    schedule_interval='00 06,18 * * *')

check_gfs_command ="""
ulimit -s unlimited  \
&& cd /home/dell/FSO \
&& SINGULARITYENV_CURR_DATE={{ ts_nodash }} \
singularity exec -e -B BJ:/FSO3.4 -B china_working:/gjx_working -B china_static:/gjx_static -B /data1/raw/gfs:/gfs fso3.simg ./wrf_check_gfs.py
"""
t0 = BashOperator(
    task_id='check-gfs',
    bash_command=check_gfs_command,
    dag=dag)

obsproc_command="""
ulimit -s unlimited  \
&& cd /home/dell/FSO \
&& SINGULARITYENV_CURR_DATE={{ ts_nodash }} \
singularity exec -e -B BJ:/FSO3.4 -B china_working:/gjx_working -B china_static:/gjx_static -B /data1/input/little_r:/little_r fso3.simg ./wrf_obsproc.py
"""
    

