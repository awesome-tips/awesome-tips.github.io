---
title: 利用Attach方式调试推送、Today、3DTouch
date: 2017-11-01 00:00:00
author: 高老师很忙
cover: true
---

利用Attach方式调试推送、Today、3DTouch
----------

**作者**: [高老师很忙](https://weibo.com/517082456)

在调试推送、`Today`、`3DTouch` 等唤起测试 App 的时候（此时App未启动），我们通常 `Run` 的方式是不行的，因为 `Run` 后 `App` 就启动了，不满足调试环境。`Xcode` 为我们提供了 `Attach` 的方式进行调试，使用起来也是超简单的。操作方式如下：

前提：已经加了断点（比如 `application: didFinishLaunchingWithOptions:` 方法里加断点）

* `Attach` 之前需要把测试 `App` 的进程杀掉（如果不杀掉进程，这种方式是无法断点调试的）；

* 选择你要 `Attach` 的测试 `App` ,有两种方式：在 `Debug` 下拉菜单下面有 `Attach to Process` 选项（直接选择你的测试 `App`，如图1）和 `Attach to Process by PID or Name` 选项（输入名称，如图2）；

![15-1](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/15-1.jpg?raw=true)

![15-2](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/15-2.jpg?raw=true)

* 用推送、`Today`、`3DTouch` 等方式唤起，就大功告成了，如下图所示

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/15-2.jpg?raw=true)