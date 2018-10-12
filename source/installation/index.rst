#############
安装
#############

包括以下几个部分:

-  :doc:`安装Airflows <airflow>`, 介绍Airflow的安装
-  :doc:`安装Singularity <singularity>`, 介绍Singularity的安装
-  :doc:`准备运行目录 <structure>`, 介绍运行环境的准备。

@startuml
   Alice -> Bob: Authentication Request
   Bob --> Alice: Authentication Response

   Alice -> Bob: Another authentication Request
   Alice <-- Bob: another authentication Response
@enduml

.. toctree::
    :hidden:
    :titlesonly:

    airflow
    singularity
    structure
