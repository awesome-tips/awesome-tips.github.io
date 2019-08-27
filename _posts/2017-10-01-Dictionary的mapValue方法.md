---
title: Dictionary的mapValue(_:)方法
date: 2017-10-01 00:00:00
author: 知识小集成员
layout: post
---


Swift 4中的Dictionary字典新增了一个mapValue(_:)方法，来转换字典的值，同时保留key。如下代码所示：

```swift

let original = ["A": "Apple", "F": "Facebook", "G": "Google"]

let result = original.mapValues { (item) -> Int in
    return item.count
}

print(result)

// ["G": 6, "A": 5, "F": 8]
```

其中original和result有相同的key，只是值不同，所以它们有相同的内部布局，不需要重新计算hash值，因此这种方式创建字典会比重新构建一个字典更快。
