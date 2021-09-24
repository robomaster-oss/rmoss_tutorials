# RMOSS项目开发指南

### 1.设计原则

rmoss模块设计主要遵循以下两个原则

* 分层设计
  * 算法层：与ROS无关的代码部分，与ROS解耦。
  * ROS层：顶层设计，调用算法层，以及通过ROS通信机制，与其它模块建立连接，实现功能。
* 动态库
  * rmoss模块都会编译成动态库，即模块可以作为独立节点运行，也可以作为库被依赖。

> 动态库生成可参考其他RMOSS项目的CMakefile.txt.

### 2. 二次开发例子

rmoss_cam模块

* 定义相机设备接口`CamInterface`，实现了虚拟相机与usb相机的通用ROS节点实现，支持自定义设备实现。

rmoss_projectile_motion模块

* 提供了重力补偿工具类`GimbalTransformTool`，被rmoss_auto_aim和rmoss_power_rune2019使用。