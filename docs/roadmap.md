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

- [x] 项目结构调整，保持与rmoss_core风格一致性（尽可能遵守ROS2风格）。
- [ ] 采用ROS2代码风格，代码通过ament_lint自动测试。
- [ ] 增加持续集成CI。
- [ ] SDF模型改用[xmacro](https://github.com/gezp/xmacro)宏编写，并规范化模块化SDF建模。
- [ ] 在rmua19_ignition_simulato中, 在launch中动态解析模型（model.sdf.xmacro）
- [ ] 裁判系统Ignition Gazebo插件：一般灯条指示器插件，支持动态变换颜色。
- [ ] 裁判系统Ignition Gazebo插件：装甲板灯条，支持动态变换颜色。

文档

- [ ] 整理rmoss_core项目文档


demo

- [ ] 基于行为树的rmua19简化1v1竞赛demo