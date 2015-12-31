layout: [post]
title: "iOS GCD 的简单使用介绍"
date: 2015-07-19 17:41:33
tags: 
- iOS
categories: 
- iOS
- 笔记
id: "GCDIntro"
---

Asynchronous Operations in iOS with Grand Central Dispatch 的笔记。

<!-- more -->

---



# 正文

[原文地址](http://jeffreysambells.com/2013/03/01/asynchronous-operations-in-ios-with-grand-central-dispatch)

> 使用 GCD 可以轻松的在 iOS 执行异步操作。
> 当执行长时间的运算而不想界面卡死时可以用到 GCD。

Grand Central Dispatch, or GCD for short, is a **C API** that makes it exceptionally easy to **perform asynchronous operations in iOS**. Asynchronous operations are a fundamental part of every iOS app when you want to **perform long operations without freezing or blocking the user interface**. You can image that if your entire app froze without warning then your users would get quite irritated.。

* blocks 或 operations 会分配到其它线程执行任务。
* 主 UI 线程可以继续执行它的任务，如 UI 响应和手势检测。
* GCD 队列可以并发执行或串联执行(一个完成后接着另一个继续执行)
* dispatch_get_main_queue 对于使用 UIKit 方法更新 iOS 应用程序的 UI 非常有用，但不是线程安全的，所以任何你所做的更新 UI 元素的调用必须始终在 main queue 中完成。
* 一旦 block 被分配到 queue 中，它将不可能被暂停，在它执行完成之前你什么都做不了。如果你有长时间运行的任务，如加载 URL，你应该在每个步骤之间添加逻辑检测判断它是否应该继续执行。

With GCD, you can **line up blocks of code** in a queue for the system to execute as necessary. These blocks or operations, will be dispatched in the queue to **another thread**, **leaving your main UI thread** to continue its tasks. It’s important to know that GCD will use separate threads for it’s operations but which thread it isn’t important to you. All that matters is that your long running process in a separate thread outside the main thread where your UI and gestures are running.

GCD queues can be concurrent or serial but serial queues (where there is one queue and each item is executed one after the other in order) are easier to understand so we’ll look at those.

The more important functions you’ll need are for creating the queue:

```objc
//创建一个 queue
dispatch_queue_t dispatch_queue_create(const char *label, dispatch_queue_attr_t attr); 

```

and adding blocks to the queue:

```objc
//向 queue 分配 block
void dispatch_async(dispatch_queue_t queue, dispatch_block_t block);

```

There’s also a couple helper functions for retrieving specific queues such as:

```objc
//两个辅助使用的特殊 queue
dispatch_queue_t dispatch_get_current_queue(void);//将 block 分配到当前的队列
dispatch_queue_t dispatch_get_main_queue(void);// 将 block 分配到 UI 主线程

```

The `dispatch_get_current_queue` function will return the current queue from which the block is dispatched and the `dispatch_get_main_queue` function will return the main queue where your UI is running.

The `dispatch_get_main_queue` function is **very useful for updating the iOS app’s UI as UIKit methods are not thread safe** (with a few exceptions) so any calls you make to update UI elements **must always be done **from the main queue.

A typical GCD call would look something like this:

```objc

// Doing something on the main thread

//创建自定义 queue
dispatch_queue_t myQueue = dispatch_queue_create("My Queue",NULL);
dispatch_async(myQueue, ^{
    // Perform long running process
    
    //在主 UI queue 更新界面
    dispatch_async(dispatch_get_main_queue(), ^{
        // Update the UI
        
    });
}); 

// Continue doing other stuff on the 
// main thread while process is running.

```

GCD relies on block so it has a really nice, readable syntax. It becomes clear what happes in the background thread and the main thread. For example, here’s how you might load a few images

```objc
//在 background thread 加载图片，加载完成后使用 dispatch_get_main_queue 更新 main UI 界面
NSArray *images = @[@"http://example.com/image1.png",
                 @"http://example.com/image2.png",
                 @"http://example.com/image3.png",
                 @"http://example.com/image4.png"];

dispatch_queue_t imageQueue = dispatch_queue_create("Image Queue",NULL);

for (NSString *urlString in images) {
    dispatch_async(imageQueue, ^{
        
        NSURL *url = [NSURL URLWithString:urlString];
        NSData *imageData = [NSData dataWithContentsOfURL:url];
        UIImage *image = [UIImage imageWithData:imageData];

        NSUInteger imageIndex = [images indexOfObject:urlString];
        UIImageView *imageVIew = (UIImageView *)[self.view viewWithTag:imageIndex];
        
        if (!imageView) return;
        
        dispatch_async(dispatch_get_main_queue(), ^{
            // Update the UI
            [imageVIew setImage:image];
        });
        
    }); 
}

// Continue doing other stuff while images load.

```

You’ll notice I check for imageView before dispatching to the main thread. This avoids the main queue dispatch if the network request took a long time and the imageView is no longer there for one reason or another. **Once a block has been dispatched onto a queue, it’s not possible to stop it. **The block will execute to completion and there’s nothing you can do. If you have a very long running process, such as loading a URL, you should add logic between each step to check to see if it should continue and if it’s still appropriate to finish the operation.

# Aside: Concurrency

If you want to run a single independent queued operation and you’re not concerned with other concurrent operations, you can use the global concurrent queue:

```objc
dispatch_queue_t globalConcurrentQueue =
dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0)

```

This will return a concurrent queue with the given priority as outlined in the documentation:


 MARCH 01, 2013
 PERMALINK
Grand Central Dispatch, or GCD for short, is a C API that makes it exceptionally easy to perform asynchronous operations in iOS. Asynchronous operations are a fundamental part of every iOS app when you want to perform long operations without freezing or blocking the user interface. You can image that if your entire app froze without warning then your users would get quite irritated.

With GCD, you can line up blocks of code in a queue for the system to execute as necessary. These blocks or operations, will be dispatched in the queue to another thread, leaving your main UI thread to continue its tasks. It’s important to know that GCD will use separate threads for it’s operations but which thread it isn’t important to you. All that matters is that your long running process in a separate thread outside the main thread where your UI and gestures are running.

GCD queues can be concurrent or serial but serial queues (where there is one queue and each item is executed one after the other in order) are easier to understand so we’ll look at those.

The more important functions you’ll need are for creating the queue:

dispatch_queue_t dispatch_queue_create(const char *label, dispatch_queue_attr_t attr);
and adding blocks to the queue:

void dispatch_async(dispatch_queue_t queue, dispatch_block_t block);
There’s also a couple helper functions for retrieving specific queues such as:

dispatch_queue_t dispatch_get_current_queue(void);
dispatch_queue_t dispatch_get_main_queue(void);
The dispatch_get_current_queue function will return the current queue from which the block is dispatched and the dispatch_get_main_queue function will return the main queue where your UI is running.

The dispatch_get_main_queue function is very useful for updating the iOS app’s UI as UIKit methods are not thread safe (with a few exceptions) so any calls you make to update UI elements must always be done from the main queue.

```objc

A typical GCD call would look something like this:

// Doing something on the main thread

dispatch_queue_t myQueue = dispatch_queue_create("My Queue",NULL);
dispatch_async(myQueue, ^{
    // Perform long running process
    
    dispatch_async(dispatch_get_main_queue(), ^{
        // Update the UI
        
    });
}); 

// Continue doing other stuff on the 
// main thread while process is running.

```

GCD relies on block so it has a really nice, readable syntax. It becomes clear what happes in the background thread and the main thread. For example, here’s how you might load a few images:

```objc

NSArray *images = @[@"http://example.com/image1.png",
                 @"http://example.com/image2.png",
                 @"http://example.com/image3.png",
                 @"http://example.com/image4.png"];

dispatch_queue_t imageQueue = dispatch_queue_create("Image Queue",NULL);

for (NSString *urlString in images) {
    dispatch_async(imageQueue, ^{
        
        NSURL *url = [NSURL URLWithString:urlString];
        NSData *imageData = [NSData dataWithContentsOfURL:url];
        UIImage *image = [UIImage imageWithData:imageData];

        NSUInteger imageIndex = [images indexOfObject:urlString];
        UIImageView *imageVIew = (UIImageView *)[self.view viewWithTag:imageIndex];
        
        if (!imageView) return;
        
        dispatch_async(dispatch_get_main_queue(), ^{
            // Update the UI
            [imageVIew setImage:image];
        });
        
    }); 
}

// Continue doing other stuff while images load.
```

You’ll notice I check for imageView before dispatching to the main thread. This avoids the main queue dispatch if the network request took a long time and the imageView is no longer there for one reason or another. Once a block has been dispatched onto a queue, it’s not possible to stop it. The block will execute to completion and there’s nothing you can do. If you have a very long running process, such as loading a URL, you should add logic between each step to check to see if it should continue and if it’s still appropriate to finish the operation.

That’s it. Start build queues and making your UI more responsive.

### Aside: Concurrency

If you want to run a single independent queued operation and you’re not concerned with other concurrent operations, you can use the global concurrent queue:

```objc

dispatch_queue_t globalConcurrentQueue =
dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0)


```

This will return a concurrent queue with the given priority as outlined in the documentation:

> **DISPATCH_QUEUE_PRIORITY_HIGH** Items dispatched to the queue will run at high priority, i.e. the queue will be scheduled for execution before any default priority or low priority queue.

> **DISPATCH_QUEUE_PRIORITY_DEFAULT** Items dispatched to the queue will run at the default priority, i.e. the queue will be scheduled for execution after all high priority queues have been scheduled, but before any low priority queues have been scheduled.

> **DISPATCH_QUEUE_PRIORITY_LOW** Items dispatched to the queue will run at low priority, i.e. the queue will be scheduled for execution after all default priority and high priority queues have been scheduled.

> **DISPATCH_QUEUE_PRIORITY_BACKGROUND** Items dispatched to the queue will run at background priority, i.e. the queue will be scheduled for execution after all higher priority queues have been scheduled and the system will run items on this queue on a thread with background status as per setpriority(2) (i.e. disk I/O is throttled and the thread’s scheduling priority is set to lowest value).

> from queue.h