---
title: 被大家忽略的UIViewController两对API
date: 2018-05-01 00:00:00
author: 高老师很忙
layout: post
---
在某个页面被pop或者dismissViewController的时候，需要执行某个操作，大家会怎么做呢？swizzle dealloc方法？这样做是没有问题的；其实UIViewController为我们提供了两对API。
针对add childViewController和remove childViewController:

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/05/13-1.jpg?raw=true)

当然，Push和Pop也是适用的。

针对Present和Dismiss:

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/05/13-2.jpg?raw=true)

那前面提到的问题就可以在viewWillDisappear:或者viewDidDisappear:里面去判断self.beingDismissed或者self.movingFromParentViewController。

虽然是iOS5之后就有了，但被很多开发童鞋忽略和遗忘了，有应用到的场景，大家可以用起来哈！
