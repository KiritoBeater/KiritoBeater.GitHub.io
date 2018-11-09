---
title: NSOperationQueue实现等待多个请求完成后执行操作
layout: post
category: blog
tag:
- iOS
- Objective-C
---

等待多个网络请求完成后再执行操作，网上给的方案一般都是GCD的处理。这里给一个NSOperationQueue的做法，使用Operation的依赖来达到同样的效果。

示例代码如下：
```ObjectiveC
    NSURL *url = [NSURL URLWithString:@"http://www.cocoachina.com"];
    
    NSOperationQueue *aQueue = [[NSOperationQueue alloc] init];
    
    NSBlockOperation *op1 = [NSBlockOperation blockOperationWithBlock:^{
        NSLog(@"run 1");
    }];
    
    NSBlockOperation *op2 = [NSBlockOperation blockOperationWithBlock:^{
        NSLog(@"run 2");
    }];

    NSBlockOperation *op3 = [NSBlockOperation blockOperationWithBlock:^{
        NSLog(@"run 3");
    }];
    
    NSBlockOperation *finalOp = [NSBlockOperation blockOperationWithBlock:^{
        NSLog(@"run final");
    }];
    [finalOp addDependency:op1];
    [finalOp addDependency:op2];
    [finalOp addDependency:op3];
    [aQueue addOperation:finalOp];
    
    NSLog(@"rep 1");
    [[NSURLSession.sharedSession dataTaskWithURL:url completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {
        NSLog(@"res 1");
        [aQueue addOperation:op1];
    }] resume];
    
    NSLog(@"rep 2");
    [[NSURLSession.sharedSession dataTaskWithURL:url completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {
        NSLog(@"res 2");

        [aQueue addOperation:op2];
    }] resume];

    NSLog(@"rep 3");
    [[NSURLSession.sharedSession dataTaskWithURL:url completionHandler:^(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error) {
        NSLog(@"res 3");
        [aQueue addOperation:op3];
    }] resume];

```

控制台输出：
```ObjectiveC
rep 1
rep 2
rep 3
res 1
run 1
res 2
run 2
res 3
run 3
run final
```