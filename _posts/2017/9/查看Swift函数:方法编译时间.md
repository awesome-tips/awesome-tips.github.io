---
title: 查看Swift函数/方法编译时间
date: 2017-09-01 00:00:00
author: 知识小集成员
cover: true
---

查看Swift函数/方法编译时间
----------

我们可以使用`-debug-time-function-bodies`标识来查看Swift中每个函数/方法的编译时间。添加方式与`-warn-long-expression-type-checking`一样，在`Other Swift Flags`添加中`-Xfrontend -debug-time-function-bodies`。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/09/28-1-1.png?raw=true)

这样，我们就可以在`Report navigator`的编译日志里面看到。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/09/27-1-2.png?raw=true)

另外，如果是用`xcodebuild`命令行，则可以如下将日志格式化输出到文本文件：

`xcodebuild -workspace App.xcworkspace -scheme App clean build OTHER_SWIFT_FLAGS="-Xfrontend -debug-time-function-bodies" | grep .[0-9]ms | grep -v ^0.[0-9]ms | sort -nr > log.txt`

知道每个函数/方法的编译时间后，就可以有针对性的做优化了。

参考

1. [Profiling your Swift compilation times](http://irace.me/swift-profiling)