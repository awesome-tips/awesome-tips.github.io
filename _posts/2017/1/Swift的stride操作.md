---
title: Swift中lazy作惰性求值
date: 2017-01-01 00:00:00
author: 知识小集成员
cover: true
---

Swift中lazy作惰性求值
----------

函数式编程中有惰性求值的概念，即一次计算在真正需要时才执行，尽可能推迟求解表达式。

假如我们有一个数组，我们对每个元素作`element*2`的map操作，获取其中某一个元素，我们会如下代码处理:

```swift
let array = [1, 2, 4, 5, 3, 7]
let element = array.map{ $0 * 2 }[3]
print(element)
```

这个计算对每个元素都*2，最后我们只取了其中一个值，也就是说在这个场景中另外5次计算是无意义的。

这时使用惰性求值就可以避免这算浪费。我们知道Swift中有个lazy关键字，如果用来修饰属性之类的，可以实现属性的惰性求值。同样，Swift扩展了LazySequenceProtocol协议，提供了一个lazy属性，用于处理map，filter等操作的惰性求值，定义如下代码所示：

```swift
/// Avoid creating multiple layers of `LazySequence` wrapper.
/// Anything conforming to `LazySequenceProtocol` is already lazy.
extension LazySequenceProtocol {

    /// Identical to `self`.
    public var lazy: Self { get }
}
```

所以，上面这个例子如果要实现惰性求值，则可以如下代码处理：

```swift
let array = [1, 2, 4, 5, 3, 7]
let element = array.lazy.map{ $0 * 2 }[3]
print(element)
```

我们在Playground中可以看到，整个计算中实际只执行了一次*2操作。