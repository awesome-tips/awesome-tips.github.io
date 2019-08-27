---
title: iOS中NSArray/NSSet的一些巧妙用法
date: 2018-01-01 00:00:00
author: Vong_HUST
layout: post
---


最近用到很多操作集合类型的方法，这里总结分享一下，也欢迎大家一起补充。

* 假设我们已经有一个 `NSArray<Model *>` 类型的数组，但是我们想把这个数组中的 `Model` 的某个属性取出组成一个新的数组，一般情况下可能是直接去遍历，但是 `NSArray/NSSet` 有一个更便捷的方法 `valueForKey:`,可以快速取出对应属性组成的数组。但是有个问题就是这个方法的效率比 `for` 循环低，数据量不大的时候使用还是没有问题的。如下面两张图：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/4-1.jpg?raw=true)

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/4-2.jpg?raw=true)

* 要取两个数组的交集的时候，可以先将 `NSArray` 转换成 `NSMutableSet`，再通过取二者交集即可。但是需要注意一点的是数组中的元素最好复写一下 `isEqual:` 和 `hash` 方法，保证取交集后的结果是正确的。

* 要将数组内元素排序或者过滤等操作，可以结合 `NSSortDescriptor` 和 `NSPredicate` 使用，可以避免掉大量冗余的 `for` 循环之类的代码。关于 `NSPredicate` 的用法可以参考 [NSHipster](http://nshipster.com/nspredicate/) 和 `Realm` 的 [Cheetsheet](https://academy.realm.io/posts/nspredicate-cheatsheet/)

* 关于图中 `valueForKey:` 的参数为什么不直接用 `@"name"` 而是用 `NSStringFromSelector(@selector(name))`，是因为后者会有代码提示可以避免硬编码带来的错误，同时后续该 `key` 换名字了之后，会有对应的警告。这个也是从 `AFNetworking` 中学到的。如图所示：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/4-3.jpg?raw=true)
