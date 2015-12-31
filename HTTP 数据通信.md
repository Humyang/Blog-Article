layout: [post]
title: "HTTP 数据通信"
date: 2015-07-19 22:24:58
tags: 
- iOS
categories: 
- iOS
- 备忘
id: "HTTP-data-communication"
---

记录了如何读取网页数据，如何与服务器交互。

<!-- more -->


---

# HTTP 数据通信

## 读取网页的数据

### 读取网页数据保存为字符串

```swift

        //将网页内容读取成字符串
        var str = NSString(contentsOfURL: NSURL(string:"http://www.jikexueyuan.com")!, encoding: NSUTF8StringEncoding, error: nil)
        
        println(str)

```

### 读取网页数据保存为二进制数据

```swift

//        将网页内容读取成二进制
        var data = NSData(contentsOfURL: NSURL(string: "http://www.jiekexueyuan.com")!)
        
        println(data)
        
        //解码为字符串
        
        println(NSString(data: data!, encoding: NSUTF8StringEncoding))

```

### NSURLConnection

上面的两种通信方式只适用于快速读取数据，因为它们工作方式是同步的，读取数据时用户界面会处于卡死状态，上面两种方式一般用于读取本地的资源。

#### 同步加载

```swift

		var resp:NSURLResponse?
        var error:NSError?
        
        //同步读取数据
        var data = NSURLConnection.sendSynchronousRequest(NSURLRequest(URL: NSURL(string: "http://www.jikexueyuan.com")!), returningResponse:&resp,error:nil)
        
        
        if let d = data{
            
        //    println(resp)
        
            //转换成字符串数据
            println(NSString(data: d, encoding: NSUTF8StringEncoding))
        }
        
        //错误处理
        if let e = error{
            println(e)
        }

```

#### 异步加载

```swift

//异步加载网络数据
        
        NSURLConnection.sendAsynchronousRequest(NSURLRequest(URL: NSURL(string: "http://jikexueyuan.com")!), queue: NSOperationQueue())
            {
                (resp:NSURLResponse!, data:NSData!, error:NSError!) -> Void in
            
                if let e = error{
                    println("发生了错误")
                }else{
                    println(NSString(data: data, encoding: NSUTF8StringEncoding))
                }
            
        }

```

## 与服务器通信

### GET 方式

```swift

		NSURLConnection.sendAsynchronousRequest(NSURLRequest(URL:NSURL(string: "http://www.jikexueyuan/index.heml?name=example")!), queue: NSOperationQueue(), completionHandler: { (resp:NSURLResponse!, data:NSData!, error:NSError!) -> Void in
            
            
            
            
            if let d = data{
                
                /*
                
                如果 queue: 参数传递的是 NSOperationQueue.mainQueue() 主线程，
                就可以直接使用下面的写法。但是如果任务是耗时的则会造成界面卡顿，不建议使用这种方式。
                
                */
                //self.tvOut.text = NSString(data:d,encoding:NSUTF8StringEncoding)
                
                /*

                如果 queue: 传递的参数是 NSOperationQueue() 操作线程，那么就不能直接修改主线程的资源，需要调用 dispatch_sync 将修改主线程资源的操作发送到主线程中执行。好处是可以避免耗时的操作造成的界面卡顿。
                
                */
                dispatch_sync(dispatch_get_main_queue(), { () -> Void in
                    //self.tvOut.text = NSString(data:d,encoding:NSUTF8StringEncoding)
                })
                
                
            }
            
        }) 

```

### POST 方式

```swift

        //POST 方式传递数据
        
        var req = NSMutableURLRequest(URL: NSURL(string: "http://www.jikexueyuan")!)
        
        req.HTTPMethod = "POST"
        req.HTTPBody=NSString(string: "name=\(0)").dataUsingEncoding(NSUTF8StringEncoding)
        
        NSURLConnection.sendAsynchronousRequest(req, queue: NSOperationQueue()) { (rsp:NSURLResponse!, data:NSData!, error:NSError!) -> Void in
            if let d = data{
                
            }
        }

```