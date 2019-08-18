---
title: Uninhabited Types
date: 2017-02-01 00:00:00
author: 知识小集成员
cover: true
---

Uninhabited Types
----------

`Never`是一个空枚举，即没有有效的`case`。所以它是一种`uninhabited type`，即明显没有值的类型。`Swift`中，以下两种情况可以看成是`uninhabited type`：

1. 一个枚举类型，如果没有`case`，或者所有`case`已知，且所有的`case`都有关联值，而所有的关联值类型都为空；
2. 元组、结构体或者类，如果有任意的`uninhabited type`类型的存储属性；

> If an expression of uninhabited type is evaluated, it is considered unreachable by control flow diagnostics.

另外，函数和元类型不能是`uninhabited type`。

参考

1. [Remove @noreturn attribute and introduce an empty Never type](https://github.com/apple/swift-evolution/blob/master/proposals/0102-noreturn-bottom-type.md)