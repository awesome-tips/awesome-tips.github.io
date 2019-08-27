---
title: Swift中的escaping-closure
date: 2017-01-01 00:00:00
author: 知识小集成员
layout: post
---


在Swift中使用`@escaping`来修饰一个逃逸闭包(`Escaping Closures`)，即闭包作为参数传到一个函数中时，这个闭包可以不在函数中调用，而在函数返回之后的某个时间再调用。如可以在函数中将闭包赋值给一个类的成员变量，或者保存在一个数组中，以备后续异步调用。这类闭包参数需要使用`@escaping`来修饰，否则会报错，如下代码所示：

```swift
var handlers: [(Int) -> Void] = []

func complete(handler: (Int) -> Void) {
    handlers.append(handler)	// error: passing non-escaping parameter 'handler' to function expecting an @escaping closure
}
```

需要注意的一个问题是，如果在类中使用逃逸闭包，且闭包内要调用实例对象的属性或方法时，必须显式地引用`self`，否则会报错，如下代码所示：

```swift
class A {
    
    var x = 10
    
    func testEscaping() {
        
        complete { (value) in
            print(value + x)		// error: reference to property 'x' in closure requires explicit 'self.' to make capture semantics explicit
        }
        
        handlers[0](10)
    }
}
```
