## RoboMaster OSS项目

###  1.基础项目

RoboMasterOSS中的基础项目，

* **[rmoss_core项目][1]** ：公共软件栈，包含的基础功能技术栈和调试功能技术栈。
* **[rmoss_contrib项目][2]** ：功能软件栈，提供各种具体算法的功能包，原则上不相互依赖，依赖于rmoss_core

### 2.RoboMasterOSS 项目概览

**[rmoss_core][1]:** （6 packages）

|          模块          |                           功能概况                           |
| :--------------------: | :----------------------------------------------------------: |
|       `rm_base`        | 基本通信模块，实现与底层通信，可以控制底层，并从底层获得相关数据。 |
|        `rm_cam`        | 相机模块，实现usb相机驱动，以及图片视频模拟成相机（方便测试）。 |
|       `rm_msgs`        |                   基本自定义ROS2 message。                   |
|       `rm_tool`        |            基本工具包，包括调试，图像处理等工具。            |
| `rm_projectile_motion` |   子弹弹道修正工具，可以修正子弹飞行过程中重力因素的影响。   |
|       `rm_task`        |          任务相关工具，提供了一个图像相关任务基类。          |

**[rmoss_contrib][2]:** （2 packages）开发中

|        模块         |                          功能概况                          |
| :-----------------: | :--------------------------------------------------------: |
|    `rm_auto_aim`    |          自瞄任务，实现了RoboMaster比赛自瞄功能。          |
| `rm_power_rune2019` | 能量机关功能任务，实现了RoboMaster2019赛级的能量机关功能。 |



[1]: https://github.com/robomaster-oss/rmoss_core	"rmoss_core"
[2]: https://github.com/robomaster-oss/rmoss_contrib	"rmoss_contrib"
