#################
Singularity安装
#################

实况分析系统采用Singularity容器技术进行封装，可以有效隔离依赖软件环境的搭建、环境变量的配置等细节。

安装 
======================

业务工作站推荐Linux操作系统，Ubuntu/centos发行版本,以centos为例：

.. code-block:: bash 

    #安装或更新依赖
    
    sudo yum update && \
    sudo yum groupinstall 'Development Tools' && \
    sudo yum install libarchive-devel

    #下载并安装最新版本
    
    git clone https://github.com/singularityware/singularity.git
    cd singularity
    ./autogen.sh
    ./configure --prefix=/usr/local --sysconfdir=/etc
    make
    sudo make install

导入镜像文件
======================

工作站中应存在FSO Singularity镜像文件fso3.simg。

.. code-block:: bash 

       >ls -al fso3.simg

参考网页
======================
<http://singularity.lbl.gov/docs-installation>


