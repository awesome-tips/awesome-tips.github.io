---
title: ViewController关联XIB文件时初始化方法的调用
date: 2017-11-01 00:00:00
author: Vong_HUST
layout: post
---

在新建一个 `ViewController` 文件时，如果同时也勾选了 `Also create XIB file`，那么`ViewController *viewController = [[ViewController alloc] init]` 得到的是和 `initWithNibName:bundle:` 初始化得到的 UI 一致的。原因是 `init` 方法最终都会调到指定构造器 `initWithNibName:bundle:`，但此时 `nibName` 为 `nil`，而且没有 VC 复写 `loadView` 的情况下，则系统会有一套自己的寻找机制来看是否有对应的 xib 文件，如果有，则加载 xib 文件。具体可参考苹果官方文档的[解释](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621487-nibname?language=objc)：

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/11/9-1.jpg?raw=true)
