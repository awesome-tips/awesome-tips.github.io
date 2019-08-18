---
title: Extract Function/Extract Method
date: 2017-10-01 00:00:00
author: 知识小集成员
cover: true
---

Extract Function/Extract Method
----------

当我们写代码写得飞起的时候，很可能在一个函数/方法里面堆积大量代码。当然，从美学的角度来讲，我们更希望写一些小而职责单一的函数/方法，所以这时候可以考虑重构。

Xcode为我们提供了一个简便的方法：`Extract Function/Extract Method`，来将代码提取成一个函数/方法。

具体操作是：首先选中要提取的代码，然后右键点击出现菜单，选择`Refactor` -> `Extract Function/Extract Method`，如下图所示：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/10/26-1-1.jpg?raw=true)

可以看到选中的代码被提取成一个单独的方法，我们可以给方法命个名，如下图所示：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/10/26-1-2.jpg?raw=true)

而且这个操作可以识别新方法需要哪些参数，是不是很方便？