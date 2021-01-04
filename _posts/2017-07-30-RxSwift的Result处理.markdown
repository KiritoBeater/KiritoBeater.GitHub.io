---
title: RxSwift的Result处理
tag:
- iOS
- RxSwift
---

在使用RxSwift的过程中，相信各位都遇到过一个可订阅的对象因为`sendError`而导致整个事件链释放的问题，尤其是在网络请求中。例如：
```Swift
button.rx.tap.flatMapFirst { netRequestObservable }
```
一旦请求失败，button再次点击就不会再发出网络请求了。

查找别人的解决方案，你会发现一种Result的处理方式。
简单来说就是将Error包裹在sendNext中，在.onNext中处理Error，这样既保留了sendError时整个事件链直接结束的优点，又确保了事件链不会因此而Dispose掉。
他们那边都介绍的很详尽，此处不再赘述。

本文提供一个简单的处理方式：

使用Alamofire的Result类来对ObservableType 进行 extension。无需自己实现Result类。

```Swift
import UIKit
import RxSwift
import Alamofire

public extension ObservableType {
    public func mapResult() -> Observable<Alamofire.Result<E>> {
        return flatMap { Observable.just( Alamofire.Result.success($0)) }
            .catchError { Observable.just( Alamofire.Result.failure($0)) }
    }
}

```

使用的时候，在适当的时候（一般是订阅之前）.mapResult 即可
```Swift
_ = button.rx.tap.flatMapFirst { netRequestObservable }.mapResult()
    .subscribe(
        onNext: { [weak self] (result) in
            if result.isSuccess {
                print(result.value)
            } else {
                print(result.error)
            }
        }
    )
```
