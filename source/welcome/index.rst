#############
前言
#############

FSO（Forecast sensitivity to observation）即预报对观测的敏感性，最初由MMM / NCAR开发，是一种基于伴随理论的用于评估观测对同化系统和数值预报贡献的方法，或者说，观测对预测误差减少的影响。

本手册介绍的是为中国气象局气象探测中心搭建的一套预报误差对观测的敏感性分析系统(FSO)，更新至v2.0版本，产品包括全国15公里分辨率逐12小时的预报误差对观测的敏感性分析。系统采用Singularity Docker容器技术对FSO软件进行了封装，以便于系统移植与管理。同时采用Python Airflow流程管理软件对整个业务作业进行可视化管理。该系统能实时监测观测系统、数值预报和同化系统，并为观测系统的调整、观测数据来源的评估提供依据。

.. image:: ../images/welcome.gif
   :align: center

#############
服务器要求
#############

`PHP <http://php.net/>`_ version 7.0.15 or newer is required, with the *intl* extension installed.

A database is required for most web application programming.
Currently supported databases are:

  - MySQL (5.1+) via the *MySQLi* driver
  - PostgreSQL via the *Postgre* driver
  - Python3 external packages: pendulum

Not all of the drivers have been converted/rewritten for FSO.
The list below shows the outstanding ones.

  - MySQL (5.1+) via the *pdo* driver
  - Oracle via the *oci8* and *pdo* drivers
  - PostgreSQL via the *pdo* driver
  - MS SQL via the *mssql*, *sqlsrv* (version 2005 and above only) and *pdo* drivers
  - SQLite via the *sqlite* (version 2), *sqlite3* (version 3) and *pdo* drivers
  - CUBRID via the *cubrid* and *pdo* drivers
  - Interbase/Firebird via the *ibase* and *pdo* drivers
  - ODBC via the *odbc* and *pdo* drivers (you should know that ODBC is actually an abstraction layer)
  
#######
Credits
#######

This FSO was originally developed by `MMM/NCAR  <https://www.mmm.ucar.edu/>`_. 
The framework was written for performance in the real world, 
with many of the original scripts, codes, and
sub-systems borrowed from the code-base of `WRF Data Assimilation System
<http://www2.mmm.ucar.edu/wrf/users/wrfda/>`_. 
It was, for years, developed and maintained by 北京朗润知天科技有限公司 
and a group of enthusiastic scientists and researchers.

