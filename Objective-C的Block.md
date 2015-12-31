layout: [post]
title: "Objective-C 的 Block"
date: 2015-08-30 12:08:18
tags: 
- iOS
categories: 
- iOS
- Objective-C
- 备忘
id: "Objective-C-Block"
---


官网的 block 翻译和一些 block 使用过程的记录

<!-- more -->


---


[资料来源](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/Blocks/Articles/bxGettingStarted.html#//apple_ref/doc/uid/TP40007502-CH7-SW1)

# 介绍

Block 对象是 C 语言级别的语法和 runtime 功能。它类似标准 C 函数，但额外在可执行代码中可以包含绑定到自动化 (栈) 或手动管理 (堆) 的内存的变量。block 因此能保持状态 (数据) 的集合使得它在执行之后仍然能影响它的行为。

你可以使用 block 组成可以传递到 API 的函数表达式，可选的存储，被多线程使用。block 最适合作为回调方法使用因为 block 能让代码在回调完成后执行和保持执行过程中需要的数据。

Block 在 GCC 和 Clang 可用预装在 OS X v10.6 Xcode 开发者工具中，你可以在 OS X v10.6 和 iOS 4.0 之后使用 block。Block runtime 是开源的你可以在 [LLVM's compiler-rt subproject repository](http://llvm.org/svn/llvm-project/compiler-rt/trunk/) 中找到。block 也已经以 [N1370: Apple’s Extensions to C](http://www.open-std.org/jtc1/sc22/wg14/www/docs/n1370.pdf) 提交到 C 标准工作组。因为 Objective-C 和 C++ 都是由 C 驱动，block 设计为可以与这三种语言工作 (以及 Objective-C++)。它的语法体现了这个目标。

你应该阅读这个文档学习什么是 block 对象和如何从 C，C++,Objective-C 使用它们。


# Block 快速使用

## 定义和使用 Block

你可以使用 `^` 定义一个 block 变量和表明 block 代码段的开始。block 自身的主体由 `{}` 包围在内,下面是例子 (与 C 语言一样，以 `;` 表明 blcok 结束。) ：

```objc

int multiplier = 7;
int (^myBlock)(int) = ^(int num) {
    return num * multiplier;
};

```

这张图片解释了上面的语法：

![](./blocks.jpg)

注意可以在定义 block 的同一个空间内通过变量使用 block。

如果你把 block 定义为变量，那么你可以像使用函数一样使用它们：

```objc
int multiplier = 7;
int (^myBlock)(int) = ^(int num) {
    return num * multiplier;
};
 
printf("%d", myBlock(3));
// prints "21"

```


## 直接使用 Block

许多情况下，你都无需定义 blcok 变量，你可以根据需要使用简写的 block 语法作为实参传递。下面例子用到了 `qsort_b` 函数，qsort_b 类似标准函数 `qsort_r`，但最后实参需要传递 block。

```objc
char *myCharacters[3] = { "TomJohn", "George", "Charles Condomine" };
 
qsort_b(myCharacters, 3, sizeof(char *), ^(const void *l, const void *r) {
    char *left = *(char **)l;
    char *right = *(char **)r;
    return strncmp(left, right, 1);
});
 
// myCharacters is now { "Charles Condomine", "George", "TomJohn" }

```

## Block 与 Cocoa

Cocoa 框架有几个方法采取了 block 作为实参，通长用来执行对集合对象的运算，或者用作运算完成后的回调处理。下面的例子展示如何把 block 传递到 NSArray 的 `sortedArrayUsingComparator:` 方法。这个方法需要一个单独的参数 － block。为了直观展示，这个例子的 block 定义为 NSComparator 本地变量。

```objc
NSArray *stringsArray = @[ @"string 1",
                           @"String 21",
                           @"string 12",
                           @"String 11",
                           @"String 02" ];
 
static NSStringCompareOptions comparisonOptions = NSCaseInsensitiveSearch | NSNumericSearch |
        NSWidthInsensitiveSearch | NSForcedOrderingSearch;
NSLocale *currentLocale = [NSLocale currentLocale];
 
NSComparator finderSortBlock = ^(id string1, id string2) {
 
    NSRange string1Range = NSMakeRange(0, [string1 length]);
    return [string1 compare:string2 options:comparisonOptions range:string1Range locale:currentLocale];
};
 
NSArray *finderSortArray = [stringsArray sortedArrayUsingComparator:finderSortBlock];
NSLog(@"finderSortArray: %@", finderSortArray);
 
/*
Output:
finderSortArray: (
    "string 1",
    "String 02",
    "String 11",
    "string 12",
    "String 21"
)
*/

```

## __block 变量

block 的一个强大功能是它们可以在同一个词法域中修改变量。你可以使用 `__block` 存储类型修饰符使变量可以在 block 内修改，在上面的 Block 与 Cocoa 的例子中，你可以使用 block 变量统计多少个字符串在比较时相等，如下面例子所示。为了直观，这个例子的 block 直接作为参数传递并使用了 `currentLocale` 在 block 内部作为只读变量。

```objc
NSArray *stringsArray = @[ @"string 1",
                          @"String 21", // <-
                          @"string 12",
                          @"String 11",
                          @"Strîng 21", // <-
                          @"Striñg 21", // <-
                          @"String 02" ];
 
NSLocale *currentLocale = [NSLocale currentLocale];
__block NSUInteger orderedSameCount = 0;
 
NSArray *diacriticInsensitiveSortArray = [stringsArray sortedArrayUsingComparator:^(id string1, id string2) {
 
    NSRange string1Range = NSMakeRange(0, [string1 length]);
    NSComparisonResult comparisonResult = [string1 compare:string2 options:NSDiacriticInsensitiveSearch range:string1Range locale:currentLocale];
 
    if (comparisonResult == NSOrderedSame) {
        orderedSameCount++;
    }
    return comparisonResult;
}];
 
NSLog(@"diacriticInsensitiveSortArray: %@", diacriticInsensitiveSortArray);
NSLog(@"orderedSameCount: %d", orderedSameCount);
 
/*
Output:
 
diacriticInsensitiveSortArray: (
    "String 02",
    "string 1",
    "String 11",
    "string 12",
    "String 21",
    "Str\U00eeng 21",
    "Stri\U00f1g 21"
)
orderedSameCount: 2
*/
```

这里的详细细节在 [block and Variables]() 讨论。

# Block 中的概念

Block 对象提供创建 C，C 驱动的语言例如 Objective-C,C++ 的特殊函数主体的方式。在其它语言和环境，block 对象也被称作 “closure”。我在通常这里把它称为 “block”，除非有标准 C 在 block 的代码中混用。

## Block 的功能

block 是一个匿名内嵌代码集合：

* 有类似函数的参数类型列表
* 有自动推断或声明的返回类型
* 可以从它定义的词法域内捕捉状态
* 可以把词法域内的状态选择性修改
* 在词法域内共享的 block 可以共享修改
* 可以持续共享和修改定义在词法域 (栈框架) 内的状态，即使词法域 (栈框架) 已经销毁

你可以复制 block 甚至传递到其它线程延迟执行 (或者从拥有它的线程到 runloop 中)。编译器和 runtime 会将 block 所有引用的变量在所有的 block 副本保留。尽管 block 可以在纯 C 和 C++ 可用，但 block 总是一个 Objective-C 对象。

## 用途

block 代表典型的小巧，独立的代码块。例如，在封装可以同时执行的工作单元，或遍历集合中的项，或者当其它运算完成时的回调方法特别有用。

block 对传统的回调方法特别有用有两个主要原因：

1. 它们可以让你写在方法实现的上下文执行之后调用的代码。
 	因此 block 通常作为框架方法的参数。
2. 它们可以访问本地变量。<br /> 相对于将包含所有需要的上下文信息封装为数据结构作为参数传递给 block 所需要做的操作，你可以更简单的直接访问本地变量。

# 声明和创建 Block

## 声明 block 引用

Block 变量会保持对 block 的引用。定义它们使用的语法类似定义指向函数的指针，除了使用 `^` 替代 `*`。block 类型与 C 的类型系统可以相互操作，下面都是有效的 block 变量声明：

```objc
void (^blockReturningVoidWithVoidArgument)(void);
int (^blockReturningIntWithIntAndCharArguments)(int, char);
void (^arrayOfTenBlocksReturningVoidWithIntArgument[10])(int);
```

block 也支持可变参数 (`...`)。没有参数的 block 必须在参数列表指定 void。

Block 被设计为完全类型安全通过给予编译器完整的元数据集合验证 block 的使用是否有效，传递到 block 的参数，和返回值的分配。你可以投递 block 引用到任何类型的指针，反之亦然。但是你不能通过指针运算符 (`*`) 反向获取 block 引用，因为 block 的尺寸无法在编译时计算。

你也可以为 block 创建类型－通常这被认为是最佳方式，当你在多个地方都要用到这个 block 时：

```objc
typedef float (^MyBlockType)(float, float);
 
MyBlockType myFirstBlock = // ... ;
MyBlockType mySecondBlock = // ... ;

```

## 创建 Block

你可以使用 `^` 运算符表明 block 词法表达式的开始，它后面随着包含参数列表的 `()`。block 的主体包含在 `{}` 内，下面的例子定义了一个简单的 block 并将它分配给前面声明的变量 (`oneFrom`)－这里的 block 以 C 声明的符号 `;` 结束：

```objc
float (^oneFrom)(float);
 
oneFrom = ^(float aFloat) {
    float result = aFloat - 1.0;
    return result;
};
```

如果你没有明确定义 block 表达式的返回值，那么它会根据 block 的内容自动推断。如果返回类型是根据推断所得并且参数列表指定为 `void`，那么你可以省略 (`void`) 参数列表。但声明了多个返回值时，则必须明确对应 (如果有必要可以使用 casting)。

## 全局 Block

在文件级别，你可以使用 block 作为全局词法：

```objc
#import <stdio.h>
 
int GlobalInt = 0;
int (^getGlobalInt)(void) = ^{ return GlobalInt; };
```

# Block 和变量

这章描述 block 和变量之间的交互，包含了内存管理。

## 变量的类型

在 block 对象的代码主体内部，变量能以五种方式处理。

你可以引用三个标准的变量类型，就像函数一样：

* 全局变量，包含静态本地变量。
* 全局函数 (不是技术上可变的）
* 本地变量和从封闭空间提供的参数

Block 也支持两种其它类型的变量：

1. 在函数级别是 `__block` 变量。这些变量在 block 内 (和闭合空间) 是易变的并且如果任何引用它的 block 被复制到堆中，这个变量都会保留。
2. `const` 导入。

最后，方法实现过程的内部，block 可以引用 Objective-C 实例变量－见 [Object and Block Variables]()。

下面的规则对在 block 内使用的变量生效：

1. 可以访问全局变量，包含位于闭合空间内的静态变量。
2. 可以访问传递到 block 的参数 (就像函数访问它的参数)。
3. 栈 (非静态) 变量通位于闭合句法空间内时会被捕捉为 `const` 变量。在程序内它们的值通过 block 表达式的指针获取。在内嵌 block 中，值会被最接近的闭合空间捕获。
4. 定义了 `__block` 修饰符的变量位于 block 的闭合空间内时会提供引用并它因此变得多变。<br /> 在闭合句法空间任何的更改都会映射，包含任意定义在同一个闭合句法空间内的其它 block。这在 [The __block Storage Type]() 中讨论。
5. 声明在 block 闭合句法空间内的本地变量，它的行为与函数中的本地变量非常相似。<br /> 每个 block 的调用都会提供一个新的变量副本。这些变量可以当作 `const` 使用或者接着被 block 闭合空间内的 block 引用。 

下面的例子说明本地非静态变量的使用：

```objc
int x = 123;
 
void (^printXAndY)(int) = ^(int y) {
 
    printf("%d %d\n", x, y);
};
 
printXAndY(456); // prints: 123 456
```

如下面所示，尝试分配新值到 block 中的 x 变量，将会导致错误：

```objc
int x = 123;
 
void (^printXAndY)(int) = ^(int y) {
 
    x = x + y; // error
    printf("%d %d\n", x, y);
};
```

要允许在 block 内部更改变量值，你可以使用 `__block` 存储类型修饰符－见 [__block存储类型]()。

## __block 存储类型

你可以指定一个外部变量为可变的，即可读和写，通过使用 `__block` 存储类型修饰符。`__block` 存储与变量的 `register`，`auto`，和 `static` 等存储类型修饰符类似，但是互斥的。

`__block` 变量存活在共享的变量的词法闭合空间之间的存储和所有 block 和 block 副本的定义或在变量的词法空间内创建的 block，因此，如果任意定义在框架内的 block 的副本会比框架销毁后依旧存活 (例如，封装后延迟执行的 block)。在给定的词法域中多个 block 可以同时使用共享的变量。

作为优化，block 存储从栈开始－就像由 block 它们自己操作。如果 block 是使用 `Block_copy` 生成的 (或者在 Objective-C 中通过发送 `copy` 消息创建的 block)，变量会被复制到堆中。因此，`__block` 变量的地址可以在任何时候改变。

这里对 `__block` 变量的两个进一步限制:它们不能改变数组的长度，并且不能构造包含 C99 变量长度的数组。

下面是 `__block` 变量的例子：

```objc
__block int x = 123; //  x lives in block storage
 
void (^printXAndY)(int) = ^(int y) {
 
    x = x + y;
    printf("%d %d\n", x, y);
};
printXAndY(456); // prints: 579 456
// x is now 579
```

下面的是 block 与几种类型的变量交互：

```objc
extern NSInteger CounterGlobal;
static NSInteger CounterStatic;
 
{
    NSInteger localCounter = 42;
    __block char localCharacter;
 
    void (^aBlock)(void) = ^(void) {
        ++CounterGlobal;
        ++CounterStatic;
        CounterGlobal = localCounter; // localCounter fixed at block creation
        localCharacter = 'a'; // sets localCharacter in enclosing scope
    };
 
    ++localCounter; // unseen by the block
    localCharacter = 'b';
 
    aBlock(); // execute the block
    // localCharacter now 'a'
}
```

## 对象和 Block 变量

block 作为变量为 Objective-C 对象，C＋＋对象，和其它 block 提供支持。

### Objective-C 对象

当 block 是副本时，它会对 block 内使用的对象变量创建强引用。如果你在方法的实现过程中使用了 block：

* 如果你通过引用访问实例变量，强引用指向 `self` 。
* 如果你通过值访问实例变量，强引用指向变量。

下面的例子说明两种情况的区别：

```objc
dispatch_async(queue, ^{
    // instanceVariable is used by reference, a strong reference is made to self
    //instanceVariable 是类的实例变量。
    doSomethingWithObject(instanceVariable);
});
 
 
id localVariable = instanceVariable;
dispatch_async(queue, ^{
    /*
      localVariable is used by value, a strong reference is made to localVariable
      (and not to self).
      
      //localVariable 通过类的实力变量赋值，内存地址已经发生改变。
    */
    doSomethingWithObject(localVariable);
});
```

若要重写特定对象变量的这个行为，你可以为它添加 `__block` 存储类型修饰符。

### C++ 对象

通常你可以在 block 内使用 C++ 对象。在成员函数内，对成员变量和函数的引用是通过隐式的 `this` 指针并且因此变得可变。这里是两个如果 block 是副本时的约定：

* 如果你有一个将要用于基于栈的 C++ 对象的 `__block` 存储类，那么通常会用到 `copy` 构造函数。
* 如果在 block 内使用任意其它基于栈的 C++ 对象，它必须有 `const copy` 构造函数。然后 C++ 对象会使用该构造函数复制。

### Block

当你复制 block 时，在 block 内部的任意对其它 block 的引用都会根据需要复制－可能会复制完整的树 (从顶部开始)。如果你拥有一个 block 变量并且在内部引用了另一个 block，那么 block 将会被复制。

# 使用 Block

## 调用 Block

如果你声明了 block 作为变量，你可以把它作为函数使用，下面两个例子说明：

```objc
int (^oneFrom)(int) = ^(int anInt) {
    return anInt - 1;
};
 
printf("1 from 10 is %d", oneFrom(10));
// Prints "1 from 10 is 9"
 
float (^distanceTraveled)(float, float, float) =
                         ^(float startingSpeed, float acceleration, float time) {
 
    float distance = (startingSpeed * time) + (0.5 * acceleration * time * time);
    return distance;
};
 
float howFar = distanceTraveled(0.0, 9.8, 1.0);
// howFar = 4.9
```

但通常是将 block 作为参数传递到函数或方法中，在这种情况下，会使用 "內联" 的方式创建 block。


## 使用 Block 作为函数的参数


你可以把 blcok 作为参数传递到函数中，就像你传递的其它参数一样。在大部分情况下你都不需要声明 block，只需在参数的位置使用內联方式传递。下面的例子使用了 `qsort_b` 函数，`qsort_b` 与标准函数 `qsort_r` 类似，但最后的参数使用了 block。

```objc
char *myCharacters[3] = { "TomJohn", "George", "Charles Condomine" };
 
qsort_b(myCharacters, 3, sizeof(char *), ^(const void *l, const void *r) {
    char *left = *(char **)l;
    char *right = *(char **)r;
    return strncmp(left, right, 1);
});
// Block implementation ends at "}"
 
// myCharacters is now { "Charles Condomine", "George", "TomJohn" }
```

注意 block 包含在了函数的参数列表内。

接下来的例子展示如何使用 block 与 `dispatch_apply` 函数，`dispatch_apply` 是这样定义的：

```objc
void dispatch_apply(size_t iterations, dispatch_queue_t queue, void (^block)(size_t));
```

这个函数将 block 提交到分配队列多次使用。它需要三个参数：第一个指定执行的循环次数，第二个指定将要提交的队列，第三个是 block 的自身，block 需要一个单独的参数－用来表明当前循环的次数。

你可以简单的使用 `dispatch_apply` 打印出循环次数，例如：

```objc
#include <dispatch/dispatch.h>
size_t count = 10;
dispatch_queue_t queue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
 
dispatch_apply(count, queue, ^(size_t i) {
    printf("%u\n", i);
});
```

## 使用 Block 作为方法的参数

Cocoa 提供了一些用到了 block 的方法。你可以传递 block 作为参数，就像你传递的其它参数一样。

下面的例子选取任意出现在给定过滤集合数组中的前五个元素的索引：

```objc
NSArray *array = @[@"A", @"B", @"C", @"A", @"B", @"Z", @"G", @"are", @"Q"];
NSSet *filterSet = [NSSet setWithObjects: @"A", @"Z", @"Q", nil];
 
BOOL (^test)(id obj, NSUInteger idx, BOOL *stop);
 
test = ^(id obj, NSUInteger idx, BOOL *stop) {
 
    if (idx < 5) {
        if ([filterSet containsObject: obj]) {
            return YES;
        }
    }
    return NO;
};
 
NSIndexSet *indexes = [array indexesOfObjectsPassingTest:test];
 
NSLog(@"indexes: %@", indexes);
 
/*
Output:
indexes: <NSIndexSet: 0x10236f0>[number of indexes: 2 (in 2 ranges), indexes: (0 3)]
*/
```

下面的例子判断一个 `NSSet` 对象是否包含由本地变量指定的字符，若果找到了就设置另一个本地变量 (`found`) 的值为 `YES` (并停止搜索)。注意 `found` 定义为 `__block` 变量和 block 定义为內联方式传递：

```objc
__block BOOL found = NO;
NSSet *aSet = [NSSet setWithObjects: @"Alpha", @"Beta", @"Gamma", @"X", nil];
NSString *string = @"gamma";
 
[aSet enumerateObjectsUsingBlock:^(id obj, BOOL *stop) {
    if ([obj localizedCaseInsensitiveCompare:string] == NSOrderedSame) {
        *stop = YES;
        found = YES;
    }
}];
 
// At this point, found == YES

```

## 复制 Block

通常，你不需要 copy (或 retain) block。只有在你明确希望 block 在定义它的空间被销毁之后仍需继续使用才需要 copy。copy 会将 block 移动到堆中。

你可以使用 C 函数将 block 进行 copy 和 release。

```objc
Block_copy();
Block_release();
```

为了避免内存泄漏，你必须成对使用 `Block_copy` 和 `Block_release`。

## 要避免的模式

block 的词法 (`^{...}`) 是代表 block 的本地栈数据结构的地址。本地栈数据结构的空间因此是封闭复合声明，因此你要避免下面的例子的使用模式：

```objc
void dontDoThis() {
    void (^blockArray[3])(void);  // an array of 3 block references
 
    for (int i = 0; i < 3; ++i) {
        blockArray[i] = ^{ printf("hello, %d\n", i); };
        // WRONG: The block literal scope is the "for" loop.
        //block 的词法域是在 for 循环内。
    }
}
 
void dontDoThisEither() {
    void (^block)(void);
 
    int i = random():
    if (i > 1000) {
        block = ^{ printf("got i at: %d\n", i); };
        // WRONG: The block literal scope is the "then" clause.
        // block 的词法域是在 if 条件判断的括号内 { }
    }
    // ...
}

```

## 调试

你可以设置断点和单独进入到 block。也可以在 GDB session 使用 `invoke-block` 调用 block，例如下面的例子：

```objc
$ invoke-block myBlock 10 20
```

如果你想传递 C 字符串，你必须引用它，例如，传递 `"this string"` 到 `doSomethingWithString` block，你将要这样做：

```objc
$ invoke-block doSomethingWithString "\"this string\""
```

# 其它

## lexical scope 词法域

## 方法

类的函数。

## 函数

不属于类，直接创建的函数。