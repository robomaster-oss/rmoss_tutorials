# 1.相机模块的使用

### RoboMaster中的视觉

在RoboMaster比赛中，相机就是机器人的眼睛，是机器人获取外界信息的重要途经，通过计算机视觉处理，从而可以做出一些复杂的行为，如备受强队青睐的杀手锏功能能量机关，或者开挂般的自瞄功能。除此之外，比赛中越来越重视视觉的应用，如RoboMaster2020赛季，雷达站等规则，使得视觉应用具有非常大潜力。

在robomaster_os中，提供了rm_cam模块，定义了一套通用相机API，实现了普通usb相机，图片模拟相机，视频模拟相机三种相机采集功能，并支持自定义工业相机扩展。

> 相机是一种非常重要的光学传感器，其种类繁多，所以相机选型也是一种学问，从百元价位的普通OV系列相机到上万的工业相机，以及不同焦距镜头的选型，这都需要针对比赛进行专门选择，这里不再详述，可参考资料[RM相机选型指南](Developers_Guide/camera_selection.md)

本文涉及模块：

- rm_cam

### rm_cam模块

#### usb相机：

运行：

```bash
ros2 launch rm_cam usb_cam.launch.py  #使用/dev/video0
```

launch文件说明：

* 略

#### 图片模拟相机：

运行：

```bash
ros2 launch rm_cam sim_cam_image.launch.py  #使用默认图片test.png
```

launch文件说明：

* 略

#### 视频模拟相机：

launch文件说明：

* 略



>  更多内容参考github: [rm_cam][1]



[1]: https://github.com/robomaster-oss/rmoss_core/tree/main/rm_cam

 