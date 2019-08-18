---
title: Swift3中的AnyHashable
date: 2017-01-01 00:00:00
author: 知识小集成员
cover: true
---

Swift3中的AnyHashable
----------

在`Swift 3`的标准库中添加了`AnyHashable`这一新类型，其用途是在需要`Hash`值的集合中，可以混合使用多种`Hashable`类型。例如，字典的`key`值，其要求是`Hashable`类型，如果希望`key`值是任意实现了`Hashable`协议的类型，则在声明字典时，可以使用`AnyHashable`作为`key`的类型，如下代码所示：

```swift
let description: [AnyHashable: Any] = [
    AnyHashable("😄"): "emoji",
    AnyHashable(42): "an Int",
    AnyHashable(34.2): "a Double",
    AnyHashable(Set(["a", "b"])): "a set of strings"
]

print(description[AnyHashable(42)]!)        // an Int
print(description[AnyHashable(34)])         // nil
print(description[AnyHashable(Set(["a", "b"]))]!)   // a set of strings
```

早先，在`ObjC`与`Swift`混合编程中，`ObjC`的`NSDictionary`导入到`Swift`时，是转换成`[NSObject: AnyObject]`类型。使用`NSObject`作为`key`的类型，因为`NSObject`是最接近于`AnyObject`且实现了`Hashable`的类型。不过`Swift`希望在标准库中限制`AnyObject`的使用，而更多的使用`Any`，所以加入了`AnyHashable`类型。

参考

1. [Add AnyHashable to the standard library](https://github.com/apple/swift-evolution/blob/master/proposals/0131-anyhashable.md)