################################
Airflow介绍
################################

采用基于Python语言的Airflow流程管理软件，对实时运行的FSO作业进行管理。针对每个作业编写DAG（定向非循环图）配置脚本，设置各个任务以及任务间的执行依赖关系。Airflow后台运行程序包括：1）调度器（Scheduler），负责在指定时间运行作业；2）管理页面后端服务器（Webserver），负责向前端（浏览器）提供HTML服务。通过在运行机器上访问http://localhost:8080/admin链接可以查看所有在运行的作业列表。其中DAG列显示的是作业名称，如gfs-10km-prod，点击可以进入作业详情页面；Schedule列显示的是作业运行时间，如 30 * * * *表示每小时的30分运行，@hourly是Airflow提供的一种简记，表明每小时00分运行；Recent Tasks列显示作业运行状态，以不同颜色表示不同运行状态，如深绿色表示已经完成的作业数，浅绿色是正在运行的任务数，灰色是等待执行的任务数，红色表示出错的任务数，通过点击相应颜色的按钮可以进入查看任务；Last Run列可以查看最近运行时间；Links列提供一些快捷的操作按钮。

安装
======================

airflow 的安装十分简单，用``pip``来安装：

.. code-block :: bash

        export AIRFLOW_HOME=~/airflow
        pip install airflow[slack]
        airflow initdb

pip 安装的**slackclient**为可选，当你需要通知到**slack**时才会用到，但我十分建议也一起安装， 能够及时收到任务执行状况报告。

一些概念
======================

DAG (Directed Acyclic Graph)
-----------------------------

它表示的是一些任务的集合，描述了任务之间的依赖关系，以及整个DAG的一些属性， 比如起止时间，执行周期，重试策略等等。通常一个.py文件就是一个DAG。 你也可以理解为这就是一个完整的shell脚本，只是它可以保证脚本中的命令有序执行。

task 任务
-----------------------------


它就是DAG文件中的一个个Operator，它描述了具体的一个操作。

Operator 执行器
-----------------------------

airflow定义了很多的 Operator，通常一个操作就是一个特定的 Operator， 比如调用 shell 命令要用 BashOperator，调用 python 函数要用PythonOperator， 发邮件要用 EmailOperator，连SSH要用 SSHOperator。社区还在不断地贡献新的 Operator。

ds 日期
-----------------------------

前面的脚本里用到了{{ ds }}变量，每个DAG在执行时都会传入一个具体的时间（datetime对象）， 这个ds就会在 render 命令时被替换成对应的时间。

.. important:: 这里要特别强调一下， 对于周期任务，airflow传入的时间是上一个周期的时间（划重点），比如你的任务是每天执行， 那么今天传入的是昨天的日期，如果是周任务，那传入的是上一周今天的值。

Macros
-----------------------------

上一条说了ds变量，你肯定会说我的脚本里如果需要不同的时间格式或者不同的时间段怎么办， 这时候就到Macro出场了，airflow本身提供了几种时间格式，比如ds_nodash，顾名思义就是不带短横-的时间格式， 而且还会有一些相关的函数可以直接调用，比如ds_add可以对时间进行加减。

airflow 配置
-----------------------------

前面为了尽快展示airflow的强大，我跳过了许多东西，比如它的配置。 在 airflow 初始化时，它会自动在AIRFLOW_HOME目录下生成ariflow.cfg文件，现在打开它让我们看看里面的构造。

executor
-----------------------------

这是airflow最关键的一个配置，它指示了airflow以何种方式来执行任务。它有三个选项：

- SequentialExecutor：表示单进程顺序执行，通常只用于测试
- LocalExecutor：表示多进程本地执行，它用python的多进程库从而达到多进程跑任务的效果。
- CeleryExecutor：表示使用celery作为执行器，只要配置了celery，就可以分布式地多机跑任务，一般用于生产环境。

sql_alchemy_conn
-----------------------------

这个配置让你指定 airflow 的元信息用何种方式存储，默认用 sqlite，如果要部署到生产环境，推荐使用 mysql。

smtp
-----------------------------

如果你需要邮件通知或用到 EmailOperator 的话，需要配置发信的 smtp 服务器。

celery
-----------------------------

前面所说的当使用 CeleryExecutor 时要配置 celery 的环境。


命令
============================

airflow 的所有执行操作都需要在命令行下完成，界面只能看任务的依赖， 包括任务执行状态，但如果任务失败了，还是要在命令行下执行。
airflow 的命令总的来说很符合直觉，常用的有如下几个：

- test： 用于测试特定的某个task，不需要依赖满足
- run: 用于执行特定的某个task，需要依赖满足
- backfill: 执行某个DAG，会自动解析依赖关系，按依赖顺序执行
- unpause: 将一个DAG启动为例行任务，默认是关的，所以编写完DAG文件后一定要执行这和要命令，相反命令为pause
- scheduler: 这是整个 airflow 的调度程序，一般是在后台启动
- clear: 清除一些任务的状态，这样会让scheduler来执行重跑

从上面的命令顺序也可以看出，通常的执行顺序是这样：编写完DAG文件， 直接用backfill命令测试整个DAG是否有问题，如果单个任务出错，查看log解决错误， 这时可以用test来单独执行，如果有依赖关系就用run执行，都搞定了后就用unpause打开周期执行， 当然 scheduler 是在后台默认打开的。之后运行过程中发现需要重跑则用clear命令。
