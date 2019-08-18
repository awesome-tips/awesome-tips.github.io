---
title: Swift在扩展中重写父类方法
date: 2017-02-01 00:00:00
author: 知识小集成员
cover: true
---

Swift在扩展中重写父类方法
----------

`Swift`在类的`extension`中，如果想重写父类的方法，会有以下两个限制(不局限于这两个，可能还有其它)：

1. 类本身必须是NSObject体系下的类，且要重写的方法的参数、返回值不能带有纯Swift的类/结构体/枚举；
2. 不能使用inout参数；

当然参数和返回值的类型如果是`String`、`Array`、`Dictionary`、`Set`这些也是OK的。