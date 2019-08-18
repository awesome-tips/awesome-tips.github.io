---
title: 动态修改应用程序的icon
date: 2018-01-01 00:00:00
author: 南峰子_老驴
cover: true
---

动态修改应用程序的icon
--------
**作者**: [南峰子_老驴](https://weibo.com/touristdiary)


偶然看到 `Price Tag` 有个替换应用图标的功能，如图，研究了一下。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/3-1.png?raw=true)

这个功能是在 `iOS 10.3` 后新增的，主要的 `API` 如下所示：

```objc
@interface UIApplication (UIAlternateApplicationIcons)
// If false, alternate icons are not supported for the current process.
@property (readonly, nonatomic) BOOL supportsAlternateIcons NS_EXTENSION_UNAVAILABLE("Extensions may not have alternate icons") API_AVAILABLE(ios(10.3), tvos(10.2));

// Pass `nil` to use the primary application icon. The completion handler will be invoked asynchronously on an arbitrary background queue; be sure to dispatch back to the main queue before doing any further UI work.
- (void)setAlternateIconName:(nullable NSString *)alternateIconName completionHandler:(nullable void (^)(NSError *_Nullable error))completionHandler NS_EXTENSION_UNAVAILABLE("Extensions may not have alternate icons") API_AVAILABLE(ios(10.3), tvos(10.2));

// If `nil`, the primary application icon is being used.
@property (nullable, readonly, nonatomic) NSString *alternateIconName NS_EXTENSION_UNAVAILABLE("Extensions may not have alternate icons") API_AVAILABLE(ios(10.3), tvos(10.2));
@end
```

只读属性 `supportsAlternateIcons` 用于判断系统是否允许修改 `App` 图标，只有在允许的情况下才能修改。`-setAlternateIconName:completionHandler:` 用于执行修改操作，如果 `iconName` 设置为 `nil`，则恢复为主图标，使用方式如下代码所示：

```objc
- (IBAction)changeIcon:(UIButton *)sender {
    if ([[UIApplication sharedApplication] supportsAlternateIcons]) {
        
        NSString *iconName = nil;
        if (sender.tag == 1) {
            iconName = @"rocket";
        } else if (sender.tag == 2) {
            iconName = @"pin";
        }
        
        [[UIApplication sharedApplication] setAlternateIconName:iconName completionHandler:^(NSError * _Nullable error) {
            
        }];
    }
}
```

除了调用 `API` 外，最主要的还需要在 `info.plist` 中配置 `CFBundleIcons` 项，这是一个字典，可包含 `CFBundlePrimaryIcon`、`CFBundleAlternateIcons`、`UINewsstandIcon` 三个键。

`CFBundlePrimaryIcon` 为主图标，即 `Assets.xcassets` 中 `AppIcon` 的信息，一般置空。`CFBundleAlternateIcons` 即用于设置替换图标，具体的配置项描述可以参考[官方文档](https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html) ，通常的配置如图所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/3-2.png?raw=true)

这里需要注意的是，替换图标应该放在工程的某个目录下，而不放在 `Assets.xcassets` 中，如图所示。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2018/01/3-3.png?raw=true)