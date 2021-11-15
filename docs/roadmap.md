# Roadmap

该页面包含RoboMasterOSS的未来工作计划，按照季度划分。目前rmoss项目还在开发中，仍可能进行代码重构，打破API/ABI，不推荐直接用于竞赛中。

### 2021 Q3 (7-9月) - 已完成

rmoss_core项目

- [x] 遵循ROS2代码风格（已重构所有API）
- [x] 代码通过ament_lint自动测试
- [x] rm_common和rm_task合并成rm_util （已重构）
- [x] rmoss_core模块文档整理
- [x] 增加持续集成CI
- [X] 增加单元测试
- [ ] ~~规范化代码注释~~

demo

- [x] 基于navgiation2的自动导航demo : https://github.com/gezp/rm_navigation2_demos

### 2021 Q4(10-12月)-进行中


rmoss_ign项目

- [X] 项目结构调整，保持与rmoss_core风格一致性（尽可能遵守ROS2风格）。
- [X] 增加持续集成CI，代码通过ament_lint自动测试。
- [X] SDF模型改用`xmacro`宏编写，并规范化模块化SDF建模。
- [X] 新增裁判系统Ignition Gazebo插件：灯条控制器（位于`rmoss_ign_plugins`）。
- [X] 针对rm22赛季，更新`rmoss_ign_resource`裁判系统SDF模型，支持全部类型装甲板贴纸，新增图传模型，42mm枪管测速模型。
- [X] 新增`rmoss_ign_cam`模块，对应rmoss_cam模块，实现仿真与真实机器人无缝切换。
- [X] 完善`rmoss_ign_base`模块，进行Node封装，支持云台相对角，绝对角控制（使用GimbalCmd msg），支持底盘速度控制，底盘跟随控制（使用ChassisCmd msg）。
- [ ] `rmua19_ignition_simulator`：支持键鼠的web玩家控制接口。
- [ ] `rmuc21_ignition_simulator`：能量机关大风车模型与控制器。
- [X] `rmua22_ignition_simulator`：比赛场地模型搭建。

rmoss_tutorial

- [X] rmoss design文档
- [X] ROS2入门指南
- [X] rmoss_ign 建模指南

demo

- [ ] 在Ignition Gazebo仿真环境中实现RoboMaster自瞄功能。