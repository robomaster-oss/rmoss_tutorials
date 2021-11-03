# RMOSS项目规范

基于RMOSS开发项目，项目工程结构以ROS2项目工程为基础，本质上构建一个ROS2 package。

### 1.代码风格规范 (Code Style)

采用[ROS2代码规范](https://docs.ros.org/en/foxy/Contributing/Code-Style-Language-Versions.html).

C++:

* 文件命名,变量命名,函数命名采用`snake_case`(下划线)方式.
* 类,结构体命名采用`CamelCase`(大驼峰)方式.

c++其他约定

* 尽可能的采用智能指针，避免原始指针与new的进行手动内存管理。

> 更多内容查看ROS2代码规范文档


### 2.项目文件结构（File Structure）

以rmoss_exmaple项目为例

```python
rmoss_exmaple
├── include
│   └── rmoss_exmaple # 主要代码include目录
├── src               # 主要代码src目录
├── rmoss_exmaple     # 若该包作为python项目时，python文件存放目录
├── launch            # launch启动文件目录
├── scripts           # python，bash等脚本存放目录
├── config            # 配置目录，如ROS参数yaml文件
├── resource          # 资源目录，如图片，模型等文件
├── test              # 测试目录，存放测试代码
├── doc               # 文档目录
├── CMakeLists.txt
├── package.xml
└── README.md
``` 

* 参考了[ROS2 package layout](https://docs.ros.org/en/foxy/Contributing/Developer-Guide.html#package-layout)
* main函数入口源文件，建议使用`_main`后缀

### 3.开发约定规范（Conventions）

坐标系及基本单位遵守ROS约定规范

* 坐标系规范以及基本单位标准: [REP 103](https://www.ros.org/reps/rep-0103.html). 
* 移动机器人参考系规范：[REP 105](https://www.ros.org/reps/rep-0105.html).

> 坐标系方向约定补充说明
>
> * 刚体坐标系(机器人坐标系)：前方x，左边为y，上方为z. 一般情况，对于描述机器人以及link之间的相对变化关系，都使用该坐标系方向。
> * 相机坐标系：前方z，右边为x，下方为y. 只有在有2D图像计算出相对相机的3D信息才使用相机坐标系，相机参考系（frame）应该使用额外的后缀`_optical`.
>
> 在描述相机link与其他link坐标变换时，依然使用刚体坐标系，在使用tf2构建坐标变换树时，会存在`camera`和`camera_optical`两个frame，`camera`对应相机link，`camera_optical`对应相机坐标系（无实体）。

云台姿态角方向约定

* 在RMOSS中，云台采用刚体坐标系方向约定，因此对于yaw角旋转，向左为正，对于pitch角旋转，向下为正。（无论云台正装，倒装，都采用该方向约定）

> Tip：对于[DJI云台控制](https://developer.dji.com/cn/payload-sdk/documentation/tutorial/gimbal-control.html)，云台姿态角即使用大地坐标系（NED，北东地坐标系）描述云台上负载设备的角度。RMOSS采用的云台约定与该约定不同。

### 4.文件头注释模板

c++

```c++
// Copyright 2021 RoboMaster-OSS
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//     http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.
```

### 5.测试

运行测试
```bash
colcon test --package-select rmoss_base
```
* 一般包括两种测试：代码风格检查和代码单元测试（test目录中的测试代码）

查看测试结果
```bash
colcon test-result --verbose
```

代码自动格式化（reformat）
```bash
# 只能解决部分格式问题，部分需要手动修正以通过test
ament_uncrustify --reformat .
```
