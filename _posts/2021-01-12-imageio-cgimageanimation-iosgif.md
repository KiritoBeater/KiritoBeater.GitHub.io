---
title: ImageIO - CGImageAnimation iOS原生GIF图片显示
category: blog
tag:
- ImageIO
---

一直以来，iOS显示动图都是一件很麻烦的事情，鉴于手写代码的繁琐，借助第三方几乎时不可避免的事情，然而从现在开始，苹果的`ImageIO/CGImageAnimation`提供了原生的动图图片解析和播放。
### Demo
先看具体的使用，基本上就一行代码
```swift
import ImageIO

let imageView = UIImageView();

if let gifURL = Bundle.main.url(forResource: "aImage", withExtension: "gif") {
    // 使用GIF的URL加载动图
    let gifCURL = gifURL as CFURL
    CGAnimateImageAtURLWithBlock(gifCURL, nil) { (index, image, stop) in
        imageView.image = UIImage(cgImage: image)
    }
    
    // Or: 使用GIF的Data加载动图
    do {
        let gifData = try Data(contentsOf: gifURL)
        let gifCData = gifData as CFData
        CGAnimateImageDataWithBlock(gifCData, nil) { (index, image, stop) in
            imageView.image = UIImage(cgImage: image)
        }
    } catch _ {
        
    }
}

```

### 详解
##### API
接下来，详细说一下相关的API
> * `@available(iOS 13.0, *)` iOS 13 系统起可用
> * 相关API仅支持`GIF`和`APNG`格式的图片


```swift
public typealias CGImageSourceAnimationBlock = (Int, CGImage, UnsafeMutablePointer<Bool>) -> Void

public func CGAnimateImageAtURLWithBlock(_ url: CFURL, _ options: CFDictionary?, _ block: @escaping CGImageSourceAnimationBlock) -> OSStatus

public func CGAnimateImageDataWithBlock(_ data: CFData, _ options: CFDictionary?, _ block: @escaping CGImageSourceAnimationBlock) -> OSStatus
```

方法仅传入动图的`URL`地址或二进制数据`Data`即可，当然因为是c函数，要转成`CFURL` 和 `CFData`

##### CGImageSourceAnimationBlock
`CGImageSourceAnimationBlock` 参数分别为
* `index`
当前显示帧的索引

* `image`
当前的图片

* `stop`
是否是最后一张图

##### options
`options`是播放动态时的额外的配置，有三个`Key`
* `kCGImageAnimationStartIndex`
动图从第几帧开始播放，默认是0

* `kCGImageAnimationDelayTime`
动图每帧之间的间隔，会覆盖动图原有的间隔（动图原有的每帧之间的时间间隔可以不同，这个属性会统一成同一间隔）

* `kCGImageAnimationLoopCount`
动图的循环次数，会覆盖动图原有的循环次数（一般是无限次）

##### OSStatus
调用的返回结果，成功时为`0`。以下是一些调用失败时可以使用的枚举`CGImageAnimationStatus`
```swift
public enum CGImageAnimationStatus : OSStatus {

    case parameterError /* NULL or invalid parameter passed to API */

    case corruptInputImage /* An image cannot be read from the given source */

    case unsupportedFormat /* The image format is not applicable to animation */

    case incompleteInputImage /* An image can be read from the given source, but it is incomplete */

    case allocationFailure /* A required resource could not be created */
}
```
