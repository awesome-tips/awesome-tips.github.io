---
title: Swift3的#keyPath
date: 2017-01-01 00:00:00
author: 知识小集成员
cover: true
---

Swift3的#keyPath
----------

在`Objective-C/Swift`中使用`KVC`或`KVO`总是需要格外小心，因为对于`key`或`keyPath`，我们使用的是字符串字面量来处理。这样在编译期无法检测我们的输入是否正确，或许我们会因为一时大意，多写了或少写了一个字符，或拼错了单词。而这个错误只能在运行时，程序崩溃时才能发现，很不爽的吧。

为此，在`Swift 3`中引入了`#keyPath()`这个表达式，它接收`Object.property`形式的参数，并将其转换成字符串，如下代码所示。因为使用的是对象和属性的方式，所以在编译时，编译器能去检测这个表达式是否有效，从而避免了上面的问题。

```swift
class Person: NSObject {
    dynamic var firstName: String = ""
    
    init(firstName: String) {
        self.firstName = firstName
    }
}

let chris = Person(firstName: "Chris")


#keyPath(Person.firstName) // => "firstName"
chris.value(forKeyPath: #keyPath(Person.firstName))
```

参考

1. [Referencing Objective-C key-paths](https://github.com/apple/swift-evolution/blob/master/proposals/0062-objc-keypaths.md)