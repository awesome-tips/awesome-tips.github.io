---
title: Tagged-Pointer
date: 2017-01-01 00:00:00
author: 知识小集成员
cover: true
---

Tagged-Pointer
----------

苹果在64位ARM架构下，对`NSNumber`等小对象对象的存储做了优化，即使用`Tagged Pointer`技术。通过使用这种技术，`NSNumber`指针变量指向的值不再是单独存储在一块内存中，而是对指针本身做了特殊处理，如下图代码所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/01/17-1-1.png?raw=true)

可以看到这些指针一部分直接保存数据(如下图蓝色部分)，另一部分作为特殊标记(如图2红色部分)，表示这是个特殊指针，不指向任何地址。这么做大大减少了这类值的存储空间，同时提高了它们的创建及读取效率。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/01/17-1-2.png?raw=true)

当然，如果数据存储部分(7个字节)无法容纳下变量的值，则会按原始的方式，另辟空间去存储值，指针的值仍然是指向这个空间的地址，如下图所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/01/17-1-3.png?raw=true)

参考

1. [深入理解Tagged Pointer](http://www.infoq.com/cn/articles/deep-understanding-of-tagged-pointer)
2. [WWDC 2013 Advanced in Objective-C](https://developer.apple.com/videos/play/wwdc2013/404/)