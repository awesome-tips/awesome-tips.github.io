---
title: Swift RawRepresentable
date: 2017-02-01 00:00:00
author: 知识小集成员
cover: true
---

Swift RawRepresentable
----------

`Swift`编译器自动为带有`raw type`的`enum`添加了`RawRepresentable`协议的实现。`RawRepresentable`协议的定义如代码清单11-1-1所示，它可以为某个类型定义一个关联的`raw value`，并在两者之间切换。如下代码所示是一个典型的带`raw value`的枚举。

```swift
public protocol RawRepresentable {

    associatedtype RawValue

    public init?(rawValue: Self.RawValue)

    public var rawValue: Self.RawValue { get }
}
```


```swift
enum Counter: Int {
    case one = 1, two, three, four, five
}

for i in 3...6 {
    print(Counter(rawValue: i))
}

// 输出
// Optional(__lldb_expr_197.Counter.three)
// Optional(__lldb_expr_197.Counter.four)
// Optional(__lldb_expr_197.Counter.five)
// nil
```

参考

1. [RawRepresentable](https://developer.apple.com/reference/swift/rawrepresentable)