---
title: Swift的stride操作
date: 2017-01-01 00:00:00
author: 知识小集成员
cover: true
---

Swift的stride操作
----------

在Swift中，如果我们想创建一个一定步长的数组，可以如下代码操作：

```swift
var array: [Double] = []
for value in 0..<10 {
    array.append(Double(value) * 0.3)
}
```

不过如果想在某个区间创建这样一个序列的话，会比较麻烦。为此，Swift提供了一个便捷函数：`stride`，可以在某个区间内创建一个任意可变步长的序列，这个步长可以是任意值。所以上面这个问题的实现可以如下代码处理：

```swift
let array = stride(from: 0, to: 3, by: 0.3).map {
    $0
}
```

实际上，`stride`的产生的序列如下代码：

`start, start + stride, start + 2 * stride, …, start + n * stride`

`stride`有两个变种：

1. `stride(from:to:by)`，开区间处理，最后一个值严格小于最大值；
2. `stride(from:through:by)`，闭区间处理，最后一个值小于或等于最大值

`stride`函数与`map`配合起来可以做一些有意思的事情。