# ROS2学习资源  

### 简介

Robot Operating System (ROS)是一个构建机器人应用的框架，包含一系列软件库和开发工具。ROS2是第一代ROS的重构，改进了许多ROS1的缺点，RMOSS项目基于ROS2实现，主要用到了ROS2的通信机制，需要熟悉ROS2中topic，service等几种通信方式。

参考资料

* [ROS2 官方文档](https://docs.ros.org/en/galactic/index.html ) : 建议参考官网进行基础学习，只需要学习tutorial中的Beginner部分即可。
* [2021年ROS暑期学校ROS2讲座 (B站)](https://www.bilibili.com/video/BV1PQ4y1y7F2)：胡春旭老师的讲座，非常棒的ROS2入门讲座，介绍了很多基础概念。

### Parameter机制

Parameter机制是一种键对值存储方式，采用ros service方式存储与查询，为node提供参数服务。所有的参数都是可以被动态的重新配置。每个节点都维护一个参数服务，也就是说每一个节点的参数都是独立互不影响的，可以通过`ros param`进行查看设置，也可通过service的方式进行更新。

* 支持参数类型：integers, floats, booleans, strings and lists(array)。
* launch文件可采用yaml文件方式加载参数，参数文件应该存放在`config`目录下。

参考资料

- [Understanding ROS2 Parameters](https://index.ros.org/doc/ros2/Tutorials/Parameters/Understanding-ROS2-Parameters/)
- [Using Parameters In CPP](https://index.ros.org/doc/ros2/Tutorials/Using-Parameters-In-A-Class-CPP/)
- [Using Parameters In Python](https://index.ros.org/doc/ros2/Tutorials/Using-Parameters-In-A-Class-Python/)
- [ros2-global-parameters](https://roboticsbackend.com/ros2-global-parameters/)
- ROS2 Design：[ros parameters](https://design.ros2.org/articles/ros_parameters.html)

### DDS机制

DDS (Data Distribution Service)，即数据分发服务，是一种专门为实时系统设计的数据分发，订阅标准。ROS2通信基于DDS实现，因此ROS2也继承了DDS的优点。

* 分布式系统：ROS2是一个分布式系统，这正得益于DDS的自动Discovery机制来实现的。（相比于ROS1，没有了master节点）
* QoS通信配置：更灵活的通信机制，满足不同场景下的需求，例如，对于传感器消息，要求实时性高，允许部分丢包，而对于控制指令消息，要求可靠性高，允许消息延迟，这时候我们可以通过配置消息QoS满足我们的需求。

参考资料

* [2021年ROS暑期学校DDS讲座(B站)](https://www.bilibili.com/video/BV1sU4y1P7yn)：非常好的DDS中文介绍讲座。
* [About Quality of Service settings](https://docs.ros.org/en/galactic/Concepts/About-Quality-of-Service-Settings.html): 官方QoS配置种类介绍。

### Composition机制

ROS Composition机制指的是将多个Node组合运行在一个进程中。ROS2是一个分布式系统，一般情况下，我们每一个Node都会运行一个进程（也就是`ros run`），将多个Node运行在一个进程中，可以提高程序性能，减小系统开销，如降低CPU和内存消耗，减小通信延迟（考虑多进程模型 vs 多线程模型），ROS Composition机制有如下两种方式：

* 手动合成（Manual Composition）：在编译期间合成，无需对Node做任何修改，原生支持。
* 动态合成（Dynamic Composition）：在运行时合成，需要先将Node注册成`component`，然后使用`rclcpp_components`在进行动态加载。

> Composition模式下，ROS2通信会进行一些优化，与采用的具体DDS厂商有关，如有些DDS会采用共享内存进行通信优化。

Manual Composition例子

```c++
// 可以直接在main()中创建两个Node。
auto node1 = std::make_shared<Task1Node>();
auto node2 = std::make_shared<Task2Node>();
// 将两个Node加入executor中
rclcpp::executors::SingleThreadedExecutor executor;
executor.add_node(node1->get_node_base_interface());
executor.add_node(node2->get_node_base_interface());
// 运行executor
executor.spin();
```

Dynamic Composition例子

```bash
# 需要先composition::Talker 和 composition::Listener 注册为component
# composition::Talker例子：https://github.com/ros2/demos/blob/foxy/composition/src/talker_component.cpp
# 运行容器
ros2 run rclcpp_components component_container
# 将component加载到容器中
ros2 component load /ComponentManager composition composition::Talker
ros2 component load /ComponentManager composition composition::Listener
```

Composition中的高效进程内通信（intra-process communication）

* 在Composition模式下，不同节点可以运行在一个进程中，而DDS是一个进程间通信模型，虽然会进行相应优化，但仍会有额外开销。ROS2提供了一套不使用DDS，直接进行进程内通信的高效方式，甚至支持zero copy通信（具有局限性，只限于点对点模式下）。
* 该方式还在实验中，不一定获得性能最优，需谨慎使用。

```c++
// 通过配置Node option实现intra-process communication (只用于Composition模式下)
auto node1 = std::make_shared<rclcpp::Node>("test1",rclcpp::NodeOptions().use_intra_process_comms(true));
auto node2 = std::make_shared<rclcpp::Node>("test2",rclcpp::NodeOptions().use_intra_process_comms(true));
```

参考资料

* https://docs.ros.org/en/foxy/Tutorials/Composition.html ： Composition方式
* https://docs.ros.org/en/galactic/Tutorials/Intra-Process-Communication.html： 进程内通信方式

