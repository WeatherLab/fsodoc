#############
运行目录
#############

FSO目录结构
------------------

/home/FSO

├── china_FSO   #FSO主目录

│   ├── be   

│   ├── fc    

│   ├── fsoplot  

│   ├── ob  

│   ├── plot  

│   ├── rc  

│   ├── run  

├── china_static

├── china_working 

├── scripts

脚本放置
------------------
  
.. code:: bash
 
      cd /home/FSO/china_FSO/be
      > be.d01.dat
      cd /home/FSO/china_FSO/fsoplot
      > data2pg.py drawfso.py drawlev.py drawmap.py drawvar.py drawvarlev.py   
        sql.py timepath.py chn.ncl fso.ncl map.ncl var.ncl varmap.ncl
      cd /home/FSO/china_FSO/run
       >wrapper_run_fso_v3.4.ksh
      cd /home/FSO/china_static
       > 
      cd /home/FSO/scripts
       >fso_2pg.py fso_adj.py fso_2pg.py fso_check_ana.py fso_check_icbc.py fso_check_obs.py
        fso_da.py fso_err.py fso_forcing.py fso_impact.py fso_nl.py fso_plot.py china_common.py
        wrf_check_gfs.py wrf_obsproc.py wrf_prod.py wrf_real_ana.py wrf_real_icbc.py wrf_wps.py
        
 
   
