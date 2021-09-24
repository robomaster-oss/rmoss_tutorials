#  RoboMasterOSS 项目概览

### [rmoss_core][1]

|          模块          |                           功能说明                           |
| :--------------------: | :----------------------------------------------------------: |
|        `rmoss_util`       | 公共工具包: 包含调试,图像处理,ROS公共封装工具等公共基础工具。   |
|     `rmoss_interfaces`    | ROS2 interface包：包含RM相关msg，srv，action定义文件        |
|        `rmoss_base`       | 基本通信工具包：提供单板计算机(SBC)与嵌入式系统(MCU)通信等相关工具。 |
|        `rmoss_cam`        | 相机工具包：提供相机的ROS封装工具，实现usb相机，以及图片视频虚拟相机。   |
| `rmoss_projectile_motion` | 弹道运动工具包: 求解弹道逆运动学，由目标位置计算云台仰角  |

* `rmoss_interfaces` : 单独仓库，作为各个ROS模块的桥梁。

### [rmoss_contrib][2]

|        模块         |                 功能说明                 |
| :-----------------: | :--------------------------------------: |
|    `rmoss_auto_aim`    |   RoboMaster基础自瞄任务的简单算法实现   |
| `rmoss_power_rune2019` | RoboMaster2019能量机关任务的简单算法实现 |

### [rmoss_ign][3]

|            模块             |                           功能说明                           |
| :-------------------------: | :----------------------------------------------------------: |
|     `rmoss_ign_plugins`     |        RoboMaster相关Ignition Gazebo Simulator插件。         |
|      `rmoss_ign_base`       |   RoboMaster基本机器人Ignition-ROS通信桥接（仿真MCU部分功能）    |
|    `rmoss_ign_resources`    | RoboMaster相关核心SDF模型资源，官方机器人模型和核心场地模型。 |


* `rmoss_ign_resources` : 单独成库, 主要包含资源文件。



[1]: https://github.com/robomaster-oss/rmoss_core	"rmoss_core"
[2]: https://github.com/robomaster-oss/rmoss_contrib	"rmoss_contrib"
[3]: https://github.com/robomaster-oss/rmoss_ign	"rmoss_ign"