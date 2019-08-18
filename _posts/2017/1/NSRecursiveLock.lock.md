---
title: NSRecursiveLock.lock(before:)
date: 2017-01-01 00:00:00
author: 知识小集成员
cover: true
---

NSRecursiveLock.lock(before:)
----------

`NSRecursiveLock`递归锁提供了一个方法`lock(before:)`，用于在多线程情况下，去尝试请求一个递归锁，然后根据返回的布尔值，来做相应的处理。如下代码所示，是一个正常的递归锁调用过程：

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
```

在这个场景下，如果我们想另起一个线程，并且尝试去获取这个递归锁，则可以如下代码处理：

```swift
DispatchQueue.global().async {
  sleep(2)
  
  let flag = lock.lock(before: Date(timeIntervalSinceNow: 1))
  if flag {
      print("lock before date")
      lock.unlock()
  } else {
      print("fail to lock before date")
  }
}
```

当然这种情况下会失败，其输出如下所示。如果将`lock(before:)`中的时间设置长一点，则会打印出"lock befor date"。