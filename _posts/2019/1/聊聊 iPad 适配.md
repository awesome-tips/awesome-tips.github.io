---
title: 聊聊 iPad 适配
date: 2019-01-01 00:00:00
author: halohily
cover: true
---

聊聊 iPad 适配
--------
**作者**: [halohily](https://weibo.com/halohily)

在最新版本中，我们为网易有道词典做了完全的 iPad 适配，你可以在 iPad 上横屏、分屏使用有道词典，也完全支持了屏幕旋转后的 UI 调整。今天来聊聊这次的适配体验。

千言万语总结成一句话：如果你正确使用了 `autolayout`（使用比例而非固定值），那么即使是原本仅支持竖屏的页面，在打开转屏开关后，页面也不会有太大的问题。况且苹果已经提升了 `autolayout` 的性能，所以如果你的 app 未来有支持 iPad 的潜在可能，那么尽可能地全部使用 `autolayout` 来布局吧。

如果现有的大量页面都已经使用了计算 `frame` 的方式来布局，也有解决办法。`UIView` 的子类 要保证在 `layoutSubviews` 方法内进行布局（根据 self 宽高而不是屏幕或 window 尺寸），这本来也是一个标准做法。对于 `ViewController`，系统提供了 `viewWillLayoutSubviews` 方法，类似于 `layoutSubviews`方法，你可以在这里进行 `vc.view` 及其子 `view` 的布局。在转屏、分屏后这些方法都会被触发。

需要注意的是，iPad 上不仅有旋转屏幕的操作，还有分屏的操作，系统也提供了进入分屏的系统通知，如果需要可以进行监听。比如大多数拍照 app 会在进入分屏后为用户弹一个分屏无法拍照的 `alert`。