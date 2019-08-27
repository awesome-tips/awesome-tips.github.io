---
title: WKWebView检测首屏渲染时间
date: 2017-09-01 00:00:00
author: 知识小集成员
layout: post
---

调研了一下`WKWebView`如何检测首屏渲染的时间，经过阅读`WebKit`源码和尝试，发现这样可以（需要调用私有方法，可以`base64`加密一下）：

```objc
// 注册
[self.webview performSelectorOnMainThread:@selector(_setObservedRenderingProgressEvents:) withObject:@(127) waitUntilDone:NO];

// 回调
- (void)_webView:(WKWebView *)webView renderingProgressDidChange:(int)progressEvents {
    // progressEvents == 64 表示首屏渲染结束
}
```

