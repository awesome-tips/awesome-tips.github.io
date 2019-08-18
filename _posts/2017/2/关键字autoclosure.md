---
title: 关键字autoclosure
date: 2017-02-01 00:00:00
author: 知识小集成员
cover: true
---

@autoclosure
----------

`Swift`中的`@autoclosure`还是一个很有意思的属性，它用于修饰函数中的闭包类型的参数，它主要有两个作用：

* 将一个表达式自动封装成一个闭包，从而简化函数/方法的调用方式，如下代码所示；

```swift
var customersInLine = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

// 显示闭包参数，调用时参数以闭包的方式传入
func serve(curstomer customerProvider: () -> String) {
    print("Now serving \(customerProvider())!")
}

serve(curstomer: {customersInLine.remove(at: 0)})

// autoclosure闭包
func serve2(curstomer customerProvider: @autoclosure () -> String) {
    print("Now serving \(customerProvider())!")
}

// 表达式`customersInLine.remove(at: 0)`被自动封装成一个闭包
serve2(curstomer: customersInLine.remove(at: 0))
```

2. 由于表达式封装成了闭包，所以可以延迟表达式的计算，一直到闭包被调用时。关于这一点的好处，可以参考[这里](https://developer.apple.com/swift/blog/?id=4)中对`assert`实现的介绍。

需要注意的是，封装后的闭包一般不带参数，而表达式的值就作为返回值。所以声明函数时闭包一般没有输入参数，即使有也会被忽略，实际上在写代码时，`Xcode`就是将`@autoclosure`参数当成一个普通的类型

参考

1. [The Swift Programming Language (Swift 4) -- Closures](https://developer.apple.com/library/prerelease/content/documentation/Swift/Conceptual/Swift_Programming_Language/Closures.html#//apple_ref/doc/uid/TP40014097-CH11-ID543 https://developer.apple.com/swift/blog/?id=4)