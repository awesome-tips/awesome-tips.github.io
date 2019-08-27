---
title: 指定构造器在 UITableViewController 中的坑
date: 2017-12-01 00:00:00
author: Vong_HUST
layout: post
---


我们都知道，如果我们想要自定义指定构造器时，应该要遵循以下3个原则(图1)：
1、子类指定构造器必须调用父类指定构造器
2、便捷构造器只能通过调用自身指定构造器来完成初始化
3、指定构造器必须要用 `NS_DESIGNATED_INITIALIZER` 标示
![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/12/5-1.jpg?raw=true)
但是如果你继承了 UITableViewController，并且自定义了指定构造器，而你的项目刚好要支持 iOS8 的话，在 iOS8 下就会出现一个必崩的 bug。示例代码及简单解释见图2。
有人提了对应的 [radar](http://www.openradar.me/23709930)， stackoverflow 上也有对应的[详尽解释](https://stackoverflow.com/a/30719434) 更多内容可[查看](http://t.cn/RX978vi)
目前唯一的解决方案就是不继承 UITableViewController，而是继承自 UIViewController 然后持有一个 UITableView😂
![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/12/5-2.jpg?raw=true)
