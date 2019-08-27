---
title: filter与flatMap过滤nil
date: 2017-01-01 00:00:00
author: 知识小集成员
layout: post
---


使用高阶函数过滤一个数组中的nil可以有两种方法：`filter`和`flatMap`。

`filter`方法如下代码所示：

```swift
let array: [Int?] = [1, 2, 3, 5, nil, 9]

let result = array.filter { element in
    element != nil
}

print(result)		// [Optional(1), Optional(2), Optional(3), Optional(5), Optional(9)]
```

`flatMap`方法如下代码所示：

```swift
let array: [Int?] = [1, 2, 3, 5, nil, 9]
let result: [Int] = array.flatMap {
    $0
}

print(result)		// [1, 2, 3, 5, 9]
```

从输出可以看出，`filter`返回的仍然是一个`Optional`数组，而`flatMap`返回的是一个非`Optional`数组。一般推荐使用第二种方法。
