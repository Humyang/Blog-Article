layout: [post]
title: "JavaScript Object"
date: 2015-11-10 00:30:33
tags: 
- 前端
categories: 
- 前端
- JavaScript
id: "JavaScript-Object"

---


详细讲解如何创建 Object，操作 Object，和 Prototype 的使用。


<!-- more -->


---

资料来源 [W3School](http://www.w3schools.com/js/js_object_definition.asp)

# JavaScript Object

## Object 的定义

> 在 JavaScript 中，对象为王，如果你懂了 object，你就明白了 JavaScritp。

在 JavaScript 中，几乎一切都是 object。

* Booleans can be objects (or primitive data treated as objects)
* Numbers can be objects (or primitive data treated as objects)
* Strings can be objects (or primitive data treated as objects)
* Dates are always objects
* Maths are always objects
* Regular expressions are always objects
* Arrays are always objects
* Functions are always objects
* Objects are objects

在 JavaScript 中，除了 Primitive Value 外的所有值都是 Object。

**Primitive Value** 是: `strings ("John Doe")`, `numbers (3.14)`, `true`, `false`, `null`, and `undefined` 等。 

### Object 是包含变量的变量

JavaScript 变量可以包含单个值：

```javascript

var person = "John Doe";

```

Object 也是变量，但 object 能包含多个值。

值以 **name:value** 形式构成 (name  和 value 通过 `:` 分隔)。

```javascript

var person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};

```

JavaScript object 是一个无序变量的集合，被称为 `named values`。

### Object Properties

在 JavaScript object 中，命名 value 的属性被称为 `properties`。

### Object Methods

Method 是可以在 object 中执行的动作。

Object 的 properties 可以是 primitive values，其它 object，和 function。

Object method 是一个包含 function 定义的 object 属性。

> JavaScript object 是命名值的集装箱，包含了 propertie 和 method。

### 创建 JavaScript Object

这里有三种方式供你创建新对象：

* 使用 Object Literal 创建当个对象。
* 使用关键字 new 创建单个对象。
* 定义 object 构造函数，然后通过构造函数创建 object。

> 在 ECMAScript 5,对象也可以通过 Object.create() 函数创建。
 
#### 使用 Object Literal 创建

这是最简单的创建 JavaScript Object 的方式。

使用 Object Literal，定义和创建都在一个语句中完成。

Object literal 是 name:value 键值对的列表，包含在花括号 {} 内。

下面是使用 object literal 创建的例子：

```javascript

var person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};

```

#### 使用 JavaScript 关键字 new

下面的例子创建一个新的 JavaScript object 并设置是个 properties：

```javascript

var person = new Object();
person.firstName = "John";
person.lastName = "Doe";
person.age = 50;
person.eyeColor = "blue";

```

> 上面的两个例子做的事情完全一样，没有必要使用 `new Object()`。
> 为了简单，可读和执行速度，建议使用第一种方式 (object literal 方法)。

#### 使用 Object Constructor

上面的例子在许多情况下受限制。它们只能创建单个 object。

有时我们想有一个 “object 类型” 供我们用做创建多个同类型的 object。

标准的创建 "object 类型" 的方式是使用 object constructor 方法：

```javascript

function person(first, last, age, eye) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eye;
}
var myFather = new person("John", "Doe", 50, "blue");
var myMother = new person("Sally", "Rally", 48, "green");

```

上面的 function (person) 是一个 object constructor。

一旦你拥有了 object constructor，你可以使用相同的类型创建多个新 object。

```javascript

var myFather = new person("John", "Doe", 50, "blue");
var myMother = new person("Sally", "Rally", 48, "green");

```

### *this* 关键字

**this** 在不同的位置表示的值不一样。

在 JavaScript 中，**this** 表示 “拥有” 这段 JavaScript 代码的 object。

**this** 的值，被用在 function 内部时，代表 “拥有” 该 function 的 object。

**this** 的值，当用在 object 中时，代表 object 它本身。

关键字 **this** 在 object constructor 没有值，它表示新的 object。

但 constructor 被用做创建 object 时，**this** 的值将会变成将要创建的新 object。


> 注意 this 不是变量，它是关键字，你不能改变 **this** 的值。

### 内置的 JavaScript Constructor

JavaScript 有一系列内置的原生 object：

```javascript

var x1 = new Object();    // A new Object object
var x2 = new String();    // A new String object
var x3 = new Number();    // A new Number object
var x4 = new Boolean()    // A new Boolean object
var x5 = new Array();     // A new Array object
var	x6 = new RegExp();    // A new RegExp object
var x7 = new Function();  // A new Function object
var x8 = new Date();      // A new Date object

```

Math() object 不在列表中，因为 Math 是全局 object，new 关键字不能用在 Math 上。


>  **Did You Know**

如你所见，JavaScript 有 primitive 数据类型的 object 版本:String,Number,Boolean。

这里没有理由创建 complex object，Primitive values 执行速度快的多。

也没有理由使用 `new Array()`,使用 literal 替代：`[]`。

也没有理由使用 `new RegExp()`,使用 pattern literal 替代: `/()/`。

也没有理由使用 `new Function()`,使用 function 表达式替代:`function(){}`。

也没有理由使用 `new Object()`,使用 object literals 替代:`{}`。

```javascript

var x1 = {};            // new object
var x2 = "";            // new primitive string
var x3 = 0;             // new primitive number
var x4 = false;         // new primitive boolean
var x5 = [];            // new array	object
var	x6 = /()/           // new regexp object
var x7 = function(){};  // new function object

```

### JavaScript Object 是易变的

Object 是易变的：它们通过引用寻址，不是通过值。

如果 y 是 object，下面的语句不会创建 y 的副本。

```javascript

var x = y;  // This will not create a copy of y.

```

object x 不是 y 的副本，它就是 y，x 和 y 指向同一个 object。

任意对 y 的更改同样会更改 x，因为它们是同一个 object。

```javascript

var person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"}

var x = person;
x.age = 10;           // This will change both x.age and person.age

```

#### 复制 Object

如果直接将 Object 赋值给变量，得到的将会是内存地址的引用。

JavaScript 中没有提供原生复制 Object 的方式，如果想真正的复制 Object 值，可以使用下面的方式进行复制：

1.使用 jQuery 复制 Object：

```javascript

var a ＝ { k:1,t:2};
var b = {};
$.extend(b,a);

```

## Object Properties

### JavaScript for...in Loop

```javascript

for (variable in object) {
    code to be executed
}

```

### Deleting Properties

```javascript

var person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};
delete person.age;   // or delete person["age"]; 

```

The delete keyword deletes both the value of the property and the property itself.

After deletion, the property cannot be used before it is added back again.

The delete operator is designed to be used on **object properties**. It has **no effect** on **variables** or **functions**.

The delete operator should not be used on **predefined JavaScript object properties**. It can **crash your application**.


### Property Attributes

所有的 properties 都有 name，除此之外它们也有值。

这个值是 property 的 Attributes 之一。

这些 Attributes 是：enumberable，configurable，和 writable。

这些 Attribute 定义 property 可以如何访问 (是可读？还是可写？)。

在 JavaScript 中，所有 attribute 都可以读，但只有 value attribute 可以被更改 (只有 property 是 writable 时)。

(ECMAScript 5 对所有 property attributes 提供了 getting method 和 setting method。 

### Prototype Properties

JavaScript object 由它的 **prototype properties** 继承。

delete 关键字无法删除继承的 properties，但如果你删除 prototype property，它将会影响从该 prototype 继承的所有 object。

## Object Methods

A JavaScript **method** is a property containing a **function definition**.

> Methods are functions stored as object properties.


## Object Prototypes


每一个 JavaScript object 都有 prototype。prototype 也是一个 object。

所有 JavaScript object 都从它的 prototype 中继承 properties 和 methods。

使用 object literal 或 new Object() 创建的 object，都从 Object.prototype 继承。

使用 new Date() 创建的 object 从 Date.prototype 继承。

Object.prototype 是 prototype 链的顶部。

所有 JavaScript 对象 (Date,Array,RegExp,Function,...) 都从 Object.prototype 继承。

### 创建 Prototype

创建 prototype 的标准方式是使用 object construct function:

```javascript

function person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}

```

通过 constructor function，你可以使用 **new** 关键字从相同的 prototype 创建新的 object。

```javascript

var myFather = new person("John", "Doe", 50, "blue");
var myMother = new person("Sally", "Rally", 48, "green");

```

### 添加 Properties 和 Methods 到 Objects

有时你想添加新的 properties (或 methods) 到已有的 object。

有时你想添加新的 properties (或 methods) 到所有已有且指定类型的 object。

有时你想添加新的 properties (或 methods) 到一个 object 的 prototype。

#### 添加 Property 到一个 object

```javascript

myFather.nationality = "English";

```

#### 添加 Method 到 object

```javascript

myFather.name = function () {
    return this.firstName + " " + this.lastName;
};

```

添加 Properties 到 Prototype

你不能像添加 Method 和 Property 到 object 中一样添加新 property 到 prototype，因为 prototype 不是一个存在的 object。

要添加新 property 到 constructor，你必须添加它到 constructor function。

```javascript

function person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
    this.nationality = "English"
}

```


#### 添加 Methods 到 Prototype

你的 constructor function 也可以定义 methods：

```javascript

function person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
    this.name = function() {return this.firstName + " " + this.lastName;};
}

```

#### 使用 prototype Property

JavaScript prototype property 允许你添加新的 properties 到现有的 prototype：

```javascript

function person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}
person.prototype.nationality = "English";

```

JavaScript prototype property 也允许你添加新的方法到现有的 prototype：

```javascript

function person(first, last, age, eyecolor) {
    this.firstName = first;
    this.lastName = last;
    this.age = age;
    this.eyeColor = eyecolor;
}
person.prototype.name = function() {
    return this.firstName + " " + this.lastName;
};

```

> 永远只修改你拥有的 prototype。永远不要修改标准 JavaScript object的 prototypes。