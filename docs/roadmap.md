# Roadmap

该页面包含RoboMasterOSS的未来工作计划，按照季度划分。目前rmoss项目还在开发中，仍可能进行代码重构，打破API/ABI，不推荐直接用于竞赛中。

### 2021 Q3 (7-9月) - 进行中

rmoss_core项目

- [x] 遵循ROS2代码风格（已重构所有API）。
- [x] 代码通过ament_lint自动测试。
- [x] rm_common和rm_task合并成rm_util （已重构）。
- [ ] rmoss_core模块文档完善(部分文档需移动至rmoss_tutorials中)
- [ ] 持续集成CI。

demo

- [ ] 基于navgiation2的自动导航demo

### 2021 Q4(10-12月)-计划中

rmoss_ign项目

* 完善模块相关文档。

* 完善rmua19_ignition_simulator功能，主要为裁判系统的开发。

demo

* 基于行为树的rmua19简化1v1竞赛demo