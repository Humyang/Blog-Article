layout: [post]
title: "iOS Swift 基础"
date: 2015-07-08 23:16:11
tags: 
- iOS
categories: 
- iOS 
- 备忘
id: "iOS-Swift-Base"

---

最近看到许多资料都用到 Swift，学习一下 Swift 基础，避免在看视频，博客时卡住。

<!-- more -->

开发环境：Xcode 6.4，知识点主要来源于[极客学院](http://www.jikexueyuan.com/path/ios/)的 iOS 视频教程和 Apple 的 [The Swift Programming Language](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/CollectionTypes.html#//apple_ref/doc/uid/TP40014097-CH8-ID105)。

Swift 的语法变化挺快的，下面如果编译时错了那么可能语法已经更改，建议去 The Swift Programming Language 查看最新语法。还有编译器对代码的格式要求很严格，这也是报错的可能。

#基本语法

## Hello World

main.swift:

```swift

import Foundation

println("Hello, World!")

```

##变量和常量

变量

```swift
var a ＝ 1
a = 10
var b = c
```swift

常量，设定值后不允许再次修改值。

`let c = a + b `

## weak ，unowned 和 strong 

`weak` 和 `unowned` 不会提升 ARC 的 retain count。

带有 weak 的变量可能会变成 nil，所以使用 weak 变量之前有义务使用 optional type 进行检查。

optional：

```swift

func compute(x: Int?) -> String {
  // This function uses optional binding to deconstruct optionals
  if let y = x {
    return "The value is: \(y)"
  } else {
    return "No value"
  }
}

print(compute(42)) // The value is: 42
print(compute(nil)) // No value

```

`unowned` 会假设在它的生命周期期间永远不会变成 nil，它需要在初始化时就设置好它的值。这意味着使用它的变量时不需要进行 optional type 检测。如果某个对象以某种方式将它释放了，那么 unowned reference 再次被使用时会应用程序会崩溃。


> Apple docs:
> Use a weak reference whenever it is valid for that reference to become nil at some point during its lifetime. Conversely, use an unowned reference when you know that the reference will never be nil once it has been set during initialization.

## Swift 数据类型

定义变量

`var str ＝ "Hello "`

定义特定类型

```swift 

var s:String = "World"

var i:Int = 100

var Words:String = "World"

```

> **说明：**一般来说不需要指定类型，Swift 会自动分析类型。

## 字符串连接

 
### 字符串相加

```swift
var str = "Hello "
str = str + "World"

println(str)

```

这种方式不能与其它类型直接连接

### 不同类型连接

```swift

var i = 200
var str = "Hello "
str = "\(str),Other Str,\(100),\(i)"

```

## 数组

不同类型可以放入同一个数组

`var array = ["Hello","World",100,2.3]`

声明空数组

`var empty = []`

只能存放特定类型的数组

`var arrStr =[String]()`

## 字典

类似 C++ 的 Map

创建一个字典

`var dict = ["name":"jikexueyuan" , "age" : "18"]`

动态添加字段

`dict["sex"] = "Female"`

取字段值

`println(dict["name"])`

## 循环语句

### 基本循环

```swift
var arr =[String]()

for index in 0...100{
	arr.append("Item \(index)")
}

println(arr)

for var index = 0; index < 3; ++index {
    println("index is \(index)")
}

```



### for in



```swift

//array 是一个数组

for value in array{
	println(value)
}

```


### while

```swift

var i = 0

//array 是一个数组

while i<arr.count {
	println(arr[i])
	i++
}

```

### 遍历字典

```swift

var dict = ["name" : "Hello","age" : "18"]

for(key,value) in dict{
	println("\(key),\(value)")
}

```

## 流程控制

```swift

for index in 0...100{
	if index%2==0 {
		println(index)
	}
	
}

//定义一个可选变量
var myName:String ?= "jike"

//如果可选变量为空，条件判断不执行。
if let name = myName {
	println("Hello \(name)")
}

```

## 函数

```swift

func sayHello(name:String){
	println("Hello \(name)")
}

sayHello("JiKe");

```

### 指定返回值类型

```swift

func getNums()->Int{
	return 2
}




```

### 返回多个值

```swift

func getNums()->(Int,Int){
	return (2,3)
}

var (a,b) = getNums()

println(a)


```

### 函数当变量使用

```swift

var fun = sayHello

fun("ZhangSan")

```

### 函数闭包

可以在函数内部写函数


## Swift 的面向对象

### 基本代码

```swift

class Hi{
	func sayHi(){
		println("Hello,JiKe")
	}
}

//类继承
class Hello:Hi{
	
	//如果有传入参数则使用传入的参数，没有则使用默认参数
	var _name:String ?= "jike"
	//构造方法	

	init(){
		println("init start")
		self._name = name
	}

	//重写方法
	override func sayHi(){
		
		
		println("Hi again \(self._name)")
	
		//执行父类方法
		
		super.sayHi()
	}
	
	//静态方法，类方法
	class func sayHello(){
		println("Hi Swift")
	}
}

var hi = Hi()
hi.sayHi()


var h = Hello(name:"ZhangsSan")
h.sayHi()

```

#### 静态方法和静态变量

```swift


class Foo {
    var name: String?           // instance property
    class var all: Foo[] = []   // type property NOT YET SUPPORTED
    class var comp: Int {       // computed type property
        return 42
    }

    class func alert() {        // type method
        println("There are \(all.count) foos")
    }
}

```

## 类的动态拓展

```swift

//在不改变类的继承结构下拓展类的功能的一种方式
extension Hi {
    func sayHaHa(){
        println("Hello,sayHaHa")
    }
}

class Hi{
    func sayHi() {
        println("Hello,JiKe")
    }
}

//在不改变类的继承结构下拓展类的功能的一种方式
extension Hi {
    func sayHaHa2(){
        println("Hello,sayHaHa2")
    }
}

var miko:Hi = Hi()

miko.sayHaHa()
miko.sayHi()
miko.sayHaHa2()

```

## 协议

```swift

protpcol People{
	func getName()->String
}

class Man:People{
	func getName() -> String {
	
		return "ZhangSan"
	}
}

var m = Man()
println("Name is \(m.getName())")


```

## 命名空间

Swift 中并没有命名空间，通过类的嵌套可以实现命名空间的概念。

### 直接的写法

```swift

class com{
	class jike{
		class XueYuan{
			func sayHello(){
				println("Hello")
			}
		}
	}
}

```

### 使用拓展添加类到命名空间中

```swift

class com{
	class jike{
	}
}

extension com.jike{
	class Hello{
		func sayHello(){
			println("Hello jike")
		}
	}
}

extension com.jike{
	class World{
		func sayWorld(){
			println("Hello jike")
		}
	}
}


```

## 单例写法

资料来源：[stackoverflow](http://stackoverflow.com/questions/24024549/dispatch-once-singleton-model-in-swift)



### Class constant

```swift

class Singleton  {
   static let sharedInstance = Singleton()
}

```

This approach supports lazy initialization because Swift lazily initializes class constants (and variables), and **is thread safe by the definition of let**.

Class constants were introduced in **Swift 1.2**. If you need to support an earlier version of Swift, use the nested struct approach below or a global constant.

类中有了 `static let sharedInstance = Singleton()` 如果类还有实例变量，那么还需要重载 init 方法了。

### Nested struct

```swift

class Singleton {
    class var sharedInstance: Singleton {
        struct Static {
            static let instance: Singleton = Singleton()
        }
        return Static.instance
    }
}

```

Here we are using the static constant of a nested struct as a class constant. This is a workaround for the lack of static class constants in **Swift 1.1 and earlier**, and still works as a workaround for the lack of static constants and variables in functions.

### dispatch_once

```objc

class Singleton {
    class var sharedInstance: Singleton {
        struct Static {
            static var onceToken: dispatch_once_t = 0
            static var instance: Singleton? = nil
        }
        dispatch_once(&Static.onceToken) {
            Static.instance = Singleton()
        }
        return Static.instance!
    }
}

```

The traditional Objective-C approach ported to Swift. I'm fairly certain there's no advantage over the nested struct approach but I'm putting it here anyway as I find the differences in syntax interesting.