# Pull Request指南

### 简介

PR（Pull Request）是开发者进行代码协助的方式之一，是向开源项目贡献代码的主要方式。

* 开发者fork原项目，通过PR向项目提交代码修改。
* 代码维护者进行代码review，提出修改意见，并进行修改。
* 代码维护者approve之后，合并到代码主线。

一般而言，一个PR与一个issue相关联，Issue的主要有两种：（1）报告Bug（2）特性请求/增强建议。例如一个issue发现了一个BUG，然后你可以解决这个BUG，那么就可以创建一个关联这个issue的PR。所以一个PR可以去解决已经存在的issue，或者先创建issue，再未该issue提PR。

PR基本流程：

* fork项目。
* 选择贡献的目标分支（如`main`分支）。
* 在目标分支上，创建新分支。
* 编写代码 （在新分支上）。
* 编写测试（可选）。
* 本地测试，必须保证测试全部通过。
* 发起并提交PR。

### 编写代码

本地开发

```bash
# fork https://github.com/robomaster-oss/rmoss_core to https://github.com/abcd/rmoss_core
git clone https://github.com/abcd/rmoss_core
# 创建新分支
git checkout -b fix_abc
# 修改代码
# ....
# 提交代码
git add . 
git commit -s -m "fix some issues"
git pull orgin fix_abc
```

如果在修改过程中，项目的main分支已经更新，并且发生冲突，无法直接合并，则需要rebase同步一下目标分支。

```bash
# github (https://github.com/abcd/rmoss_core)页面，点击Fetch upstream
git pull orgin main
git rebase -i main
# 安装提示解决冲突
```

### 本地测试

运行测试

```bash
colcon test --package-select rmoss_base
```

- 一般包括两种测试：代码风格检查和代码单元测试（test目录中的测试代码）

查看测试结果

```bash
colcon test-result --verbose
```

### 发起pull request

* 在github页面上，将新分支`fix_abc`发起PR，如果发现测试不通过，需要进行相应修改。

参考资料

* https://blog.csdn.net/u011923621/article/details/106671789

