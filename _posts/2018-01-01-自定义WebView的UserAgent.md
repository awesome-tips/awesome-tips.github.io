---
title: 自定义WebView的UserAgent
date: 2018-01-01 00:00:00
author: 拿破仑的风火轮_
layout: post
---


1. 产品需求:所有 `APP` 内的 `WebView` 访问的自家服务, 根据 `UserAgent` 自动切换显示合适的内容.
2. 思路:自定义全局的 `UserAgent` .
3. 实现代码如下:

```objc
/**
 * User-Agent 格式参照了 AFNetworking 设置
 */
- (void)customizeWebViewUserAgent {
    NSString *userAgent = nil;
    
#pragma clang diagnostic push
#pragma clang diagnostic ignored "-Wgnu"
    // User-Agent Header; see http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.43
    userAgent = [NSString stringWithFormat:@"%@/%@ (%@-WebView; iOS %@; Scale/%0.2f)", [[NSBundle mainBundle] infoDictionary][(__bridge NSString *)kCFBundleExecutableKey] ?: [[NSBundle mainBundle] infoDictionary][(__bridge NSString *)kCFBundleIdentifierKey], [[NSBundle mainBundle] infoDictionary][@"CFBundleShortVersionString"] ?: [[NSBundle mainBundle] infoDictionary][(__bridge NSString *)kCFBundleVersionKey], [[UIDevice currentDevice] model], [[UIDevice currentDevice] systemVersion], [[UIScreen mainScreen] scale]];
#pragma clang diagnostic pop
    
    if (userAgent) {
        if (![userAgent canBeConvertedToEncoding:NSASCIIStringEncoding]) {
            NSMutableString *mutableUserAgent = [userAgent mutableCopy];
            if (CFStringTransform((__bridge CFMutableStringRef)(mutableUserAgent), NULL, (__bridge CFStringRef)@"Any-Latin; Latin-ASCII; [:^ASCII:] Remove", false)) {//把不符合ASCII编码的字符,转码成ASCII编码格式
                userAgent = mutableUserAgent;
            }
        }
        
        [NSUserDefaults.standardUserDefaults registerDefaults:@{@"UserAgent": userAgent}];
    }
}

```

* `UIWebView` 和 `WkWebView` 的默认 `UserAgent` 抓包如图所示

    ![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/6-1.png?raw=true)

* 自定义 `UserAgent` 如图所示

    ![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/6-2.png?raw=true)
