---
title: NSFetchedResultsController兼容性问题
date: 2017-11-01 00:00:00
author: Vong_HUST
layout: post
---

熟悉 `CoreData` 的都知道 `NSFetchedResultsController` 这个类，与 `tableView` 和 `collectionView` 结合起来使用非常方便。

但是这个类在 `iOS10` 中有个比较坑爹的地方，如果使用的是下图的方式初始化

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/18-1.jpg?raw=true)

并且传入的 `cacheName` 不为 `nil`，那么在 `iOS10` 下面可能会产生各种莫名其妙的崩溃。详细原因如下图描述：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/18-2.jpg?raw=true)

简单翻译一下就是：修改了 `vc` 的 `fetchRequest` 之后，`context` 的 `save` 操作会打开一个或多个文件描述符，当打开的文件描述符数目超过`255`(真机)后，后续的资源加载都会导致崩溃。

当初遇到这个问题的时候，整个应用都处于随机崩溃的情况，看日志都是加载 `storyboard` 或者 `xib` 等资源时的崩溃，但是死活复现不出来，看崩溃日志也找不到原因。然后无意间发现 `Xcode console` 中一直不断输出如下警告信息：

```objc
(NSFetchedResultsController): couldn't read cache file to update store info timestamps
```

然后 google 了一下，找到了一个相同的问题，并且有完整的复现 `Demo` 及复现步骤，然后全局代码搜索果然发现有一个地方初始化的时候传入了 `cacheName`，将其置 `nil` 后就再也没有那段 `warning` 同时上线之后也没有再收到资源加载的崩溃了。

所以 `Xcode` 的 `warning` 还是值的注意的。附上这个 `radar` 的[链接](http://www.openradar.me/28361550)，里面包含 `Demo` 地址。

今天再去复现的时候，试了两台 `iOS10` 的设备，`Xcode 9.1` 下 `iPhone5S iOS10.2` 这个 bug 已经不存在了，但是 `iPhone7 iOS10.0` 还是存在的。
