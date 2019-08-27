---
title: ArraySlice的用途
date: 2017-02-01 00:00:00
author: 知识小集成员
layout: post
---

`Swift`提供了`ArraySlice`来执行数组的切片操作。类似于其它语言中的切片(如Python)，`ArraySlice`对象复用了原始数组的存储结构，而不是新开辟一块内存区域来将数组片断的元素拷贝过来。因此，它能让我们快速高效地对大数组的片段执行操作。如下代码所示：

```swift
var array: [Int] = []

for i in 0..<1000 {
    array.append(i)
}

let slice = array[100..<300]
let result = slice.map {
    $0 * 2
}.reduce(0) {
        $0 + $1
}

print(result)       // 79800
```

`ArraySlice`与`Array`有相同的接口，所以通常可以在切片数组上执行与原始数组相同的操作。

参考

1. [ArraySlice](
