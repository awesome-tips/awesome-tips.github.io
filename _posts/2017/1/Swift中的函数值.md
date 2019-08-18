---
title: Swift中的函数值
date: 2017-01-01 00:00:00
author: 知识小集成员
cover: true
---

Swift中的函数值
----------

我们知道在Swift中，函数是一等公民，即函数也是一种类型，可充当参数、返回值等角色，当然也可以定义函数类型的常量/变量。利用这个特性，在某些场景下可以简化我们的代码，如下代码所示：

```swift
let setInt: (Int, String) -> Void = UserDefaults.standard.set
let getInt: (String) -> Int = UserDefaults.standard.integer

setInt(10, "key")
print(getInt("key"))
```