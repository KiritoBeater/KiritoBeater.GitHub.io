---
tag:
- Tool
---

关于CocoaPods的一些略微高级一些的使用技巧。

> Mac OSX 10.11 以后升级CocoaPods权限问题. 1.升级Gem:sudo gem update --system 2. 安装Cocoapods：sudo gem install -n /usr/local/bin cocoapods

* 建立Podfile文件

    建议init后直接执行pod install，然后在打开的Xcode中修改Podfile文件。

        pod init

* 指定平台版本

    pod init会自动生成，解注释即可。

        platform :ios, '8.0'

* 使用Dynamic Frameworks代替Static Libraries

    通过标志use_frameworks!就可知开启这个功能。如果需要使用Swift的库，就必须加上这个标志了。

    同上，pod init会自动生成，解注释即可。

        use_frameworks!

* 指定target的依赖库

    pod init自动生成的格式。

        target :ZipApp do   
            pod 'SSZipArchive'
        end

* 排除target

        target 'Artsy Tests', :exclusive => true do   
            pod 'FBSnapshotTestCase', '1.4'
        end

* 指定源

    官方源的速度略慢。可以通过使用国内源。

    也可以通过指定源使用私有Pod。

        source 'https://github.com/CocoaPods/Specs.git'   //官方源
        source 'https://git.coding.net/hging/Specs.git'   //coding源
        source 'http://git.oschina.net/akuandev/Specs'    //oschina源

* 抑制警告

    inhibit_warnings参数能够有效的抑制CocoaPods引入的第三方代码库产生的warning。

    全部指定

        inhibit_all_warnings!

    针对指定。

        pod 'ReactiveCocoa', '~> 2.4', :inhibit_warnings => true

* 使用 master 分支

        pod 'ARAnalytics/Mixpanel', :git => 'https://github.com/gowalla/AFNetworking.git'

* 指定branch

        pod 'Reachability', :git => 'https://github.com/gowalla/AFNetworking.git', :branch => 'dev'

* 指定tag

        pod 'AFNetworking', :git => 'https://github.com/gowalla/AFNetworking.git', :tag => '0.7.0'

* 指定commit

        pod 'ARTiledImageView', :git => 'https://github.com/dblockARTiledImageView', :commit => '1a31b864d1d56b1aaed0816c10bb55cf2e078bb8'

* 使用子库

        pod 'QueryKit/Attribute'
        pod 'QueryKit', :subspecs => ['Attribute', 'QuerySet'] //多个子库

* 使用本地代码

    通过:path可以指定本地代码，不过需要确保目录包含podspec文件。
    在实际开发中使用私有Pod时，可以先使用本地代码，每次私有Pod修改后，可以直接pod update '私有pod' 更新，开发完成后再更新私有pod版本。

        pod 'AFNetworking', :path => '~/Documents/AFNetworking'

* 指定xcodeproj

    默认会使用Podfile文件同级目录下第一个xcodeproj，但也可以指定

        xcodeproj 'MyProject'

        target :test do   
            # This Pods library links with a target in another project.
            xcodeproj 'TestProject'
        end

* 指定连接的target

    如果不显式指定连接的target，Pods会默认连接project的第一个target。如果需要，可以使用link_with指定连接一个或多个target

        link_with 'MyApp', 'MyOtherApp'

* 指定环境

    如下只会在Debug环境下面加入PonyDebugger库到工程。

        pod 'PonyDebugger', :configuration => ['Debug']

* 指定target的配置文件

        xcodeproj 'TestProject', 'Mac App Store' => :release, 'Test' => :debug

* 加快pod install/update 速度

    使用CocoaPods来添加第三方类库，无论是执行pod install还是pod updat很多时候都卡在了Analyzing dependencies不动，这是更新本地的pod spec所以文件导致的。通过--no-repo-update标志可以不更新本地pod spec索引。当然首次install不应该添加这个标志，后续修改Podfile的时候可以适当使用，加快pod速度。

        pod install --no-repo-update   
        pod update --no-repo-update  

* 输出详细日志

        pod update --verbose

参考：[CocoaChina：CocoaPods的一些略为高级一丁点的使用](http://www.cocoachina.com/ios/20150916/13384.html)
