---
title: iOS 11中applicationDidEnterBackground:延迟执行
date: 2017-09-01 00:00:00
author: 知识小集成员
layout: post
---

App 进入后台后, `applicationDidEnterBackground:`这个方法将延迟大约 1000 毫秒执行, 那么如果在进入后台时做一些任务，可能会达不到预期的效果。如果 App 刚进入应用立即启动，`applicationDidEnterBackground:` 和 `applicationWillEnterForeground:` 这两个方法都不会调用。如果有这么一个场景，进入后台后给应用设置手势密码，当 App 刚进入后就立即启动，那么 `applicationDidEnterBackground`：这个方法不会立即执行，从而手势密码也就不会设置。

