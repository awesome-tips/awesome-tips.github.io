---
title: iOS 清理 cookies
date: 2017-11-01 00:00:00
author: 知识小集成员
cover: true
---

iOS 清理 cookies
----------

在手机端开发 `web` 页面时，有时候我们可能需要删除一些 `cookie` 值。JS 删除 `cookie` 主要是将 `cookie` 的 `expires` 属性设置为一个早于当前时间的值。不过如果 `cookie` 是 `HttpOnly` 的话，表示这个 `cookie` 值不能通过非 `HTTP` 方式来访问，而无法通过 JS 来访问，`document.cookie` 获取不到，所以也无法通过 JS 来删除这样的 `cookie` 值。

不过除了通过 `server` 端来处理外，我们也可以借助 `native` 端来执行删除操作。iOS 端使用 `NSHTTPCookie` 对象来表示一个 `cookie` ，并通过 `NSHTTPCookieStorage` 来管理当前应用的所有 `cookie`，包括 `HttpOnly/secure` 类型的 `cookie` 。所有想要删除 `cookie` ，只需要依据给定的条件(如域、path等属性)来找出对应的 `NSHTTPCookie` 对象，并删除就行。以下代码是清空当前应用程序所有 `cookie` 的操作：

```objc
NSArray<NSHTTPCookie *> *cookies = [NSHTTPCookieStorage sharedHTTPCookieStorage].cookies;
for (NSHTTPCookie *cookie in cookies) {
	[[NSHTTPCookieStorage sharedHTTPCookieStorage] deleteCookie:cookie];
}
```

当然，如果要在 `web` 端触发操作，还需要提供 `Hybrid` 接口。