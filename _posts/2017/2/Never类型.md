---
title: Never类型
date: 2017-02-01 00:00:00
author: 知识小集成员
cover: true
---

Never类型
----------

之前有一条知识小集讲了可以用 `@noreturn` 用来修饰函数，以告诉编译器函数永远不返回值给调用方。如下代码是原来的`fatalError`的声明。

```swift
public func fatalError(_ message: @autoclosure () -> String = default, file: StaticString = #file, line: UInt = #line)
```

不过作为函数类型的一个正交属性，它与函数声明的其它一些属性一起使用时会产生一些歧义，如与`@throws`和`non-void`返回值。如当成 `@throws` 一起使用时，可能会困惑指"无法正常返回，但可以抛出异常"，还是"完全无法返回"？

所以现在使用Never枚举类型来替代`@noreturn`，以消除这种歧义，所以`fatalError`现在声明如下代码所示。这样() throws -> Never就好理解了，即"不能正常返回，但可能抛出异常"。

```swift
/// Unconditionally prints a given message and stops execution.
///
/// - Parameters:
///   - message: The string to print. The default is an empty string.
///   - file: The file name to print with `message`. The default is the file
///     where `fatalError(_:file:line:)` is called.
///   - line: The line number to print along with `message`. The default is the
///     line number where `fatalError(_:file:line:)` is called.
public func fatalError(_ message: @autoclosure () -> String = default, file: StaticString = #file, line: UInt = #line) -> Never
```

需要注意的是`Never`是一个空枚举，如下代码所示：

```swift
/// The return type of functions that do not return normally; a type with no
/// values.
///
/// Use `Never` as the return type when declaring a closure, function, or
/// method that unconditionally throws an error, traps, or otherwise does
/// not terminate.
///
///     func crashAndBurn() -> Never {
///         fatalError("Something very, very bad happened")
///     }
public enum Never {
}
```

参考

1. [Remove @noreturn attribute and introduce an empty Never type](https://github.com/apple/swift-evolution/blob/master/proposals/0102-noreturn-bottom-type.md)