---
title: __attribute__((objc_requires_super))
date: 2017-01-01 00:00:00
author: 知识小集成员
layout: post
---


Objective-C允许子类可以重写父类的方法。如果我们希望子类方法重写父类方法时必须使用super来调用父类的对应方法，则可以在方法声明后面添加clang的编译属性`objc_requires_super`。添加这一属性后，如果子类没有调用父类方法，则会给出一个编译警告，如下代码所示：

```objc
@interface Bird : NSObject

- (void)fly __attribute__((objc_requires_super));

@end

@implementation Bird

- (void)fly {
    NSLog(@"Bird Fly");
}

@end


@interface Eagle : Bird

@end

@implementation Eagle

- (void)fly {
    
}		// Method possibly missing a [super fly] call

@end
```

这个属性只能用记类中的方法声明，而不能用于协议。另外，`Foundation`提供了一个对应的宏`NS_REQUIRES_SUPER`，定义如下代码所示：

```objc
#ifndef NS_REQUIRES_SUPER
#if __has_attribute(objc_requires_super)
#define NS_REQUIRES_SUPER __attribute__((objc_requires_super))
#else
#define NS_REQUIRES_SUPER
#endif
#endif
```

参考

1. [Attributes in Clang](http://clang.llvm.org/docs/AttributeReference.html#objc-requires-super)
