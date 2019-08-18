---
title: SourceTree 搭配 Kaleidoscope 进行 Code Review
date: 2017-12-01 00:00:00
author: 知识小集成员
cover: true
---

SourceTree 搭配 Kaleidoscope 进行 Code Review
----

平时在 `Gitlab`、`GitHub`、`SourceTree` 上进行 `CodeReview` 的时候，只能看到发生改动的地方，想要查看改动点对应的上下文时非常麻烦(网页上要不断的点展开)。今天给大家介绍一个我们小组内 `CodeReview` 时用到的工具及其配置，如果你有其它方式，欢迎一起交流探讨。确保配置前已安装好 `SourceTree` 以及 `Kaleidoscope`，配置方式如下

* 点击 `Kaleidoscope` 菜单 –> 点击 `Integration` –> 下载 `ksdiff`（点击 `Read More`）

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/12/7-1.jpg?raw=true)

* 安装完成之后，删除 `~/.gitconfig` 文件中 `difftool` 与 `mergetool` 相关配置（删之前最好备份一下原文件）

* 打开 `SourceTree` 的偏好设置，按下图的方式配置。两处 `Command` 都填 `/usr/local/bin/ksdiff`，`Argument` 分别为 `--partial-changeset --relative-path "$MERGED" -- "$LOCAL" "$REMOTE"` 、`--merge --output "$MERGED" --base "$BASE" -- "$LOCAL" --snapshot "$REMOTE" --snapshot`。这两个参数也可以按自己的需求来配置。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/12/7-2.jpg?raw=true)

* 以上设置完成之后可以给 `SourceTree` 加一个自定义动作，快捷键按自己的喜好设置，参数项填 `difftool -y -t sourcetree $SHA HEAD` 即可。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/12/7-3.jpg?raw=true)

以上配置完成之后就大功告成了，使用方式就是在 `SourceTree` 中选中一个非 `HEAD` 的 `commit`，然后按下快捷键，就会在 `Kaleidoscope` 打开所有改动过的文件。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/12/7-4.jpg?raw=true)