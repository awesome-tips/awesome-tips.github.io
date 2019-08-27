---
title: -warn-long-expression-type-checking标识
date: 2017-09-01 00:00:00
author: 知识小集成员
layout: post
---


Swift的类型检测(`type-checker`)是编译时的一个性能瓶颈。

在Xcode 9中添加了一个编译器标识位`-warn-long-expression-type-checking`，可以对那些耗时长的类型检测操作给出警告。

我们可以在`Build Settings`->`Swift Compiler - Custom Flags`->`Other Swift Flags`中添加这个标识：`-Xfrontend -warn-long-expression-type-checking=<limit>`；其中`<limit>`是个阈值，以毫秒为单位，超出这个值的类型检测就给出警告。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/09/27-1-1.png?raw=true)

编译的警告信息如下图所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/09/27-1-2.png?raw=true)

获取警告信息之后，就可以根据需要去优化对应的操作。至于`<limit>`，可以凭经验设置，设置低了，可能会产生大量的警告信息。建议从高到低设置，先优化耗时高的。另外，建议只在`DEBUG`模式下开启。

另外，在Xcode 9之前可以使用`-warn-long-function-bodies`标识(Xcode 9仍然保留)，这个是警告哪个方法的类型检测超过阈值。可以尝试一下。

参考

1. [Measuring Swift compile times in Xcode 9](https://www.jessesquires.com/blog/measuring-compile-times-xcode9/)
