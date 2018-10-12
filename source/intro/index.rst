#####################
WRF FSO 简介
#####################

WRF（Weather Research And Forecast Model) FSO系统包括预报模式（WRF）及其伴随（WRFPLUS）、变分数据同化系统（WRFDA）和诊断、绘图工具（TOOLS)。该系统框架和流程如下：


1.观测场与背景场进入WRFDA得到分析场，从分析场和背景场出发，分别进行相同时效的非线性前向预报。

2.计算两组预报场与真实场的预报误差。根据这两组预报误差的差异定义预报准确度F（通常为干总能量）。

3.计算预报准确度对预报场（分别来自背景场和分析场）的梯度，利用伴随模式WRFPLUS分别进行两次反向积分，得到预报误差对分析变量的敏感度。

4.预报误差对分析变量的敏感性结果作为输入场，进入WRFDA的伴随模式，计算预报误差对观测的敏感性，它涉及观测算子的伴随、观测误差协方差及Hessian矩阵的逆，在最小化过程中采取Lanczos迭代方法获得。


参考网页：

<http://www2.mmm.ucar.edu/wrf/users/wrfda/Tutorials/2012_July/docs/README_FSO_v3.3.pdf>

<http://www2.mmm.ucar.edu/wrf/users/wrfda/Tutorials/2014_July/docs/WRFDA_sensitivity.pdf>
