---
title: Swift中lazy作惰性求值static方法与class方法的区别
date: 2017-01-01 00:00:00
author: 知识小集成员
layout: post
---


在Swift中，`static`和`class`这两个关键字都可以修饰类的方法，以表明这个方法是一个类方法。不过这两者稍微有一些区别：`class`修饰的类方法可以被子类重写，而`static`修饰的类方法则不能。如下代码所示：

```swift
class A {
    
    class func method1() {
        print("A.method1");
    }
    
    static func method2() {
        print("A.method2");
    }
}

class B : A {
    
    override class func method1() {
        print("B.method1");
    }
    
    override static func method2() {	// Error: Cannot override static method
        print("B.method2");
    }
}

B.method1()
B.method2()
```
