---
title: NSRecursiveLock递归锁的使用
date: 2017-01-01 00:00:00
author: 知识小集成员
layout: post
---


`NSRecursiveLock`定义的是一个递归锁，这个锁可以被同一线程多次请求，而不会引起死锁。它主要是用在循环或递归操作中。我们先来看下面代码示例：

```swift
let lock = NSLock()
var recursiveMethod: ((Int) -> Void)! = nil
   
recursiveMethod = { value in
  
  defer {
      lock.unlock()
  }
  
  lock.lock()
  
  guard value > 0 else {
      return
  }
  
  print(value)
  sleep(2)
  recursiveMethod(value - 1)
}
   
DispatchQueue.global().async {
  
  print("start")
  recursiveMethod(5)
  print("end")
}
```

这段代码是一个典型的死锁情况。在我们的线程中，`RecursiveMethod`是递归调用的。所以每次进入这个闭包函数时，都会去加一次锁，而从第二次开始，由于锁已经被使用了且没有解锁，所以它需要等待锁被解除，这样就导致了死锁，线程被阻塞住了。调试器中会输出信息如下代码所示：

```swift
start
5
2017-01-07 12:48:26.580 Test111[3633:116345] *** -[NSLock lock]: deadlock (<NSLock: 0x6080000c4750> '(null)')
2017-01-07 12:48:26.581 Test111[3633:116345] *** Break on _NSLockError() to debug.
```

在这种情况下，我们就可以使用`NSRecursiveLock`。它可以允许同一线程多次加锁，而不会造成死锁。递归锁会跟踪它被`lock`的次数。每次成功的`lock`都必须平衡调用`unlock`操作。只有达到这种平衡，锁最后才能被释放，以供其它线程使用。

所以，使用`NSRecursiveLock`对图1的代码进行一下改造，这样，程序就能正常运行了，如下代码所示：

```swift
let lock = NSRecursiveLock()
var recursiveMethod: ((Int) -> Void)! = nil
   
recursiveMethod = { value in
  
  defer {
      lock.unlock()
  }
  
  lock.lock()
  
  guard value > 0 else {
      return
  }
  
  print(value)
  sleep(2)
  recursiveMethod(value - 1)
}
   
DispatchQueue.global().async {
  
  print("start")
  recursiveMethod(5)
  print("end")
}

// 输出
// start
// 5
// 4
// 3
// 2
// 1
// end
```
