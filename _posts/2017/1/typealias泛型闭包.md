---
title: typealias泛型闭包
date: 2017-01-01 00:00:00
author: 知识小集成员
cover: true
---

typealias泛型闭包
----------

在`Swift`中我们可以用`typealias`来为已经存在的类型重新定义名字的,通过命名可以使代码变得更加清晰。当然也可以给闭包类型定义一个新名字，给带有泛型的闭包重新定义名字的方式如下代码所示：

```swift
typealias Block<U> = (U, U) -> Bool

func compare<T: Comparable>(number1: T, number2: T, algorithm: Block<T>) -> Bool {
    return algorithm(number1, number2)
}

compare(number1: 10, number2: 20) {
    $0 < $1
}
```