---
title: iOS 11中的New Color Set
date: 2017-09-01 00:00:00
author: Lefe_x
layout: post
---

适配 iOS 11 时意外发现个`New Color Set`，仔细研究了下，发现比较爽。

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/09/20-1-1.jpg?raw=true)

它集中管理项目中的颜色，项目中有多少颜色一目了然。不过按目前的实现方式`Color`的名字必须使用【16 进制】颜色的名字。当然你可以自己加个前缀之类的，比如：`gray_50E3C2`，这样在方法中`mtColorWithHexString:` 中去掉前缀即可。

使用的时候，直接使用：

```objc
[UIColor colorNamed:name];
```

![](https://github.com/southpeak/iOS-tech-set/blob/master/images/2017/09/20-1-2.jpg?raw=true)

但是这个方法只有在 iOS 11 以上系统有效，我们可以自己实现一个方法，或者把系统的方法替换掉。

```objc
@implementation UIColor (main)

+ (UIColor *)mtColorNamed:(NSString *)name
{
    if (name.length == 0) {
        return [UIColor clearColor];
    }
    
    NSString *cString = [[name stringByTrimmingCharactersInSet:[NSCharacterSet whitespaceAndNewlineCharacterSet]] uppercaseString];
    if (cString.length != 6) {
        return [UIColor clearColor];
    }
    
    if (@available(iOS 11.0, *)) {
        return [UIColor colorNamed:name];
    } else {
        return [self mtColorWithHexString:name];
    }
}

+ (UIColor *)mtColorWithHexString:(NSString *)color
{
    unsigned int r, g, b;
    [[NSScanner scannerWithString:[color substringWithRange:NSMakeRange(0, 2)]] scanHexInt:&r];
    [[NSScanner scannerWithString:[color substringWithRange:NSMakeRange(2, 2)]] scanHexInt:&g];
    [[NSScanner scannerWithString:[color substringWithRange:NSMakeRange(4, 2)]] scanHexInt:&b];
    
    return [UIColor colorWithRed:((CGFloat) r / 255.0f) green:((CGFloat) g / 255.0f) blue:((CGFloat) b / 255.0f) alpha:1.0f];
}

@end
```

使用时，直接调用我们自定义的方法即可：

```objc
static NSString* const k50E3C2Color = @"50E3C2";
static NSString* const k10AEFFColor = @"10AEFF";

- (void)viewDidLoad {
    [super viewDidLoad];
    
    _label = [[UILabel alloc] initWithFrame:CGRectMake(40, 100, 100, 50)];
    _label.text = k50E3C2Color;
    _label.textAlignment = NSTextAlignmentCenter;
    _label.textColor = [UIColor mtColorNamed:k10AEFFColor];
    _label.backgroundColor = [UIColor mtColorNamed:k50E3C2Color];
    [self.view addSubview:_label];
}
```
