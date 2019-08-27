---
title: pod install 和 pod update 的区别
date: 2017-11-01 00:00:00
author: Vong_HUST
layout: post
---

首先 `podfile.lock` 和 `podfile` 必须加入版本控制。

`install` 并不是第一次创建 `podfile` 时运行一次，后面就不再使用了。`install` 命令不仅在初始时使用，在新增或删除 `repo` 时也需要运行。每次添加或删除 `repo` 后应该执行 `install` 命令，这样其它的 `repo` 不会更新。`update` 仅仅在只需更新某一个 `repo` 或所有时才使用。每次执行 `install` 时，会将每个 `repo` 的版本信息写入到 `podfile.lock`，已存在于 `podfile.lock` 的 `repo` 不会被更新只会下载指定版本，不在 `podfile.lock` 中的 `repo` 将会搜索与 `podfile` 里面对应 `repo` 匹配的版本。即使某个 `repo` 指定了版本，如 `pod 'A', '1.0.0'`，最好也是不要使用 `update`，因为 `repo A` 可能有依赖，如果此时使用 `update` 会更新其依赖。

参考：

1. [pod install vs. pod update](https://guides.cocoapods.org/using/pod-install-vs-update.html)
