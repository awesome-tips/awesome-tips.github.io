---
title: 通过导入DSYM使用Instruments做性能分析
date: 2017-11-01 00:00:00
author: Vong_HUST
cover: true
---

通过导入DSYM使用Instruments做性能分析
----------

**作者**: [Vong_HUST](https://weibo.com/VongLo)

通常情况下，使用 `Instruments` 做性能分析，看调用栈时，是能够直接看到对应方法调用堆栈的，而不是一串的地址，但这个前提是 Xcode 用编译过这个应用。如果是用同事或者打包服务器上的安装包做性能分析时，就无法看到对应的方法调用堆栈信息了，只能看到一串地址。这个时候可以通过导入 `dSYM` 的方式来查看对应的方法调用堆栈，方式如下（见图）：打开 `Instruments` -> `运行一遍你的应用` -> `停止` -> `File` -> `Symbols` -> `dSYM Path : Locate`即可。如下图所示：

![图一](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/4-1.JPG?raw=true)

但是有些时候可能应用中包含 `extension`，则直接 `locate` 会提示无法定位到 dSYM 文件

> The specified path didn't locate a dSYM for any of the selected libraries.

这个时候需要把你的 `dSYM.zip` 解压，右键显示其内容将对应的 `.app.dSYM` 拷出，然后 `locate` 到这个拷出的 `dSYM` 文件即可或者按照下图操作也是可行的。具体流程见图：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/4-2.GIF?raw=true)