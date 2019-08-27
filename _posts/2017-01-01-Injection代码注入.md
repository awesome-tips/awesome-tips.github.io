---
title: Injection代码注入
date: 2017-01-01 00:00:00
author: 知识小集成员
layout: post
---


`Injection`是johnno开发的一个`Xcode`插件，允许我们将代码实现更快注入到模拟器运行的程序或macOS程序。原先可以通过`Alcatraz`安装到Xcode中，不过现在是独立的App了。可以在[这里](http://johnholdsworth.com/Injection.app.zip)下载安装。启动后会出现在屏幕顶部的工具栏中，如下图所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/01/10-1-1.png?raw=true)

要检测是否有效，可以在某个类里面添加`injected`方法，然后打个断点。在代码修改后保存，然后注入，如果进入这个断点，则说明安装成功，同时控制器会有相应信息输出，如下图所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/01/10-1-2.png?raw=true)

`Injection`使用`AppleScript`来和Xcode进行通信，以确定当前的文件与工程，然后将代码注入到模拟器，再加载新代码，并将新代码替换原来的代码。其效果如下图所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/01/10-1-3.gif?raw=true)

`Injection`程序还包含一个`Xprobe`浏览器，用于查看程序的内存。可以选择图1中的`Load Xprobe`菜单项，弹出的窗口中显示了当前时间点的对象实例，我们可以在这做一些有意思的事情，如下图所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/01/10-1-4.png?raw=true)

[Injection工程源码](https://github.com/johnno1962/injectionforxcode)

[文档](https://johntmcintosh.com/blog/2016/10/03/code-injection-ios)
