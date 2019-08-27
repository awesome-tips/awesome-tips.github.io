---
title: Swift Compile Warning
date: 2017-02-01 00:00:00
author: 知识小集成员
layout: post
---


在`Swift`中，我们通常会用`FIXME/TODO/MARK`来做一些注释标注，这些标注在代码的`dropdown box`中能显示出来，如下图所示：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/02/23-1-1.png?raw=true)

不过，如果我们标注的是一些警告或错误信息的话，这用方式通常比较容易遗忘，不像`Objective-C`中的`#warning`一样，在编译时能被检测出来。

如果我们想在编译时让编译器高亮提示，即如下图所示，

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/02/23-1-2.png?raw=true)

则可以在`Build Phases`中添加一个`Run Script`，脚本代码如下图所示：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/02/23-1-3.png?raw=true)

可以看到，我们还能添加自定义的注释标签，如`WARNING/ERROR`。

参考

1. [HOW TO HIGHLIGHT YOUR TODOS, FIXMES, & ERRORS IN XCODE](https://krakendev.io/blog/generating-warnings-in-xcode)
