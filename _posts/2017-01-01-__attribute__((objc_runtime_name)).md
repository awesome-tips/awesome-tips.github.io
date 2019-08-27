---
title: __attribute__((objc_runtime_name))
date: 2017-01-01 00:00:00
author: 知识小集成员
layout: post
---


`Objective-C`在默认情况下是将类或协议的名字作为元数据名称(`metadata name`)，即如果我们打印一个对象的`class`方法，输出就是对象所属类的类名，如下图所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/01/16-1-1.png?raw=true)

如果我们想为类或协议指定一个字符串作为其元数据名称，而不是使用默认的，则可以使用编译属性`objc_runtime_name`，如下图代码所示，只需要在类或协议声明之前加上`__attribute__((objc_runtime_name("identifier")))`。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/01/16-1-2.png?raw=true)

参考

1. [Clang 5 documentation](http://clang.llvm.org/docs/AttributeReference.html#objc-runtime-name)
2. [Clang Attributes 黑魔法小记](http://blog.sunnyxx.com/2016/05/14/clang-attributes/)
