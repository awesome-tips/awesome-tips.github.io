---
title: ArraySlice使用注意事项
date: 2017-02-01 00:00:00
author: 知识小集成员
layout: post
---

使用`ArraySlice`时，需要注意两点：

- `ArraySlice`会维持对原始数组的一个强引用，而不仅仅是它所表示的片断。这样即使原始数组对象的生命周期结束了，也可能无法释放。所以不建议长期存储`ArraySlice`对象，仅用于临时操作。如下代码所示：

```swift
class MyClass {
    var index: Int
    init(index: Int) {
        self.index = index
    }
}

class ViewController: UIViewController {
    
    var slice: ArraySlice<MyClass>? = nil
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        var array: [MyClass] = []
        for i in 0..<100 {
            let clz = MyClass(index: i)
            array.append(clz)
        }
        
        slice = array[10..<30]
    }
}
```

`array`在生命周期结束后不会释放，如下图所示。

![8-1-1](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/02/08-2-1.png?raw=true)

- 与`Array`不同的是，`ArraySlice`起始索引不一定是0，而是取决于其创建方式。一般是采用共享索引的方式，即`ArraySlice`对象的起始索引就是切片的开始位置，如代码清单8-2-2所示，切片是从100开始，所以`slice[100]`是OK的，而`slice[99]`会报越界错误。通常建议使用`startIndex`和`endIndex`来取代指定的索引值，如下代码所示。

```swift
var array: [Int] = []

for i in 0..<1000 {
    array.append(i)
}

let slice = array[100..<300]

slice[100]
slice[99]       // fatal error: Index out of bounds
```

```swift
slice[slice.startIndex]         // 100
slice[slice.endIndex - 1]       // 299
```

参考

1. [ArraySlice](
