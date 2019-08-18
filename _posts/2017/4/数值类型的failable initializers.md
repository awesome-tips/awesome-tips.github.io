---
title: 数值类型的failable initializers
date: 2017-04-01 00:00:00
author: 知识小集成员
cover: true
---

数值类型的failable initializers
---------

`Swift 3.1`为数值类型(`Int, Int8, Int16, Int32, Int64, UInt, UInt8, UInt16, UInt32, UInt64, Float, Float80, Double`)实现了`failable initializers: init?(exactly value:)`。这些`initializer`在创建数值类型失败时会返回`nil`，对于处理一些从诸如`json`这样松散的数据类型的数值时非常有用。

如下代码是[raywenderlich]((https://www.raywenderlich.com/156352/whats-new-in-swift-3-1))中的一段示例。

```swift
class Student {
  let name: String
  let grade: Int

  init?(json: [String: Any]) {
    guard let name = json["name"] as? String,
          let gradeString = json["grade"] as? String,
          let gradeDouble = Double(gradeString),
          let grade = Int(exactly: gradeDouble)  // <-- 3.1 feature here
    else {
        return nil
    }
    self.name = name
    self.grade = grade
  }
}

func makeStudents(with data: Data) -> [Student] {
  guard let json = try? JSONSerialization.jsonObject(with: data, options: .allowFragments),
        let jsonArray = json as? [[String: Any]] else {
    return []
  }
  return jsonArray.flatMap(Student.init)
}

let rawStudents = "[{\"name\":\"Ray\", \"grade\":\"5.0\"}, {\"name\":\"Matt\", \"grade\":\"6\"},
                    {\"name\":\"Chris\", \"grade\":\"6.33\"}, {\"name\":\"Cosmin\", \"grade\":\"7\"},
                    {\"name\":\"Steven\", \"grade\":\"7.5\"}]"
let data = rawStudents.data(using: .utf8)!
let students = makeStudents(with: data)
dump(students) // [(name: "Ray", grade: 5), (name: "Matt", grade: 6), (name: "Cosmin", grade: 7)]
```

这里过滤了`json`中`grade`值转换成`Int`值时不准确的数据。

参考

1. [What’s New in Swift 3.1?](https://www.raywenderlich.com/156352/whats-new-in-swift-3-1)
2. [Swift evolution: Failable Numeric Conversion Initializers](https://github.com/apple/swift-evolution/blob/master/proposals/0080-failable-numeric-initializers.md)