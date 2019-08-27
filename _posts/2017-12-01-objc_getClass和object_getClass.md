---
title: objc_getClass和object_getClass
date: 2017-12-01 00:00:00
author: 南峰子_老驴
layout: post
---

昨天打开好久没开的公众号后台，看到一个小伙伴 [@阳光下的小泡沫星人002](https://weibo.com/u/5848750701) 给我留言，指正我之前写的关于Runtime的[文章](http://southpeak.github.io/2014/10/25/objective-c-runtime-1/) 中一个错误之处，并为此写了一篇[文章](http://www.jianshu.com/p/d0c6a3efb4d4) 在此感谢。

这个错误是关于获取 `NSObject` 的元类的 `isa` 指针的问题。在我的文章中，错误的用 `objc_getClass((__bridge void *)[NSObject class])` 这种方式来获取对象的指针。代码如下：

```objc
void TestMetaClass(id self, SEL _cmd) {
    NSLog(@"This objcet is %p", self);
    NSLog(@"Class is %@, super class is %@", [self class], [self superclass]);
    Class currentClass = [self class];
    for (int i = 0; i < 4; i++) {
        NSLog(@"Following the isa pointer %d times gives %p", i, currentClass);
        currentClass = objc_getClass((__bridge void *)currentClass);
    }
    NSLog(@"NSObject's class is %p", [NSObject class]);
    NSLog(@"NSObject's meta class is %p", objc_getClass((__bridge void *)[NSObject class]));  // 0x0
}
```

实际上 `objc_getClass` 的参数是类名的字符串，获取指定类的类对象。上述代码中 `(__bridge void *)[NSObject class])` 的结果并不是类名的字符串，而是一个对象的指针，所以 `objc_getClass` 函数返回值的相当于是一个 `nil`，打印指针的值就是 `0x0`。所以正确使用 `objc_getClass` 的方式应该是`objc_getClass("NSObject")`，其效果与 `[NSObject class]` 是一样的。

要想获取 `NSObject` 类对象的元类，可以使用 `object_getClass` 函数。这个函数参数是 `id` 类型，即一个对象，返回对象的 `Class` 信息，即对象的 `isa` 指针；如果传入的是一个类对象，获取的就是元类信息。

所以正确的代码如下，`for` 循环中的输出结果也印证了 `NSObject` 元类的isa指向的是其本身。

```objc
void TestMetaClass(id self, SEL _cmd) {
    NSLog(@"This objcet is %p", self);
    NSLog(@"Class is %@, super class is %@", [self class], [self superclass]);
    Class currentClass = [self class];
    for (int i = 0; i < 4; i++) {
        NSLog(@"Following the isa pointer %d times gives %p", i, currentClass);
        currentClass = object_getClass(currentClass);
    }
        
    // Following the isa pointer 0 times gives 0x10048e1f0
    // Following the isa pointer 1 times gives 0x10048e220
    // Following the isa pointer 2 times gives 0x7fff8c8e50f0
    // Following the isa pointer 3 times gives 0x7fff8c8e50f0
    NSLog(@"NSObject's class is %p", [NSObject class]);
    NSLog(@"NSObject's meta class is %p", object_getClass([NSObject class]));      
        
    // NSObject's class is 0x7fff8c8e5140
    // NSObject's meta class is 0x7fff8c8e50f0
}
```

由于博客已停更，错误之处可以在微博上私信。还请阅读的时候不要盲从。
