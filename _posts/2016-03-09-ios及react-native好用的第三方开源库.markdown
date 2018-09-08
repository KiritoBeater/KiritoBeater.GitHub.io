---
title: iOS及React Native好用的第三方开源库
layout: post
date: 2016-03-09 22:23
category: blog
tag:
- Objective-C
- Swift
- React-Native
---

iOS开发中object-c，swift及React Native好用的第三方开源库（持续更新）


## iOS

### 功能类

#### 网络请求
- [AFNetworking](https://github.com/AFNetworking/AFNetworking) (Objective-C)
- [Alamofire](https://github.com/Alamofire/Alamofire) (Swift)

#### 网络图片
- [SDWebImage](https://github.com/rs/SDWebImage) (Objective-C)
- [Kingfisher](https://github.com/onevcat/Kingfisher) （Swift）

#### Model映射
- [SwiftyJSON](https://github.com/SwiftyJSON/SwiftyJSON) 方便的json读取
- [ObjectMapper](https://github.com/Hearst-DD/ObjectMapper)
- [MJExtension](https://github.com/CoderMJLee/MJExtension)

#### 响应式编程
- [ReactiveCocoa](https://github.com/ReactiveCocoa/ReactiveCocoa) 可以支持OC
- [RxSwift](https://github.com/ReactiveX/RxSwift) 
- [RxAlamofire](https://github.com/RxSwiftCommunity/RxAlamofire) Rx网络请求
- [RxOptional](https://github.com/RxSwiftCommunity/RxOptional) Rx可选转换

#### KVO
- [KVOController](https://github.com/facebook/KVOController)

#### Cell高度自适应
- [UITableView-FDTemplateLayoutCell](https://github.com/forkingdog/UITableView-FDTemplateLayoutCell)

#### 蓝牙通讯
- [YmsCoreBluetooth](https://github.com/kickingvegas/YmsCoreBluetooth)

#### 键盘遮挡
- [TPKeyboardAvoiding](https://github.com/michaeltyson/TPKeyboardAvoiding)

#### 图片处理
- [GPUImage](https://github.com/BradLarson/GPUImage)
- [MWPhotoBrowser](https://github.com/mwaterfall/MWPhotoBrowser)
- [SwiftyImage](https://github.com/devxoul/SwiftyImage) 

#### Runtime
- [Aspects](https://github.com/steipete/Aspects)

#### 缓存
- [PINCache](https://github.com/pinterest/PINCache)

#### 数据库
- [fmdb](https://github.com/ccgus/fmdb)

#### 扫码类
- [ZXingObjC](https://github.com/TheLevelUp/ZXingObjC)

#### 应用内购买
- [RMStore](https://github.com/robotmedia/RMStore) (OC)
- [SwiftyStoreKit](https://github.com/bizz84/SwiftyStoreKit) (Swift)

#### 钥匙链存储
- [SSKeychain](https://github.com/soffes/sskeychain)

#### 性能优化
- [Texture](https://github.com/TextureGroup/Texture) 异步渲染框架（原AsyncDisplayKit）

#### 时间处理
- [SwiftDate](https://github.com/malcommac/SwiftDate) (Swift)

#### 加密处理
- [CryptoSwift](https://github.com/krzyzanowskim/CryptoSwift) (Swift)
> Swift 不能直接引入CommonCrypto, CryptoSwift自己实现了一套

#### 私有API
- [iOS-Runtime-Headers](https://github.com/nst/iOS-Runtime-Headers) 

#### 网络状态
- [Reachability](https://github.com/tonymillion/Reachability)
- [Reachability.swift](https://github.com/ashleymills/Reachability.swift)

#### 简化Frame
- [UIView-Positioning](https://github.com/freak4pc/UIView-Positioning) Swift

#### Socket
- [SocketIO-Client-CPP](https://github.com/socketio/socket.io-client-cpp) OC用，C++
- [socket.io-client-swift](https://github.com/socketio/socket.io-client-swift)

### 视图类

#### HUD
- [SVProgressHUD](https://github.com/SVProgressHUD/SVProgressHUD) 易用HUD
- [JGProgressHUD](https://github.com/JonasGessner/JGProgressHUD)  适用于自己封装
- [MBProgressHUD](https://github.com/jdg/MBProgressHUD)           适用于自己封装
- [Toast-Swift](https://github.com/scalessec/Toast-Swift)
- [Toast](https://github.com/scalessec/Toast)
> Toast 不方便的地方是不能去阻断交互，需要自己处理

#### 弹出框组件
- [MMPopupView](https://github.com/adad184/MMPopupView)

#### Cell侧滑
- [MGSwipeTableCell](https://github.com/MortimerGoro/MGSwipeTableCell)
- [SWTableViewCell](https://github.com/CEWendel/SWTableViewCell)

#### 侧滑视图
- [RESideMenu](https://github.com/romaonthego/RESideMenu)
- [ECSlidingViewController](https://github.com/ECSlidingViewController/ECSlidingViewController)
- [SlideMenuControllerSwift](https://github.com/dekatotoro/SlideMenuControllerSwift) (Swift)

#### Tabbar
- [CYLTabBarController](https://github.com/ChenYilong/CYLTabBarController)

#### 日历
- [PDTSimpleCalendar](https://github.com/jivesoftware/PDTSimpleCalendar)
- [JTAppleCalendar](https://github.com/patchthecode/JTAppleCalendar)

#### 表格
- [ios-charts](https://github.com/danielgindi/ios-charts)

#### 背景虚化
- [FXBlurView](https://github.com/nicklockwood/FXBlurView)

#### 输入框
- [SlackTextViewController](https://github.com/slackhq/SlackTextViewController) 评论输入框

#### CoreText
- [DTCoreText](https://github.com/Cocoanetics/DTCoreText)

#### Block
- [BlocksKit](https://github.com/zwaldowski/BlocksKit)

#### 下拉刷新
- [MJRefresh](https://github.com/CoderMJLee/MJRefresh)
- [DGElasticPullToRefresh](https://github.com/gontovnik/DGElasticPullToRefresh) 下拉刷新 (Swift)

#### 动画
- [UIView-Animation-Extensions](https://github.com/r3econ/UIView-Animation-Extensions)
- [pop](https://github.com/facebook/pop)
- [JazzHands](https://github.com/IFTTT/JazzHands)

#### 轮播图
- [SDCycleScrollView](https://github.com/gsdios/SDCycleScrollView)

#### 星星条
- [DJWStarRatingView](https://github.com/danwilliams64/DJWStarRatingView)
- [Cosmos](https://github.com/evgenyneu/Cosmos) (Swift)
> Note 更圆滑的🌟🌟
```Swift
let mStarPoints = [
    CGPoint(x: 50.0,  y: 0.0),
    CGPoint(x: 64.5,  y: 30.0),
    CGPoint(x: 97.5,  y: 34.5),
    CGPoint(x: 74.0,  y: 58.0),
    CGPoint(x: 79.5,  y: 90.5),
    CGPoint(x: 50.0,  y: 75.0),
    CGPoint(x: 20.5,  y: 90.5),
    CGPoint(x: 26.0,  y: 58.0),
    CGPoint(x: 2.5,   y: 34.5),
    CGPoint(x: 35.5,  y: 30.0)
]
```

#### UIStackView
- [FDStackView](https://github.com/forkingdog/FDStackView)

#### 导航栏
- [FDFullscreenPopGesture](https://github.com/forkingdog/FDFullscreenPopGesture)
- [KMNavigationBarTransition](https://github.com/MoZhouqi/KMNavigationBarTransition)

#### 布局类
- [Masonry](https://github.com/SnapKit/Masonry) (Objective-C)
- [SnapKit](https://github.com/SnapKit/SnapKit) (Swift)

#### Interface Builder
- [IBAnimatable](https://github.com/IBAnimatable/IBAnimatable) (Swift)

#### 广告页
- [XHLaunchAd](https://github.com/CoderZhuXH/XHLaunchAd) 开屏广告页

#### 原生分享
- [MonkeyKing](https://github.com/nixzhu/MonkeyKing) (Swift)

#### UICollectionViewLayout
- [UICollectionViewLeftAlignedLayout](https://github.com/mokagio/UICollectionViewLeftAlignedLayout) 左对齐

#### 选项卡
- [VTMagic](https://github.com/tianzhuo112/VTMagic) 左右滑动分页控制器
- [HMSegmentedControl](https://github.com/HeshamMegid/HMSegmentedControl) 选项卡

#### 直播和视频播放
- [PLPlayerKit](https://github.com/pili-engineering/PLPlayerKit) 播放器，挺干净的。
- [PLMediaStreamingKit](https://github.com/pili-engineering/PLMediaStreamingKit) 直播推流

### 其他
- [YYKit](https://github.com/ibireme/YYKit)


## React Native

#### 导航
- [react-navigation](https://github.com/react-community/react-navigation)
