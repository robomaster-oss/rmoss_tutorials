# RMOSS项目规范(暂定)

基于RMOSS开发项目，本质上构建一个ROS2 package，所以项目工程结构以ROS2项目工程为基础。

* 工程项目目录结构完全与ROS2项目一致。
* ROS2 package具有CMake package和Python package两种，这里只详细介绍CMake package。

### 1.CMake package

#### 1.1 项目文件结构（File Structure）

以rm_exmaple项目为例

```bash
rm_exmaple
├── include
│   └── rm_exmaple #主要代码include目录
├── src     #主要代码src目录
├── nodes   #ros node目录，程序main函数入口
├── launch  #launch启动文件目录
├── scripts #python，bash等脚本存放目录
├── doc　　　#文档目录
├── CMakeLists.txt
├── package.xml
└── README.md
```

#### 1.2 CMakeLists使用例子

以下为rm_base的CMakeLists.txt的文件例子

```bash
cmake_minimum_required(VERSION 3.5)
project(rm_base)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

#find package
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rm_interfaces REQUIRED)
find_package(geometry_msgs REQUIRED)

#include
include_directories(include)

#create rm_base lib
AUX_SOURCE_DIRECTORY(${PROJECT_SOURCE_DIR}/src DIR_SRCS)
add_library(${PROJECT_NAME} ${DIR_SRCS})
ament_target_dependencies(${PROJECT_NAME}
    rclcpp 
    rm_interfaces
    geometry_msgs
)
#create robot_base_example node
add_executable(robot_base_example nodes/robot_base_example_node.cpp)
target_link_libraries(robot_base_example ${PROJECT_NAME})

# Install include directories
install(DIRECTORY include/
    DESTINATION include
)
# Install libraries
install(TARGETS ${PROJECT_NAME}
    EXPORT ${PROJECT_NAME}
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include
)
# Install executable nodes
install(TARGETS robot_base_example
  DESTINATION lib/${PROJECT_NAME}
)
# Install executable scripts
install(PROGRAMS 
        scripts/chassis_control_test.py 
        scripts/gimbal_control_test.py 
    DESTINATION lib/${PROJECT_NAME})

#export rm_base lib
ament_export_targets(${PROJECT_NAME} HAS_LIBRARY_TARGET)
ament_export_dependencies(rclcpp)
ament_export_dependencies(rm_interfaces)
ament_export_dependencies(geometry_msgs)

#test
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
```

#### 1.3 CMakeLists 使用说明

##### ament_package

```bash
ament_package()
```

- 每个package的CMakeLists.txt必须包含。
- 目的：安装package.xml，注册package到ament index，安装config files for CMake（即可以被find_package找到）。

> Tip：ament_package()放在CMakeLists.txt最后即可

##### Compiler Options

```makefile
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()
target_compile_options(my_target PRIVATE -Wall)
```

##### Include

```makefile
#methods1:为整个package添加include目录
include_directories(include)
#methods2:只为目标添加include目录
target_include_directories(my_target
  PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>)
```

##### Dependency

```makefile
#methods1:将会包含必要的头文件以及依赖库（推荐方法）
find_package(Eigen3 REQUIRED)
ament_target_dependencies(my_target Eigen3)
#methods2:CMake经典方式
find_package(Eigen3 REQUIRED)
target_link_libraries(my_target Eigen3::Eigen)
```

##### Install

```bash
# 安装include目录
install(DIRECTORY include/
  DESTINATION include
)
# 安装相关资源目录，如launch等
install(DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)
# 安装node可执行文件
install(
  TARGETS [node-names]
  DESTINATION lib/${PROJECT_NAME}
)
#其他可执行文件安装（python脚本，bash脚本等）
install(PROGRAMS scripts/my_executable DESTINATION lib/${PROJECT_NAME})
```

注意，python或bash脚本请在第一行加入解释器注释，如下：

```makefile
#!/bin/bash           #对于bash脚本
#!/usr/bin/python3    #针对于python3脚本
```

#####  构建Library

```makefile
#library
add_library(my_library SHARED src/export_my_library.cpp)
#export
ament_export_targets(export_my_library HAS_LIBRARY_TARGET)
ament_export_dependencies(some_dependency)
#安装library 
install(
  TARGETS my_library
  EXPORT export_my_library
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  RUNTIME DESTINATION bin
  INCLUDES DESTINATION include
)
```

- ament_export_targets ：为Cmake导出target，这样就可以使用target_link_libraries链接该库。
- ament_export_dependencies：导出该library的下游依赖

多余的两个方法

```makefile
#等价于install()中的INCLUDES DESTINATION
ament_export_include_directories(include)
#等价于ament_export_targets()中的HAS_LIBRARY_TARGET参数
ament_export_libraries(my_library)
```

##### environment hook

```makefile
ament_environment_hooks("${CMAKE_CURRENT_SOURCE_DIR}/env-hooks/${PROJECT_NAME}.sh.in")
ament_environment_hooks("${CMAKE_CURRENT_SOURCE_DIR}/env-hooks/${PROJECT_NAME}.dsv.in")
```

- 待续

### 2.Python Package

* 略

### 3.README规范

* 略