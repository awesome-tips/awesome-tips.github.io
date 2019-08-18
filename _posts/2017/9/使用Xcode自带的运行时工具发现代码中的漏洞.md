---
title: 使用Xcode自带的运行时工具发现代码中的漏洞
date: 2017-09-01 00:00:00
author: Lefe_x
cover: true
---

使用Xcode自带的运行时工具发现代码中的漏洞
----------

**作者**: [Lefe_x](https://weibo.com/u/5953150140)

我们可以使用 `Xcode` 自带的 运行时工具发现代码中的漏洞，有些难以复现的 Bug 往往使用这些工具很容易定位到，比如线程引发的资源竞争问题，内存问题等。

* **Main thread checker**【Xcode 9 新增特性】：当某些代码必须在主线程执行时，而你没有在主线程执行，那么 Xcode 9 会提示。`XXX must be used from thread only.`。这个工具 `Xcode 9` 是默认打开的，建议开启。如下两图Xcode 9前后对比。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/09/26-1-2.jpg?raw=true)

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/09/26-1-3.jpg?raw=true)

* **Address Sanitizer**：发生内存异常时可以使用这个工具调试，比如 `buffer overflow`, `use-after-free`, `double free`, `use after end of scope`。

* **Thread Sanitizer**：定位多线程问题，比如数据争用（`Data race`），想要打开这个开关，需要关闭 `Address Sanitizer` ，`Malloc Stack` 和 `Memory Management` 选项。下面这段代码会出现资源竞争的问题。勾选后，将会提示：

```objc
Race on a library object in -[ViewController testThreadRace] at 0x7b080000db20

for (int i = 0; i < 10; i++) {
   dispatch_async(dispatch_get_global_queue(0, 0), ^{
      [self testThreadRace];
   });
}

- (void)testThreadRace
{
    BOOL found = [_dict objectForKey:@"lefe"];		// Race on a library object in -[ViewController testThreadRace] at 0x7b080004b520
    if (found) {
        NSLog(@"Found");
    }
    [_dict setObject:@"WangSuyan" forKey:@"lefe"];
}
```

* **Undefined Behavior Sanitizer 【Xcode 9新增特性】**：检测未定义的行为，这些多数服务于 C 语言，因为 OC 和 Swift 相对比较安全，在语言设计时就消除了大多数未定义的行为，如下图。它可以检测到大约 15 种未定义的行为，比如常见的有数组越界，未初始化，无效的枚举值，除数为零和空值判断等。我们用例子来列举几个未定义的行为（想了解更多看[官方文档](https://developer.apple.com/documentation/code_diagnostics/undefined_behavior_sanitizer)）：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/09/26-1-1.jpg?raw=true)

```objc
- (NSInteger)testUndefinedBehavior
{
    NSInteger value;
    if (self.name.length > 0) {
        value = 12;
    }
    return value;
}
```

如果勾选 `Undefined Behavior Sanitizer` 这样选项，Xcode 会提示

```
Variable 'value' is used uninitialized whenever 'if' condition is false
```