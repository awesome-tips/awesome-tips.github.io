---
title: 缓存 NSDateFormatter
date: 2018-01-01 00:00:00
author: 拿破仑的风火轮_
layout: post
---


为什么要缓存 `NSDateFormatter` ?

> Creating a date formatter is not a cheap operation. If you are likely to use a formatter frequently, it is typically more efficient to cache a single instance than to create and dispose of multiple instances. One approach is to use a static variable.
> [developer.apple.com](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/DataFormatting/Articles/dfDateFormatting10_4.html)


思路: 利用 `NSCache`, 以 stringFormatter+NSLocale的localeIdentifier 为key缓存 `NSDateFormatter`. 当`UIApplicationDidReceiveMemoryWarningNotification` 或 `NSCurrentLocaleDidChangeNotification` 释放 `NSCache` 缓存的对象.

代码参考[code](https://github.com/BrooksWon/BTNSDateFormatterFactory/blob/master/BTNSDateFormatterFactory/BTNSDateFormatterFactory.m),  核心实现代码如下:

```objc
- (NSDateFormatter *)dateFormatterWithFormat:(NSString *)format andLocale:(NSLocale *)locale {
    @synchronized(self) {
        NSString *key = [NSString stringWithFormat:@"%@|%@", format, locale.localeIdentifier];
        
        NSDateFormatter *dateFormatter = [loadedDataFormatters objectForKey:key];
        if (!dateFormatter) {
            dateFormatter = [[NSDateFormatter alloc] init];
            dateFormatter.dateFormat = format;
            dateFormatter.locale = locale;
            [loadedDataFormatters setObject:dateFormatter forKey:key];
        }
        
        return dateFormatter;
    }
}
```
