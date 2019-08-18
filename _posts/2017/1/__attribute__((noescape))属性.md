---
title: __attribute__((noescape))属性
date: 2017-01-01 00:00:00
author: 知识小集成员
cover: true
---

\_\_attribute\_\_((noescape))属性
----------

在Cocoa中，大部分API的`closure/block`参数都是逃逸的(`escaping`)，因此，在swift中调用Objective-C的API时，编译器会自动在Objective-C API中的`closure/block`参数前面添加`@escaping`。

在Objective-C中，如果我们不希望`block`是逃逸的，则可以在参数前面添加`((noescape))`属性，如下代码所示。另外也可以用系统提供的`NS_NOESCAPE/CF_NOESCAPE`宏。

```objc
// Handler.h
typedef void (^CompleteHandler)(void);

@interface Handler : NSObject

- (void)invokeBlockNow:(__attribute__((noescape)) CompleteHandler)blk;

- (void)invokeBlockLater:(NS_NOESCAPE CompleteHandler)blk;

@end

// Handler.m
@interface Handler ()

@property (nonatomic, strong) NSMutableSet *laterBlocks;

@end

@implementation Handler

- (void)invokeBlockNow:(CompleteHandler)blk {
    blk();
}

- (void)invokeBlockLater:(CompleteHandler)blk {
    if (self.laterBlocks == nil) {
        self.laterBlocks = [NSMutableSet set];
    }
    
    [self.laterBlocks addObject:blk];
    
    dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(2 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
        NSSet *blocks = [self.laterBlocks copy];
        for (void (^blk)(void) in blocks) {
            blk();
        }
    });
}

@end
```

不过在Xcode 8下测试了一下，编译器对这个属性貌似是无感的，在Siwft中调用，无论有没有加`((noescape))`属性，都不会有错误或警告提示，如下代码所示：

```swift
class HandlerCaller: NSObject {

    func call() {
        
        let handler = Handler()
        
        handler.invokeBlockNow { 
            print("invoke block now in swift")
        }
        
        handler.invokeBlockLater { 
            print("invoke block later in swift")
        }
    }
}
```

另外，对`C API`的处理也是相同的。

参考

1. [Make non-escaping closures the default](https://github.com/apple/swift-evolution/blob/master/proposals/0103-make-noescape-default.md)
2. [Add @noescape to public library API](https://github.com/apple/swift-evolution/blob/master/proposals/0012-add-noescape-to-public-library-api.md)