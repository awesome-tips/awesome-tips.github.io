---
title: 用xcconfig配置BuildSettings
date: 2018-02-01 00:00:00
author: 高老师很忙
layout: post
---


当我们项目中有很多 `Target`，并且不同 `Configurations` 下的配置也不同的时候，直接配置 `BuildSettings` 是一件很痛苦的事情，这个时候就可以用 `xcconfig` 来解耦了。`xcconfig` 是用来保存 `BuildSettings` 键值对的纯文本文件，并且还可以共享公用的配置，在中大型项目中很是实用。

我们来举个简单栗子🌰吧，创建2个`xcconfig`文件，一个是`Common.xcconfig`（公共设置）,一个是`Debug.xcconfig`（Debug的时候使用的），如图1；

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/21-1-1.JPG?raw=true)

如图2；

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/21-1-2.JPG?raw=true)

如图3；

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/21-1-3.JPG?raw=true)

这个时候我们去 `Build Settings` 里面去查看就可以看到我们写入的内容了，如图4。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/21-1-4.JPG?raw=true)
