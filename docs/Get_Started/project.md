###  1.基础项目

RoboMasterOSS中的基础项目，

* **[rmoss_core项目][1]** ：公共软件栈，基础功能包。
* **[rmoss_contrib项目][2]** ：功能软件栈，任务级的功能包。

### 2.RoboMasterOSS 项目概览

**[rmoss_core][1]:** （6 packages）

|          模块          |                          功能说明                           |
| :--------------------: | :---------------------------------------------------------: |
|      `rm_common`       |        公共工具包，包括调试，图像处理等公共基础工具         |
|    `rm_interfaces`     | RM相关的ROS interface包，包含相关msg，srv，action定义文件。 |
|       `rm_base`        |  基本通信工具包，包含PC与嵌入式系统（stm32）通信相关工具。  |
|        `rm_cam`        |     相机工具包，实现usb相机驱动，以及图片视频虚拟相机。     |
|       `rm_task`        |         任务相关工具，提供了一个图像相关任务基类。          |
| `rm_projectile_motion` | 通用弹道模型工具包，可以修正子弹飞行过程中重力因素的影响。  |

**[rmoss_contrib][2]:** （2 packages）

|        模块         |                 功能说明                 |
| :-----------------: | :--------------------------------------: |
|    `rm_auto_aim`    |   RoboMaster基础自瞄任务的简单算法实现   |
| `rm_power_rune2019` | RoboMaster2019能量机关任务的简单算法实现 |





[1]: https://github.com/robomaster-oss/rmoss_core	"rmoss_core"
[2]: https://github.com/robomaster-oss/rmoss_contrib	"rmoss_contrib"
