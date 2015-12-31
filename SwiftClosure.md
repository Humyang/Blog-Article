layout: [post]
title: "Swift 的 Closure 和 Function"
date: 2015-09-25 18:41:15
tags: 
- iOS
categories: 
- iOS
- Swift
- 备忘
id: "SwiftClosureFunction"
---

在学 ReactiveCocoa 时发现源代码大量用到 Closure 和 Function，这里记录一些知识点，方便日后查询。

<!-- more -->


---

Closure 类似 Objective-C 的 block ，是一个独立的代码块，可以在代码中传递和使用。它的功能很强大但很陌生，有人对它建立了这样一个域名：[fuckingswiftblocksyntaxhttp.com](http://fuckingswiftblocksyntax.com/)。

# Function 类型

每一个 function 都有指定的 function 类型，由 function 的参数类型和返回值类型组成，例如：

```swift
func addTwoInts(a: Int, b: Int) -> Int {
    return a + b
}
func multiplyTwoInts(a: Int, b: Int) -> Int {
    return a * b
}
```

这两个 function 的类型都是 `(Int, Int) -> Int`，它们表示的这个 function 需要两个 Int 参数和一个 Int 返回值。

这里是另一个例子：

```swift
func printHelloWorld() {
    println("hello, world")
}
```

它的类型是 `() -> ()`,表示 function 不需要参数并且返回 `Void`，没有指定返回值的 function 总会返回 `Void`，相当于 Swift 中一个空的 tuple，用 `()` 表示。

## 使用 Function 类型

可以像 Swift 中其它类型一样使用 Function 类型，例如，可以定义一个 Function 类型的常量或变量并对它分配相应的 Function 变量：

```swift
var mathFunction: (Int, Int) -> Int = addTwoInts
```

这里定义了一个 mathFunction 变量，它的类型是需要两个 Int 参数和返回值是 Int 的 Function，新变量指向称为 addTwoInts 的 function。

接着就可以把 mathFunction 作为 function 调用 ：

```swift
println("Result: \(mathFunction(2, 3))")
// prints "Result: 5"
```

## Function 类型作为参数类型

你可以使用 function 类型例如 `(Int, Int) -> Int` 作为其它 function 的参数类型，使得 function 调用者可以在调用 function 时提供某些方面的功能实现。

这里是一个打印数学函数结果的例子：

```swift
func printMathResult(mathFunction: (Int, Int) -> Int, a: Int, b: Int) {
    println("Result: \(mathFunction(a, b))")
}
printMathResult(addTwoInts, 3, 5)
// prints "Result: 8"
```

这个例子定义了称为 printMathResult 的 function，它有三个参数，第一个参数是 mathFunction，你可以传递该类型的任意 function 作为第一个参数，第二和第三个参数是 a 和 b，都是 Int 类型，用作为 mathFunction 提供输入值。

当 `printMathResult` 被调用时，它被传递了 `addTwoInts` ，和分别是 `3` 和 `5` 的 Int 类型，打印的结果是 `8`.

printMathResult 的作用是调用相应类型的数学 function 并打印结果。它不关心数学 function 的实际如何实现，它只关心数学 function 的类型是否正确。这使得 printMathResult 可以把一部分实现以安全类型的方式交给 function 调用者。

## Function 类型作为返回类型

Function 类型也可以作为其它 Function 的返回类型，可以通过在 Function 的返回箭头 (->) 后面输入一个完整的 function 类型作为该 function 的返回类型。

下面的例子定义了两个简单的 function 称为 stepForward 和 stepBackward。stepForward function 返回比输入值多 1 的值，stepBackward function 返回比输入值少 1 的值。它们的类型都是 `(Int) -> Int`: 

```swift
func stepForward(input: Int) -> Int {
    return input + 1
}
func stepBackward(input: Int) -> Int {
    return input - 1
}
```

这里有一个 function 称为 chooseStepFunction，它返回的类型是 "function 类型 `(Int) -> Int`"。

`chooseStepFunction` 基于 Bool 类型参数 `backwards` 决定返回值是 `stepForward` 或 `stepBackward`：

```swift
func chooseStepFunction(backwards: Bool) -> (Int) -> Int {
    return backwards ? stepBackward : stepForward
}
```

现在就可以使用 chooseStepFunction 获取前进方向或其它方向的 Function了：

```swift
var currentValue = 3
let moveNearerToZero = chooseStepFunction(currentValue > 0)
// moveNearerToZero now refers to the stepBackward() function
```

上面的例子使用变量 `currentValue` 决定返回的 Function 是执行值增长还是递减，`currentValue` 的初始值是 3，因为 `currentValue > 0` 返回 `true`，所以 `chooseStepFunction` 返回 `stepBackward` Function。返回 Function 的引用保存在常量 `moveNearerToZero` 中。

现在可以使用 `moveNearerToZero` 使 `currentValue` 递减成 0:

```swift
println("Counting to zero:")
// Counting to zero:
while currentValue != 0 {
    println("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
println("zero!")
```

##嵌套 Function 

大部分 Function 都是定义在全局空间的的全局 Function，你也可以把 Function 定义在其它 Function 的内部，它们称为 嵌套 Function。

嵌套 Function 默认在外部是隐藏的，但可以在它的闭合空间 ( `{}` 内)被调用和使用。enclosing function 也可以返回一个嵌套 function 使得嵌套 function 可以在其它空间使用。

上面的例子可以写成嵌套 function 的形式：

```swift
unc chooseStepFunction(backwards: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    return backwards ? stepBackward : stepForward
}
var currentValue = -4
let moveNearerToZero = chooseStepFunction(currentValue > 0)
// moveNearerToZero now refers to the nested stepForward() function
while currentValue != 0 {
    println("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
println("zero!")
// -4...
// -3...
// -2...
// -1...
// zero!
```

# Closure

在 Function 章节中介绍的全局和嵌套 Function，实际上是特殊的 Closure，Closure 有三种形式：

* 全局 Function 是有名称但不捕捉任何值的 Closure。
* 嵌套 Function 是有名称且可以从它的封闭空间捕捉值的 Closure。
* Closure 表达式是无名称的 Closure，使用了轻量级的语法表达，并且可以从围绕它的上下文中捕捉值。

Swift 的 Closure 表达式的风格清晰和简洁，它鼓励在常见的使用场景优化使用简短，整洁的语法，优化方式包括：

* 从上下文推测参数和返回值类型
* 从 Closure 用单行表达式隐式返回值
* 缩短参数名称
* 尾式 Closure 写法。

下面会介绍具体的实现方式。


## Closure 表达式

在 Function 中介绍的嵌套 Function，是一种命名和定义自包含的代码块作为一个较大的 Function 的一部分的便利方式。在写类似 Function 构造的简短版本时不需要完整的定义和命名。尤其是当这个 function 是作为其它一个或多个 function 的参数时。

Closure 表达式是一种简短集中的内嵌 Closure 写法。Closure 表达式提供了几个语法优化 closure 的写法缩短它的代码并且不会使它所表达的意思变的模糊。下面的用例子说明 closure 表达式如何优化 `sorted` function 的写法，通过多次迭代，得出最简洁的写法，每次都会用更简洁的方式表达 `sored` function。

## Sored Function

Swift 的标准库提供了一个称为 sorted 的 function，它可以排序已知类型的数组的值，基于由你提供的排序 closure。一旦完成排序处理，sorted 返回与旧数组同样类型和尺寸的新数组，里面的元素已经按照命令正确排序。sorted 不会修改原始数组。

sorted 会根据拼音对下面的 String 类型数组进行排序：

```swift
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
```

sorted function 有两个参数：

* 已知值的类型的数组
* 与数组内容相同类型的两个参数并返回 Bool 类型的 closure。返回值是根据 “排序时第一个参数的值应该放在第二参数的值前面还是后面” 判断。如果第一个值应该出现在第二个值前面，closure 返回 true，否则返回 false。

例子是排序 String 值的数组，因此排序 closure 需要的 Function 类型是 `(String, String) -> Bool`。

一种提供排序 closure 的方式是写一个对应类型的常规 Function，把它作为 sorted function 的第二个参数：


```swift
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

func backwards(s1: String, s2: String) -> Bool {
    return s1 > s2
}
var reversed = sorted(names, backwards)
```
如果 s1 大于 s2，那么会返回 true，排序时 s1 会出现在 s2 之前。大于的意思是位于字母表的顺序后面，例如 B 比 A 大。

这个例子中的写法太长，本质上就是为了传达 a > b 的意思。在下面的例子中，将会使用 closure 表达式以内嵌的方式传递 closure。

## Closure 表达式语法

Closure 表达式的语法一般如下：

```swift
{ (parameters) -> return type in
    statements
}


```

Closure 表达式的语法可以使用常量参数，变量参数，和 `inout` 参数。不能提供默认值。可以使用可变参数，如果你命名了可变参数并把它放置在参数列表末尾。元组也可以被用作参数类型和返回类型。

这个例子演示之前的 `backwards` Function 的 closure 表达式版本：

```swift
reversed = sorted(names, { (s1: String, s2: String) -> Bool in
    return s1 > s2
})
```
这个内嵌 closure 的参数声明和返回类型等同 backwards function 的声明。这两种情况中，它们都被写为 `(s1: String, s2: String) -> Bool`。但是，在内嵌 closure 表达式中，参数和返回类型都是写在大括号内，不是写在外面。

closure 的主体是通过关键字 `in` 开始。这个关键字说明 closure 的参数和返回类型的定义已经完成，接下来开始 closure 的主体实现。

因为这个 closure 的实现很短，所以它可以写为一行：

```swift
reversed = sorted(names, { (s1: String, s2: String) -> Bool in return s1 > s2 } )
```

调用 sorted 的方式整体没有改变，Function 参数传递了由一对括号包围着参数和返回值的 function，这就是一个内嵌 closure。

## 从上下文推断类型

因为排序 closure 是作为参数传递到 function 中，Swift 可以从 `sorted` 第二个参数类型推测内嵌 closure 的参数类型和它返回值的类型。这个参数期待的类型是 `(String, String) -> Bool`，这意味着 (String,String) 和 Bool 类型不需要写为 closure 表达式定义的一部分。因为所有类型都可以被推断，所以表示返回类型的箭头 (->) 和围绕参数的括号也可以被忽略：


```swift
reversed = sorted(names, { s1, s2 in return s1 > s2 } )
```

当传递 closure 到 function 中作为内嵌 closure 表达式时，Swift 总是能够推断参数和返回值类型。因此，当 closure 作为 function 的参数时你永远不需要写完整的内嵌 closure。

## 单行表达式 closure 实现隐式返回

单行表达式 Closure 可以在它的实现中通过忽略 `return` 关键字实现隐式返回单行表达式的结果，例如上面的例子：

```swift
reversed = sorted(names, { s1, s2 in s1 > s2 } )
```

在这里，sorted function 的第二个参数的 function 类型明确要求必须通过 closure 返回 Bool 类型值。因为 closure 的主体包含了单行表达式 (`s1 > s2`) 它是返回 Bool 值的，没有歧义，所以 `return` 关键字可以被忽略。 

## Shorthand Argument Names

Swift 对内嵌 Closure 自动提供了参数名的缩写，它可以通过 `$0, $1, $2` 等等指向 closure 的参数值。

如果你在 closure 表达式使用参数名缩写，你可以忽略 closure 的参数列表的定义，缩写参数名的类型和数字将会根据期望的 Function 类型推断。in 关键字也可以被忽略，因为单行 closure 表达式组成了它的主体：

```swift
reversed = sorted(names, { $0 > $1 } )
```

在这里，$0 和 $1 指向 closure 的第一个和第二个 String 参数。

## 运算符 Functions

上面的 closure 表达式的写法还能更短，Swift 的 String 类型为有两个参数类型为 String 的 Function 中的大于运算符 (>) 定义了 sting 特有的实现过程，它会返回一个 Bool 类型的值。它匹配的 function 类型与 sorted function 需要的第二个参数的类型吻合，因此，你可以简单的传入一个大于运算符，Swift 将会推出你想要使用的 string 特有的实现过程：

```swift
reversed = sorted(names, >)
```

更多关于运算符 Function 的资料，见 [Operator Functions](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AdvancedOperators.html#//apple_ref/doc/uid/TP40014097-CH27-ID42)。

# 尾式 Closures

如果你需要传递 closure 表达式到 function 中作为 function 的最后一个参数并且是很长的 closure expression，那么可以使用尾式 closure (trailing closure) 代替。 尾式 closure 是写在 function 括号外部 (和后面) 的 closure 表达式：

```swift
func someFunctionThatTakesAClosure(closure: () -> ()) {
    // function body goes here
}
 
// here's how you call this function without using a trailing closure:
 
someFunctionThatTakesAClosure({
    // closure's body goes here
})
 
// here's how you call this function with a trailing closure instead:
 
someFunctionThatTakesAClosure() {
    // trailing closure's body goes here
}
```

> 注意：如果 closure 表达式是 function 需要的唯一参数并且你将表达式作为尾式 closure 传递，那么当你调用函数时不需要在函数名后面写括号对 `()`

在 Closure 表达式语法演示的字符串排序 closure 使用尾式 closure：

```swift
reversed = sorted(names) { $0 > $1 }
```

# Capturing Values

closure 可以在定义它的环绕上下文中捕捉常量和变量。然后 closure 可以在它的主体内引用和修改这些常量和变量的值，即使原始空间定义的常量和变量可能不是长时间存在的。

在 Swift 中，内嵌 function 是最简单形式的可以捕捉值的 closure，它是写在其它 function 主体内的 function。内嵌 function 可以捕捉任何外部 function 的 参数也可以捕捉任何定义在外部 function 的常量和变量。

这里是一个 function 的例子 `makeIncrementer`，它包含一个 `incrementer` 内嵌 function。内嵌 function 从环绕上下文中捕获两个值，`runningTotal` 和 `amount`。捕获这些值之后，`incrementer` 通过 `makeIncrementer` 返回作为每次 function 被调用时使用 `amount` 提升 `runningTotal` 的值的 closure：

```swift
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementer() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}
```

`makeIncrementer` 的返回类型是 `() -> Int`，意味着它是返回一个 function，而不是简单的值，返回的 function 没有参数，并且每次调用都会返回这个 Int 值。学习 function 如何返回其它 function，见 Function [Types as Return Types](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Functions.html#//apple_ref/doc/uid/TP40014097-CH10-ID177)。

在 `makeIncrementer` 中定义了称为 `runningTotal` 的 Int 变量，而将要返回的 incrementer 保存了当前运行时的 总计。这个变量初始值为 0。 

makeIncrementer 有一个单独的 Int 参数拓展名称为 forIncrement，本地名称为 amount。这个参数用来指定 runningTotal 值在返回的 incrementer function 每次调用时应该增加多少。

makeIncrementer 定义的内嵌 function 称为 incrementer，它执行实际的增加操作。这个 function 只是简单的把 amount 和 runningTotal 相加，并返回它们的值。

如果只看内嵌 function，那么它是这样的：

```swift
func incrementer() -> Int {
    runningTotal += amount
    return runningTotal
}
```

这个 incrementer function 没有任何参数，但是它的 functoin 主体引用了 runningTotal 和 amount。它是从环绕它的 Function 中捕捉 runningTotal 和 amount 的现有值并在它自己的 function主体中使用它们。

因为它每次被调用都会修改 runningTotal 变量，incrementer 捕获了当前 runningTotal 变量的引用，不只是复制它的初始值，捕捉引用确保当 makeIncrementer 的调用结束后 runningTotal 不会消失，并确保 runningTotal 在下次 incrementer function 被调用时可用。

因为它没有修改 amount，amount 也没有在外部改变，incrementer 实际上将保存在 amount 的值的 copy 捕获和保存。这个值随着新的 incrementer function 保存。

> Swift 会判断应该捕获引用还是应该对值进行 copy，你不需要注明 amount 或 runningTotal 它们也能在 incrementer function 中使用。Swift 也会处理所有 runningTotal 的 disposing 涉及的内存管理，当它长时间不被 incrementer function 需要时。

这里是 makeIncrementer 使用的例子：

```swift
let incrementByTen = makeIncrementer(forIncrement: 10)
```

这个例子设置称为 `incrementByTen` 的常量指向一个每次调用对 runningTotal 增加 10 的增量 function。多次调用这个 function 会有下面的效果：

```swift
incrementByTen()
// returns a value of 10
incrementByTen()
// returns a value of 20
incrementByTen()
// returns a value of 30
```

如果你创建第二个增量 function，它将有新的属于它的存储引用，分隔 runningTotal 变量：

```swift
let incrementBySeven = makeIncrementer(forIncrement: 7)
incrementBySeven()
// returns a value of 7
```

再次调用原来的增量 function (`incrementByTen`) 增加它的 `runningTotal` 变量，并不会被 `incrementBySeven` 所影响：

```swift
incrementByTen()
// returns a value of 40
```

说明：如果你分配 closure 到类实例的 property，那么 closure 捕捉实例是通过指向实例或成员，你将会在 closure 和 instance 之间创建 strong 引用周期。Swift 使用捕捉列表打破这些 strong 引用周期，更多信息，见 [Strong Reference Cycles for Closures](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AutomaticReferenceCounting.html#//apple_ref/doc/uid/TP40014097-CH20-ID56)。

# Example

## Functoin 作为参数和 Function 返回值有两个 -> 的例子

像这样的 Function 结构，在 ReactiveCocoa 中大量用到。

```swift
func MainFunc(value: Int,hello:Int, paramerFunc: (Int,Int) -> Int) -> Int -> Int {
    return {
        a in
        
        var s =  paramerFunc(a,a)
        return s  + 4000
    }
}

var NewFunc = MainFunc(2,3, {value2,h2 in
    return value2 * 3*h2
})
var j = NewFunc(20)
println(j)

MainFunc(2,3, {value2,h2 in
    return value2 * 3*h2
})(30)
```

1.

方法 MainFunc 的类型是：

`(Int,Int,(Int,Int)->Int)->Int->Int`

参数与返回类型由 `->` 分隔。
需要的参数是：`(Int,Int,(Int,Int)->Int)`,由两个 Int 和一个 Function 类型组成。
返回的类型是： `Int->Int`，也是一个方法类型，加上个括号结构那么类型就很清晰了：

`(Int,Int,(Int,Int)->Int)->((Int)->Int)`

2.

MainFunc 中将 Function 作为参数，该参数需要的类型是 `(Int,Int) -> Int`，在调用 MainFunc 方法时直接使用 Closure 作为值传递到这个参数中：

```swift
var NewFunc = MainFunc(2,3, {value1,value2 in
    return value1 * 3*value2
})
```
Closure 中 value1,value2 是 MainFunc 方法的参数 paramerFunc 的类型 `(Int,Int) -> Int` 关联的两个传入值，返回值也是与 paramerFunc 的类型对应， in 则是用来分隔参数和方法定义。

这个 Closure 的写法省略了参数类型和返回值，因为可以由 Swift 编译器自动判断，Closure 完整的写法可以看上面的章节。

当 MainFunc 返回值给 NewFunc 后，NewFunc 类型是 `Int->Int`，Function 的内容就是 MainFunc 所返回的一个 Closure。

```swift
	{
        a in
        var s =  paramerFunc(a,a)
        return s  + 4000
    }
```

3.

调用 NewFunc，返回最终的结果：

```swift
var j = NewFunc(20)
println(j)
```

这种调用方式也能得出相同效果：

```swift
var b = MainFunc(2,3, {value2,h2 in
    return value2 * 3*h2
})(20)
```

## Function 返回值有更多个 -> 的例子

上面的例子返回值有两个 `->`，代表返回 `Int -> Int` 的 Function 类型，那么返回值有更多个 `->` 呢？ 

下面是一个用到泛型的例子，返回值有三个 -> :

```swift
func MoreReturn<T,U,E,X,Y,Z>(value: T,hello:U,EEs:E,ZZs:Z,YYs:Y, multFunction: (T,U) -> X) -> E -> Z -> Y {
    return { //#1
        a in
        return { //#2
            c in
            var d = multFunction(a as! T ,c as! U)
            return d as! Y //#3
        }
    }
}
```

MoreReturn 的 Function 类型是：`(T,U,E,Z,Y,(T,U) -> X) -> E -> Z -> Y`,在 Xcode 中可以看到 MoreReturn 的类型是  `E -> Z -> Y`，跟该类型对应的 Closure 是：

```swift
	{	a in
        return {
            c in
            var d = multFunction(a as! T ,c as! U)
            return d as! Y
        }
    }
```
这个 Closure 有一个参数，和一个 Function 返回值，那么 MoreReturn 的类型加上括号就是：`(E ->(Z -> Y))`,本来以为是 `((E) ->((Z) -> Y)))`，结果编译不通过。

如果想多个参数，可以这样  `((E,Z) ->(Z -> Y))`,对应的 Closure 也需要更改：

```swift
	{a,q in
        return {
            c in
            var d = multFunction(a as! T ,c as! U)
            return d as! Y
        }
    }
```

下面来使用这个复杂的 function：

```swift
//获取 #1 return 的内容
var NewFunc1 = Fanxing(20, 20,20,20,20,{ (Va, Vb) -> Int in
    return Va * Vb
    }
)
//获取 #2 return 的内容
var NewFunc2: (Int -> Int) = NewFunc1(20,20)
//获取 #3 return 的内容
NewFunc2(21)

//跟上面效果相同
NewFunc1(20,20)(20)
```


下面再来一个四个 -> 的 Function，帮助理解它们是如何嵌套的：

```swift
func Fanxing<T,U,E,X,Y,Z>(value: T,hello:U,EEs:E,ZZs:Z,YYs:Y, multFunction: T -> X) -> Z -> Z -> Y -> Z -> Y {
    return {
        a in
        return {
            c in
            return {
                v in
                return {
                    e in
                    return e as! Y
                }
            }
        }
    }
}

var NewFunc1 = Fanxing(20, 20,20,20,20,{ Va -> Int in
    return Va
    }
)
```

在 Xcode 看到 NewFunc1 的返回类型：`Int -> Int -> Int -> Int -> Int`。

那么 Fanxing 的返回类型加上括号后是：`(T,U,E,Z,Y,T->X)->(Z -> (Z -> (Y -> (Z -> Y))))`，比原来的写法 `(T,U,E,Z,Y,T->X)->Z->Z->Y->Z->Y` 清晰很多，而且也能一下就看出来返回值嵌套的规律。弄清楚它的规律之后，再翻回前面的内容就发现没什么难点了。