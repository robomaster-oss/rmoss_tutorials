# RMOSS项目规范(暂定)

基于RMOSS开发项目，本质上构建一个ROS2 package，所以项目工程结构以ROS2项目工程为基础。

* 工程项目目录结构完全与ROS2项目一致。
* CMakeLists文件编写与ROS2项目一致，并提供模板，方便自行编写。

### 项目工程目录结构

以rm_exmaple项目为例

```bash
rm_exmaple
├── include
│   └── rm_exmaple #主要代码include目录
├── src     #主要代码src目录
├── nodes   #ros node目录，程序main函数入口
├── launch  #launch启动文件目录
├── scripts #python等脚本存放目录
├── doc　　　#文档目录
├── CMakeLists.txt
├── package.xml
└── README.md
```

### CMakeLists规范

以下为rm_task的CMakeLists.txt的文件例子

```bash
cmake_minimum_required(VERSION 3.5)

project(rm_task)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(ament_index_cpp REQUIRED)
find_package(rclcpp REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(image_transport REQUIRED)
find_package(cv_bridge REQUIRED)
find_package(OpenCV REQUIRED)

include_directories(include)

# rm_task lib
AUX_SOURCE_DIRECTORY(${PROJECT_SOURCE_DIR}/src DIR_SRCS)
add_library(${PROJECT_NAME} ${DIR_SRCS})

ament_target_dependencies(${PROJECT_NAME}
 rclcpp 
 sensor_msgs
 image_transport 
 cv_bridge
 OpenCV
)

#task_show_image example
add_executable(task_show_image nodes/task_show_image.cpp)
target_link_libraries(task_show_image ${PROJECT_NAME})

# Install launch directories
install(DIRECTORY launch
  DESTINATION share/${PROJECT_NAME}
)

# Install include directories
install(DIRECTORY include/
  DESTINATION include
)
# Install libraries
install(TARGETS ${PROJECT_NAME}
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  RUNTIME DESTINATION bin
)
# Install executables
install(TARGETS task_show_image
  DESTINATION lib/${PROJECT_NAME}
)

#export include
ament_export_include_directories(include)
#export libraries
ament_export_libraries(${PROJECT_NAME})
#export dependency
ament_export_dependencies(rclcpp)
ament_export_dependencies(sensor_msgs)
ament_export_dependencies(image_transport)
ament_export_dependencies(cv_bridge)
ament_export_dependencies(OpenCV)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
```



### README规范

* 略