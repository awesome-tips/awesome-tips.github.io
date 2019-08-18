---
title: Swift 4.0 中 Dictionary 编码成类数组结构的字符串
date: 2017-12-01 00:00:00
author: 知识小集成员
cover: true
---

Swift 4.0 中 Dictionary 编码成类数组结构的字符串
----

在Swift 4.0中，使用`Codable`来编码一个`Dictionary`时，某些情况下得到的可能并不是类似于字典/对象结构的字符串，而可能是一个类似数组结构的字符串，如下代码所示：

```swift
let dict: [Float : String] = [
    18.0: "ff0000",
    20.0: "00ff00",
    21.0: "0000ff"
]

let encoder = JSONEncoder()
encoder.outputFormatting = [.prettyPrinted, .sortedKeys]
let encoded = try! encoder.encode(dict)
let jsonText = String(decoding: encoded, as: UTF8.self)
print(jsonText)

//[
//  21,
//  "0000ff",
//  18,
//  "ff0000",
//  20,
//  "00ff00"
//]
```

这里的`dict`以`Float`类型为`key`，结果是输出一个类似数组的字符串。查看源码中`Dictionary`对`Encodable`协议的扩展实现，如下代码所示：

```swift
extension Dictionary : Encodable /* where Key : Encodable, Value : Encodable */ {
    public func encode(to encoder: Encoder) throws {
        assertTypeIsEncodable(Key.self, in: type(of: self))
        assertTypeIsEncodable(Value.self, in: type(of: self))

        if Key.self == String.self {
            // Since the keys are already Strings, we can use them as keys directly.
            var container = encoder.container(keyedBy: _DictionaryCodingKey.self)
            for (key, value) in self {
                let codingKey = _DictionaryCodingKey(stringValue: key as! String)!
                try (value as! Encodable).__encode(to: &container, forKey: codingKey)
            }
        } else if Key.self == Int.self {
            // Since the keys are already Ints, we can use them as keys directly.
            var container = encoder.container(keyedBy: _DictionaryCodingKey.self)
            for (key, value) in self {
                let codingKey = _DictionaryCodingKey(intValue: key as! Int)!
                try (value as! Encodable).__encode(to: &container, forKey: codingKey)
            }
        } else {
            // Keys are Encodable but not Strings or Ints, so we cannot arbitrarily convert to keys.
            // We can encode as an array of alternating key-value pairs, though.
            var container = encoder.unkeyedContainer()
            for (key, value) in self {
                try (key as! Encodable).__encode(to: &container)
                try (value as! Encodable).__encode(to: &container)
            }
        }
    }
}
```

可以看到当 `key` 的类型为 `String` 和 `Int` 时，使用 `_DictionaryCodingKey` 来编码 `key`，进而编码 `key-value` 对，最后以类似字典的结构输出(依赖于 `keyed container` )，这是因为在 `Codable` 系统中，这两个类型是有效的可编码 `key` 类型；而其它类型则不是，由于 `Dictionary` 无法告诉其它类型如何编码自身，所以将这些值 `key` 存储在一个 `unkeyed container` 中，最终处理成一个数组。

参考：

1. [UnkeyedEncodingContainer](https://developer.apple.com/documentation/swift/unkeyedencodingcontainer)
2. [Why Dictionary sometimes encodes itself as an array](https://oleb.net/blog/2017/12/dictionary-codable-array/)