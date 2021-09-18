# RMOSS项目规范(暂定)

基于RMOSS开发项目，项目工程结构以ROS2项目工程为基础，本质上构建一个ROS2 package。

### 1.代码风格规范

采用[ROS2代码规范](https://docs.ros.org/en/foxy/Contributing/Code-Style-Language-Versions.html).

C++:

* 文件命名,变量命名,函数命名采用`snake_case`(下划线)方式.
* 类,结构体命名采用`CamelCase`(大驼峰)方式.
* 枚举变量推荐采用`CamelCase`(大驼峰)方式.

> 更多内容查看ROS2代码规范文档


### 2.项目文件结构（File Structure）

以rm_exmaple项目为例

```bash
rm_exmaple
├── include
│   └── rm_exmaple # 主要代码include目录
├── src            # 主要代码src目录
├── rm_exmaple     # 若该包作为python项目时，python文件存放目录
├── launch         # launch启动文件目录
├── scripts        # python，bash等脚本存放目录
├── config         # 配置目录，如ROS参数yaml文件
├── resource       # 资源目录，如图片，模型等文件
├── test           # 测试目录，存放测试代码
├── doc            # 文档目录
├── CMakeLists.txt
├── package.xml
└── README.md
```

* 参考了[ROS2 package layout](https://docs.ros.org/en/foxy/Contributing/Developer-Guide.html#package-layout)

### 3.文件头注释模板

C++:

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