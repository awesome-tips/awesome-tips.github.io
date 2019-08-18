---
title: string view 
date: 2017-03-01 00:00:00
author: 知识小集成员
cover: true
---

string view 
----------

`Swift`中的`String`本身不是一个集合，不过它提供了一些属性来将其内容表示为集合。不同的属性可以将字符串呈现为不同的可视化及数据表示的视图，主要有4种类型：

1. `Character View`(`characters`属性，类型为`String.Character​View`)：扩展字符集群的集合，类似于自然语言字符。主要是以`Unicode`字符来表示；
2. `Unicode Scalar View`(`unicode Scalars`，类型为`String.Unicode​Scalar​View`)：`Unicode`标题值的集合，即以`21-bit`作为`Unicode`的基本单元的值；
3. `UTF-16 View`(`utf16`属性，类型为`String.UTF16View`)：`UTF-16`字符的集合，即以`16-bit`作为`Unicode`的基本单元的值；
4. `UTF-8 View`(`utf8`属性，类型为`String.UTF8View`)：`UTF-8`字符的集合，即以`8-bit`作为`Unicode`的基本单元的值；如果`Swift`要和`C API`交互，则`String`以这种格式传递给C函数；

官方文档给了一个实例，如图1所示，可以看到这几种表示方式的区别。

```swift
let cafe = "Cafe\u{301} du 🌍"

print(cafe.unicodeScalars.count)
// Prints "10"
print(Array(cafe.unicodeScalars))
// Prints "["C", "a", "f", "e", "\u{0301}", " ", "d", "u", " ", "\u{0001F30D}"]"
print(cafe.unicodeScalars.map { $0.value })
// Prints "[67, 97, 102, 101, 769, 32, 100, 117, 32, 127757]"

print(cafe.utf16.count)
// Prints "11"
print(Array(cafe.utf16))
// Prints "[67, 97, 102, 101, 769, 32, 100, 117, 32, 55356, 57101]"

print(cafe.utf8.count)
// Prints "14"
print(Array(cafe.utf8))
// Prints "[67, 97, 102, 101, 204, 129, 32, 100, 117, 32, 240, 159, 140, 141]"
```

参考

1. [String](https://developer.apple.com/reference/swift/string)
