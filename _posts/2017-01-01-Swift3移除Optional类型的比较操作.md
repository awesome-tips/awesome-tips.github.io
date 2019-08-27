---
title: Swift3移除Optional类型的比较操作
date: 2017-01-01 00:00:00
author: 知识小集成员
layout: post
---


`Swift 3`已经移除了`Optional`类型的比较操作，这在[Swift evolution SE-0121: Remove Optional Comparison Operators](https://github.com/apple/swift-evolution/blob/master/proposals/0121-remove-optional-comparison-operators.md)这条中明确了这一点。

在`Swift 3`之前，标准库定义了4个操作符以支持`Optional`类型，如下图所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/01/14-1-1.png?raw=true)

不过`Swift 3`中，由于泛型不支持条件一致性判断，即没有通用的方法来定义在比较nil和非nil值时，应该得到怎样的值，所以实际结果可能不是预期的。所以，在`Swift 3`中，如果去比较两个`Optional`值，会给出编译错误，如下代码所示。而这一比较在Swift 3之前是没有问题的。

```swift
let dic1 = [
    "first": "123",
    "last": "234"
]

let dic2 = [
    "first": "123",
    "last": "968"
]

dic1["middle"] < dic2["middle"]		// value of optional type 'String?' not unwrapped; did you mean to use '!' or '?'?
```

当然在SE-0121中也说了，等泛型更加成熟后，不排除会将这一特性再添加回来。
