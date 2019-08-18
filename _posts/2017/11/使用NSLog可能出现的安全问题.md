---
title: 使用NSLog可能出现的安全问题
date: 2017-11-01 00:00:00
author: iOS_OneByte
cover: true
---

使用NSLog可能出现的安全问题
----------

**作者**: [iOS_OneByte](https://weibo.com/u/5549095051)

iOS 经常定义类似如下的输出宏:

```objc
#ifdef DEBUG
	#define ZJLog(fmt, ...) NSLog((fmt), ##__VA_ARGS__)
#else
	#define ZJLog(...)
#endif
```

但是大部分人可能只是遵循国际惯例，并不知道如果直接使用 `NSLog` 的危害或者如何去查看别人家的应用输出，其实很简单，只是 `Xcode` 隐藏的很深,路径如下

```
Xcode8 - Window - Devices
Xcode9 - Window - Devices And Simulators
```

如下图所示：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/13-2.jpg?raw=true)

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/13-3.jpg?raw=true)

这个利用好的话,对于调试自己或者查(po)看(jie)别人家的应用都很有用,效果如下图所示：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/13-4.jpg?raw=true)