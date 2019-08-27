---
title: Sequence prefix(while:)
date: 2017-04-01 00:00:00
author: 知识小集成员
layout: post
---


Swift的`Sequence`协议提供了一个`prefix(_:)`方法，返回序列前面n个元素组成的序列，与之对应的是`suffix(_:)`方法，返回序列后面n个元素组成的序列。如果指定的长度大于序列的长度，则返回整个序列。如下代码所示：

```swift
var arr = [Int]()

for i in 0..<20 {
    arr.append(i)
}

arr.prefix(5)           // [0, 1, 2, 3, 4]
arr.suffix(5)           // [15, 16, 17, 18, 19]

arr.prefix(30)          // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
arr.suffix(30)          // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
```

在`Swift 3.1`中新增了一个`prefix`方法，即`prefix(while:)`，它返回满足给定谓词的连续元素的子序列，直到第一个不满足的元素为止。同时还提供了一个类似的方法，即`drop(while:)`，不同的是这个方法是抛弃满足给定谓词的连续元素，而返回以第一个不满足谓词的元素为起始元素，后续元素组成的子序列，如下代码所示：

```swift
var arr = [2, 4, 6, 7, 10, 3, 9, 19]

// [2, 4, 6]
arr.prefix {
    $0 % 2 == 0
}

// [7, 10, 3, 9, 19]
arr.drop {
    $0 % 2 == 0
}
```

[raywenderlich](https://www.raywenderlich.com/156352/whats-new-in-swift-3-1) 中给了一个`Fibonacci`的例子，如下所示，可以参考一下：

```swift
let fibonacci = sequence(state: (0, 1)) {
  (state: inout (Int, Int)) -> Int? in
  defer {state = (state.1, state.0 + state.1)}
  return state.0
}

// Swift 3.1
let interval = fibonacci.prefix(while: {$0 < 1000}).drop(while: {$0 < 100})
for element in interval {
  print(element) // 144 233 377 610 987
}
```

参考

1. [What’s New in Swift 3.1?](https://www.raywenderlich.com/156352/whats-new-in-swift-3-1)
2. [Swift evolution: Add prefix(while:) and drop(while:) to the stdlib](https://github.com/apple/swift-evolution/blob/master/proposals/0045-scan-takewhile-dropwhile.md)


