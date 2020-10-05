# RMOSS项目开发指南

### 1.设计原则

rmoss模块设计主要遵循以下两个原则

* 分层设计

  * 算法层：与ROS无关的代码部分，与ROS解耦和。
  * ROS层：顶层设计，调用算法层，以及通过ROS通信机制，与其它模块建立连接，实现功能。
* 动态库
  * rmoss模块都会编译成动态库，即模块可以作为独立节点运行，也可以作为库被依赖。

> 动态库生成可参考其他RMOSS项目的CMakefile.txt.

### 2..二次开发例子

基于rm_base的standard_robot_base模块

* 复用rm_base中的serialport_dev数据传输类和fixed_packet数据封装类，大大降低了工作量。

task_image_related模块

* 继承task_image_related中的基类，无需关心ROS接收图像层面，只需要实现`taskImageProcess`函数即可实现图像处理任务。
* 被task_auto_aim和task_power_rune2019应用。

rm_tool模块

* 提供了一些基本类，被其它模块广泛应用，如单目测量封装函数（PnP）等等
* 被task_auto_aim和task_power_rune2019等模块应用。

rm_projectile_motion模块

* 提供了重力补偿工具类，被task_auto_aim和task_power_rune2019应用。