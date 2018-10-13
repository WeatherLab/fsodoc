############
Airflow启动
############

启动
======================

Airflow后台运行程序包括

.. code-block:: bash

     airflow webserver  #启动调度器

     airflow scheduler #启动后端网页

调度器（Scheduler），负责在指定时间运行作业。

管理页面后端服务器（Webserver），负责向前端（浏览器）提供HTML服务。


Airflow基础命令
============================

airflow的所有执行操作都需要在命令行下完成，界面只能看任务的依赖，包括任务执行状态，但如果任务失败了，还是要在命令行下执行。
airflow的命令总的来说很符合直觉，常用的有如下几个：

- test： 用于测试特定的某个task，不需要依赖满足
- run: 用于执行特定的某个task，需要依赖满足
- backfill: 执行某个DAG，会自动解析依赖关系，按依赖顺序执行
- unpause: 将一个DAG启动为例行任务，默认是关的，所以编写完DAG文件后一定要执行这和要命令，相反命令为pause
- scheduler: 这是整个 airflow 的调度程序，一般是在后台启动
- clear: 清除一些任务的状态，这样会让scheduler来执行重跑

从上面的命令顺序也可以看出，通常的执行顺序是这样：编写完DAG文件，直接用backfill命令测试整个DAG是否有问题，如果单个任务出错，查看log解决错误，这时可以用test来单独执行，如果有依赖关系就用run执行，都搞定了后就用unpause打开周期执行，当然 scheduler 是在后台默认打开的。之后运行过程中发现需要重跑则用clear命令。

举例
-----------------------------

1.

.. code-block:: bash

     airflow test dag_id task_id execution_date

用于测试该dag_id中的task_id这一任务，并给定测试时间 例如：

.. code-block:: bash

    airflow test fso-prod-00Z-v2.0 2-3-adj-backward 2018-08-16T02:00:00

2.

.. code-block:: bash
 
    airflow backfill dag_id -s start_date -e end_date 

用于反算和补充某个时刻或某段时间的dag流程,注意的是start_date和end_date之间必须要相差一天,例如：

.. code-block:: bash

    airflow backfill fso-prod-00Z-v2.0 -s 2018-08-16 -e 2018-08-17
