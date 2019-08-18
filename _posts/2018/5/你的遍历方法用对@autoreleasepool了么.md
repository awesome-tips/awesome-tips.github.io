---
title: 你的遍历方法用对@autoreleasepool了么
date: 2018-05-01 00:00:00
author: 高老师很忙
cover: true
---

你的遍历方法用对@autoreleasepool了么
----------
**作者**: [高老师很忙](https://weibo.com/517082456)

在每次遍历的时候生成了很多占内存大的对象，如果交于默认的autoreleasepool去管理生命周期，会有因为内存飙升产生crash的风险，这个时候我们就需要手动控制这些对象的生命周期。也就是需要在适当的位置上去使用@autoreleasepool()。

系统为我们提供了很多的遍历方法，比如说**for循环**、**for-in**、**enumerateObjectsWithOptions:**、**dispatch_apply**等方法，那有的同学就说都加上吧，就出现了下面这段代码：

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/05/3-1.jpg)

虽然说这样写也没什么异常，但是这里真的有必要加么？其实快速遍历这几个方法系统自动为我们添加了autoreleasepool方法，从文档里可以看到蛛丝马迹：

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/05/3-2.jpg)

不过，其他方法都需要加上@autoreleasepool()哈！

使用 YYFPSLabel 快速检测页面滑动的流畅度
--------
**作者**: [KANGZUBIN](https://weibo.com/kangzubin)

`FPS` (Frames Per Second) 是图像领域中的定义，表示每秒渲染帧数，通常用于衡量画面的流畅度，每秒帧数越多，则表示画面越流畅，`60fps` 最佳。

在 `iOS` 开发中，在复杂布局的列表页面，我们通常需要对列表的滑动进行性能优化，以保持页面流畅。对于保持流畅的优化技巧，可以参见 `@ibireme` 的这篇文章 **《iOS 保持界面流畅的技巧》** https://blog.ibireme.com/2015/11/12/smooth_user_interfaces_for_ios/，我们不再赘述。

这里主要介绍一下如何快速检测页面滑动的流畅度，即如何检测屏幕的 `FPS` ?

`Xcode` 的 `Instrument` 提供了相关的工具，详见 `Core Animation/GPU Driver/Time Profile` 等模块，但是使用起来还是比较繁琐，不直观。

在 **YYText** `https://github.com/ibireme/YYText) 的 [Demo](https://github.com/ibireme/YYText/tree/master/Demo/YYTextDemo` 中提供了一个 `YYFPSLabel`，它使用系统提供的 `CADisplayLink` 的 `timestamp` 属性，配合 `timer` 的执行次数计算得出 `FPS`，实现原理详见 `YYFPSLabel` 源码和这篇文章的介绍：`https://www.jianshu.com/p/878bfd38666d`

因此，我们可以在工程的 `DEBUG` 模式下，给 `KeyWindow` 添加一个 `YYFPSLabel`，如下：

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/05/4-1.png)

就可以在屏幕上实时看到 `FPS` 值了：

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/05/4-2.jpg)

另外，`FPS` 的值跟机器的处理器性能息息相关，不同的设备的表现往往都不同，因此我们只要能保证 `App` 在低端设备上运行的 `FPS` 为 `50+`，基本就可以认为是流畅的了。

Demo 地址：`https://github.com/kangzubin/XMNetworking/tree/master/Demo`