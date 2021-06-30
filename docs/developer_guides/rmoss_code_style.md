# RMOSS 代码规范

### 代码风格规范（C++）

* 建议采用Google C++代码风格规范，以下为补充。

#### 文件命名规范

- 目录与文件命名均 __下划线式书写__，即采用小写，单词之间采用下划线"_"作为分割。
- 命名必须采用英文，描述核心功能，建议1-3个单词为宜，为避免命名过长，适当采用缩写形式。
- xxx.h/cpp一般成对存在，并分别位于include与src中。

#### 代码命名规范

__类/结构体/枚举类型命名__

- __大驼峰式__ 书写，如TestRobot
- 可选：结构体以"\_t"结尾，枚举变量以"\_e"

__变量命名__

- __下划线式书写__，如test_vaule。
- 全局变量或者类成员变量，以下划线"\_"结尾,如mem\_vaule\_。

__函数命名__

- __小驼峰式__ 书写，如testFunction
- 建议采用动宾结构词组

#### 注释规范

__文件头注释模板__

```c++
/*******************************************************************************
 *  Copyright (c) 2020 robomaster-oss, All rights reserved.
 *
 *  This program is free software: you can redistribute it and/or modify it 
 *  under the terms of the MIT License, See the MIT License for more details.
 *
 *  You should have received a copy of the MIT License along with this program.
 *  If not, see <https://opensource.org/licenses/MIT/>.
 *
 ******************************************************************************/
```

__函数及变量注释规范__

- 无





