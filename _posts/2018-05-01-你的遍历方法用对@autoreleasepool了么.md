---
title: 你的遍历方法用对@autoreleasepool了么
date: 2018-05-01 00:00:00
author: 高老师很忙
layout: post
---
在每次遍历的时候生成了很多占内存大的对象，如果交于默认的autoreleasepool去管理生命周期，会有因为内存飙升产生crash的风险，这个时候我们就需要手动控制这些对象的生命周期。也就是需要在适当的位置上去使用@autoreleasepool()。

系统为我们提供了很多的遍历方法，比如说**for循环**、**for-in**、**enumerateObjectsWithOptions:**、**dispatch_apply**等方法，那有的同学就说都加上吧，就出现了下面这段代码：

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/05/3-1.jpg?raw=true)

虽然说这样写也没什么异常，但是这里真的有必要加么？其实快速遍历这几个方法系统自动为我们添加了autoreleasepool方法，从文档里可以看到蛛丝马迹：

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/05/3-2.jpg?raw=true)

不过，其他方法都需要加上@autoreleasepool()哈！

