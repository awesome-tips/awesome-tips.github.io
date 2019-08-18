---
title: Array.contains操作
date: 2017-01-01 00:00:00
author: 知识小集成员
cover: true
---

Array.contains操作
----------

Swift中判断一个`Array`中是否包含某个元素，我们可以使用`contains`方法，如下代码所示：

```swift
let array = [2, 5, 6, 7, 19, 40]

array.contains(10)				// false
```

不过这个方法要求数组中的元素类型实现了`Equatable`协议，否则无法使用，如下代码所示：

```swift
enum Animal {
    case dog
    case cat(Int)
}

let animals: [Animal] = [.dog, .dog]
let hasCat = animals.contains(.cat(100))	// 编译器错误
```

还好Swift为我们提供了另一个`contains`方法，可以自定义谓词条件作为判断依据，其定义如下：

```swift
public func contains(where predicate: (Element) throws -> Bool) rethrows -> Bool
```

这个方法会查看数组是否包含满足给定的谓词条件的元素。可以看到这个方法是一个高阶函数，其参数是一个尾随闭包，在闭包内我们可以根据实际需要来实现我们自己的判断。所以上面的判断可以如下代码实现：

```swift
enum Animal {
    case dog
    case cat(Int)
}

let animals: [Animal] = [.dog, .dog]
let hasCat = animals.contains { animal in
    
    if case .cat = animal {
        return true
    } else {
        return false
    }
}
```

当然，对于元素类型实现了`Equatable`协议的数组，也可以使用这个方法。可以自定义谓词条件，查看数组是否有满足此条件的元素，如下代码所示：

```swift
let array = [2, 5, 6, 7, 19, 40]

array.contains { (element) -> Bool in
    element % 7 == 0
}
```