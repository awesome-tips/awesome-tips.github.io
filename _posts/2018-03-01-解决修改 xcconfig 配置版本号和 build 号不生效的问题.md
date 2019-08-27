---
title: 解决修改 xcconfig 配置版本号和 build 号不生效的问题
date: 2018-03-01 00:00:00
author: 高老师很忙
layout: post
---

之前我有介绍过 `xcconfig` 这个 tip，最近使用中遇到了一点小问题：当我使用 `xcconfig` 来管理版本号和 `build` 号时（如下图所示），

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/03/5-1.jpg?raw=true)

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/03/5-2.jpg?raw=true)

编译一次之后，修改这两个值，此时我在运行的时候想把这两个值读出来，如下图所示：

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/03/5-3.jpg?raw=true)

发现读出来的依然是修改之前的值，如下图所示：

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/03/5-4.jpg?raw=true)

此时打开 `Product` 下面的 `Demo.app` 文件，查看 `Info.plist` 文件发现，里面果然显示的还是老值，如下图所示：

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/03/5-5.jpg?raw=true)

这是因为使用 `xcconfig` 管理这两个值后，`Info.plist` 用的这两个值是 `User-Defined` 变量，并不能检测这两个变量内容有变更导致的缓存问题。最简单的解决办法就是 `Clean` 一下，再运行就能显示正确的值了，但对于中大型项目来说 `Clean` 的成本有点高，所以就想到了用脚本来解决这个问题（如下图所示），

![](https://github.com/iOS-Tips/iOS-tech-set/blob/master/images/2018/03/5-6.jpg?raw=true)

每次运行时更新这两个缓存中的值即可。

如果有其他更好的解决办法，欢迎分享！
