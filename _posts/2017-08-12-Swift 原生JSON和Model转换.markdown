---
tag:
- Swift
---

Apple 在 Swift 4 的 Foundation 的模块中添加了对 JSON 解析成Model的原生支持。

虽然之前也有[ObjectMapper](https://github.com/Hearst-DD/ObjectMapper)和[SwiftyJSON](https://github.com/SwiftyJSON/SwiftyJSON)这样的解决方案，但是Swift 4中添加了原生支持还是不免让人兴奋，使用起来也相对方便了许多。

### 简单使用

如果你的 JSON 数据结构和你使用的 Model 对象结构一致的话，那么解析过程将会非常简单。只需要让Model声明 `Codable` 协议即可。

JSON数据：
```json
{
    "userInfos": [
        {
            "userName": "小名",
            "age": 18,
            "height": 178.56,
            "sex": true
        },
        {
            "userName": "小方",
            "age": 18,
            "height": 162.56,
            "sex": false
        }
    ]
}
```

Model对象：
```swift

struct UserList: Codable {

    let userInfos: [UserInfo]

    struct UserInfo: Codable {

        let userName: String
        let age: Int
        let height: Float
        let sex: Bool
    }
}
```

JSON转Model：
```swift
    let jsonDecoder = JSONDecoder()
    let modelObject = try? jsonDecoder.decode(UserList.self, from: jsonData)
```

Model转JSON：
```swift
    let jsonEncoder = JSONEncoder()
    let jsonData = try? jsonEncoder.encode(modelObject)
```

关于 `Codable`
```swift
/// A type that can convert itself into and out of an external representation.
public typealias Codable = Decodable & Encodable
```

`Codable` 同时声明了 `Decodable` 和 `Encodable` 两个协议，只需要单向处理的话可以只声明其中一个协议。

需要注意的是，使用时必须保证 JSON 数据结构和你使用的 Model 对象结构一致，任何不一致都会导致解析失败。

但是实际开发过程中，往往不会总是这样满足我们的需要，有时也需要我们对解析过程做一些改变。

### 自定义键值名

为了保持风格一致，我们有时候不得不改变key成为我们需要的key值。

仍然使用上面的例子，现在我们把Model中的key `height` 改为 `bodyHeight`

```swift
struct UserList: Codable {

    let userInfos: [UserInfo]
    
    struct UserInfo: Codable {
        
        let userName: String
        let age: Int
        let bodyHeight: Float
        let sex: Bool
        
        private enum CodingKeys: String, CodingKey {
            case userName
            case age
            case bodyHeight = "height"
            case sex
        }
    }
}
```

### 格式处理

`JSONEncoder` 和 `JSONDecoder` 本身也提供了对时间格式的处理，Data的处理，浮点不匹配的处理。可以根据自己的需要设置自己想要的格式。

```swift
    /// The strategy to use in decoding dates. Defaults to `.deferredToDate`.
    open var dateDecodingStrategy: JSONDecoder.DateDecodingStrategy

    /// The strategy to use in decoding binary data. Defaults to `.base64`.
    open var dataDecodingStrategy: JSONDecoder.DataDecodingStrategy

    /// The strategy to use in decoding non-conforming numbers. Defaults to `.throw`.
    open var nonConformingFloatDecodingStrategy: JSONDecoder.NonConformingFloatDecodingStrategy
```

`JSONEncoder` 在生成 JSON 的时候默认的格式是
```
{"userInfos":[{"age":18,"sex":true,"height":178.55999755859375,"userName":"小名"},{"age":18,"sex":false,"height":162.55999755859375,"userName":"小方"}]}
```

如果想要提高阅读体验, 可以设置属性 `outputFormatting`

```swift

open var outputFormatting: JSONEncoder.OutputFormatting

let jsonEncoder = JSONEncoder()
jsonEncoder.outputFormatting = .prettyPrinted

```

然后生成的JSON格式就会变成这样

```
{
  "userInfos" : [
    {
      "age" : 18,
      "sex" : true,
      "height" : 178.55999755859375,
      "userName" : "小名"
    },
    {
      "age" : 18,
      "sex" : false,
      "height" : 162.55999755859375,
      "userName" : "小方"
    }
  ]
}
```

### JSON中 没有 Model 所需要的 Key

如果JSON的数据结构中，有些 Key - Value 不一定出现，Model中对应的要实用可选类型

JSON数据：
```json
{
    "userInfos": [
        {
            "userName": "小名",
            "age": 18,
            "sex": true
        },
        {
            "userName": "小方",
            "age": 18,
            "height": 162.56,
            "sex": false
        }
    ]
}
```

Model对象：
```swift

struct UserList: Codable {

    let userInfos: [UserInfo]

    struct UserInfo: Codable {

        let userName: String
        let age: Int
        let height: Float?
        let sex: Bool
    }
}
```

#### 参考:
* [Using JSON with Custom Types](https://developer.apple.com/documentation/foundation/archives_and_serialization/using_json_with_custom_types) 附 [Apple Playground](https://docs-assets.developer.apple.com/published/3025f0dbf0/UsingJSONwithCustomTypes.zip)
* [Swift 4 JSON 解析指南](https://bignerdcoding.com/archives/37.html)

