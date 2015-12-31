layout: [post]
title: "JavaScript 基础知识"
date: 2015-11-09 00:04:55
tags: 
- 前端 
categories: 
- 前端
- JavaScript
id: "WebDevelopJavaScript"

---


一些 JavaScript 的基础知识。

<!-- more -->


---

# 常用参考

[JavaScript 参考手册](http://www.w3school.com.cn/jsref/index.asp)

[JS & DOM 参考手册](http://www.w3school.com.cn/jsref/index.asp)

[HTML DOM Style 对象属性参考手册](http://www.w3school.com.cn/jsref/dom_obj_style.asp)

[HTML DOM Event 对象参考手册。](http://www.w3school.com.cn/jsref/dom_obj_event.asp)

# JavaScript 基础

资料来自 [W3School](http://www.w3school.com.cn/js/js_datatypes.asp)。

## JavaScript 数据类型

JavaScript 数据类型包括字符串、数字、布尔、数组、对象、Null、Undefined。

JavaScript 拥有动态类型。这意味着相同的变量可用作不同的类型：

```javascript

var x                // x 为 undefined
var x = 6;           // x 为数字
var x = "Bill";      // x 为字符串

```

### JavaScript 数组
下面的代码创建名为 cars 的数组：

```javascript

var cars=new Array();
cars[0]="Audi";
cars[1]="BMW";
cars[2]="Volvo";

```

或者 (condensed array):

```javascript

var cars=new Array("Audi","BMW","Volvo");

```

或者 (literal array):

```javascript

var cars=["Audi","BMW","Volvo"];

```

### JavaScript 对象

JavaScript 对象
对象由花括号分隔。在括号内部，对象的属性以名称和值对的形式 (name : value) 来定义。属性由逗号分隔：


```javascript
var person={firstname:"Bill", lastname:"Gates", id:5566};
```

对象属性有两种寻址方式：

```javascript

name=person.lastname;
name=person["lastname"];

```

### Undefined 和 Null

Undefined 这个值表示变量不含有值。
可以通过将变量的值设置为 null 来清空变量。
实例

```javascript

cars=null;
person=null;
```

### 声明变量类型

当您声明新变量时，可以使用关键词 "new" 来声明其类型：

```javascript
var carname=new String;
var x=      new Number;
var y=      new Boolean;
var cars=   new Array;
var person= new Object;

```
JavaScript 变量均为对象。当您声明一个变量时，就创建了一个新的对象。

JavaScript 高级教程：

[ECMAScript 原始类型](http://www.w3school.com.cn/js/pro_js_primitivetypes.asp)

[ECMAScript 类型转换](http://www.w3school.com.cn/js/pro_js_typeconversion.asp)

[ECMAScript 引用类型](http://www.w3school.com.cn/js/pro_js_referencetypes.asp)

## JavaScript 对象

JavaScript 中的所有事物都是对象：字符串、数字、数组、日期，等等。
在 JavaScript 中，对象是拥有属性和方法的数据。

在 JavaScript 中，对象是数据（变量），拥有属性和方法。

当您像这样声明一个 JavaScript 变量时：

```javascript
var txt = "Hello";
```

您实际上已经创建了一个 JavaScript 字符串对象。字符串对象拥有内建的属性 length。对于上面的字符串来说，length 的值是 5。字符串对象同时拥有若干个内建的方法。

```javascript
txt.indexOf();

txt.replace();

txt.search();
```

### 创建 JavaScript 对象
你也可以创建自己的对象。
本例创建名为 "person" 的对象，并为其添加了四个属性：
实例

```javascript

person=new Object();
person.firstname="Bill";
person.lastname="Gates";
person.age=56;
person.eyecolor="blue";

```

## JavaScript 函数

### 局部 JavaScript 变量

在 JavaScript 函数内部声明的变量（使用 var）是局部变量，所以只能在函数内部访问它。（该变量的作用域是局部的）。
您可以在不同的函数中使用名称相同的局部变量，因为只有声明过该变量的函数才能识别出该变量。
只要函数运行完毕，本地变量就会被删除。

### 全局 JavaScript 变量

在函数外声明的变量是全局变量，网页上的所有脚本和函数都能访问它。

### JavaScript 变量的生存期

JavaScript 变量的生命期从它们被声明的时间开始。
局部变量会在函数运行以后被删除。
全局变量会在页面关闭后被删除。

### 向未声明的 JavaScript 变量来分配值

如果您把值赋给尚未声明的变量，该变量将被自动作为全局变量声明。
这条语句：
carname="Volvo";
将声明一个全局变量 carname，即使它在函数内执行。

## JavaScript 运算符

JavaScript 赋值运算符
赋值运算符用于给 JavaScript 变量赋值。
给定 x=10 和 y=5，下面的表格解释了赋值运算符：

运算符 | 例子 | 等价于 | 结果
------------- | ------------- | ------------- | -------------
=	| x=y	 | 	x=5
+=	| x+=y	| x=x+y | 	x=15
-=	| x-=y	| x=x-y | 	x=5
*=	| x*=y	| x=x*y | 	x=50
/=	| x/=y	| x=x/y | 	x=2
%=	| x%=y	| x=x%y | 	x=0

###  + 运算符

如果把数字与字符串相加，结果将成为字符串。

### 比较运算符

比较运算符在逻辑语句中使用，以测定变量或值是否相等。
给定 x=5，下面的表格解释了比较运算符：

运算符	 | 描述	 | 例子
------------- | ------------- | -------------
==	 | 等于	 | x==8 为 false
===	 | 全等（值和类型） | 	 x === 5 为 true; x==="5" 为 false
!=	 | 不等于	 | x!=8 为 true
 >	 | 大于	 |  x>8 为 false 
<	 | 小于	 | x<8 为 true
 >=	 | 大于 | 或等于 | 	x>=8 为 false
<=	 | 小于 | 或等于 | 	x<=8 为 true

## JavaScript 的 For 循环

不同类型的循环
JavaScript 支持不同类型的循环：

* **for** - 循环代码块一定的次数
* **for/in** - 循环遍历对象的属性
* **while** - 当指定的条件为 true 时循环指定的代码块
* **do/while** - 同样当指定的条件为 true 时循环指定的代码块

### For 循环
for 循环是您在希望创建循环时常会用到的工具。
下面是 for 循环的语法：

```javascript

for (语句 1; 语句 2; 语句 3)
  {
  被执行的代码块
  }

```

* 语句 1 在循环（代码块）开始前执行
* 语句 2 定义运行循环（代码块）的条件
* 语句 3 在循环（代码块）已被执行之后执行

#### 语句 1
通常我们会使用语句 1 初始化循环中所用的变量 (var i=0)。
<br />
语句 1 是可选的，也就是说不使用语句 1 也可以。
<br />
您可以在语句 1 中初始化任意（或者多个）值：

同时您还可以省略语句 1（比如在循环开始前已经设置了值时）：

```javascript
var i=2,len=cars.length;
for (; i<len; i++)
{
document.write(cars[i] + "<br>");
}
```

#### 语句 2
通常语句 2 用于评估初始变量的条件。

语句 2 同样是可选的。

如果语句 2 返回 true，则循环再次开始，如果返回 false，则循环将结束。

提示：如果您省略了语句 2，那么必须在循环内提供 break，否则循环就无法停下来。这样有可能令浏览器崩溃。
请在本教程稍后的章节阅读有关 break 的内容。

#### 语句 3
通常语句 3 会增加初始变量的值。

语句 3 也是可选的。

语句 3 有多种用法。增量可以是负数 (i--)，或者更大 (i=i+15)。

语句 3 也可以省略（比如当循环内部有相应的代码时）：

```javascript
var i=0,len=cars.length;
for (; i<len; )
{
document.write(cars[i] + "<br>");
i++;
}
```

### For/In 循环

JavaScript for/in 语句循环遍历对象的属性：

```javascript


var person={fname:"John",lname:"Doe",age:25};

for (x in person)
  {
  txt=txt + person[x];
  }

```

### do/while 循环

do/while 循环是 while 循环的变体。该循环会执行一次代码块，在检查条件是否为真之前，然后如果条件为真的话，就会重复这个循环:

```javascript
do
  {
  需要执行的代码
  }
while (条件);
```

## JavaScript Break 和 Continue 语句

break 语句用于跳出循环。

continue 用于跳过循环中的一个迭代。

### JavaScript 标签

正如您在 switch 语句那一章中看到的，可以对 JavaScript 语句进行标记。
如需标记 JavaScript 语句，请在语句之前加上冒号：

```
label:
语句
```

break 和 continue 语句仅仅是能够跳出代码块的语句。

语法

```
break labelname;

continue labelname;
```

continue 语句（带有或不带标签引用）只能用在循环中。
break 语句（不带标签引用），只能用在循环或 switch 中。
通过标签引用，break 语句可用于跳出任何 JavaScript 代码块：
实例

```javascript
cars=["BMW","Volvo","Saab","Ford"];
list:
{
document.write(cars[0] + "<br>");
document.write(cars[1] + "<br>");
document.write(cars[2] + "<br>");
break list;
document.write(cars[3] + "<br>");
document.write(cars[4] + "<br>");
document.write(cars[5] + "<br>");
}
```

## JavaScript 错误处理 - Throw、Try 和 Catch

**try** 语句测试代码块的错误。
**catch** 语句处理错误。
**throw** 语句创建自定义错误。

### 错误发生的原因

 当 JavaScript 引擎执行 JavaScript 代码时，会发生各种错误： 
 
可能是语法错误，通常是程序员造成的编码错误或错别字。

可能是拼写错误或语言中缺少的功能（可能由于浏览器差异）。

可能是由于来自服务器或用户的错误输出而导致的错误。

当然，也可能是由于许多其他不可预知的因素。

### 抛出错误

当错误发生时，JavaScript 引擎通常会停止，并生成一个错误消息。

### 检测和捕捉错误

**try** 语句允许我们定义在执行时进行错误测试的代码块。

**catch** 语句允许我们定义当 **try** 代码块发生错误时，所执行的代码块。

JavaScript 语句 **try** 和 **catch** 是成对出现的。

```javascript
try
  {
  //在这里运行代码
  }
catch(err)
  {
  //在这里处理错误
  }
```

### Throw 语句

throw 语句允许我们创建自定义错误。

正确的技术术语是：创建或抛出异常（exception）。

如果把 throw 与 try 和 catch 一起使用，那么您能够控制程序流，并生成自定义的错误消息。

#### 语法

`throw exception`

异常可以是 JavaScript 字符串、数字、逻辑值或对象。

```javascript
<script>
function myFunction()
{
try
  {
  var x=document.getElementById("demo").value;
  if(x=="")    throw "empty";
  if(isNaN(x)) throw "not a number";
  if(x>10)     throw "too high";
  if(x<5)      throw "too low";
  }
catch(err)
  {
  var y=document.getElementById("mess");
  y.innerHTML="Error: " + err + ".";
  }
}
</script>

<h1>My First JavaScript</h1>
<p>Please input a number between 5 and 10:</p>
<input id="demo" type="text">
<button type="button" onclick="myFunction()">Test Input</button>
<p id="mess"></p>


```

## JavaScript 验证

### 表单验证


```html
<html>
<head>
<script type="text/javascript">

function validate_required(field,alerttxt)
{
with (field)
  {
  if (value==null||value=="")
    {alert(alerttxt);return false}
  else {return true}
  }
}

function validate_form(thisform)
{
with (thisform)
  {
  if (validate_required(email,"Email must be filled out!")==false)
    {email.focus();return false}
  }
}
</script>
</head>

<body>
<form action="submitpage.htm" onsubmit="return validate_form(this)" method="post">
Email: <input type="text" name="email" size="30">
<input type="submit" value="Submit"> 
</form>
</body>

</html>
```

### E-mail 验证

```html
<html>
<head>
<script type="text/javascript">
function validate_email(field,alerttxt)
{
with (field)
{
apos=value.indexOf("@")
dotpos=value.lastIndexOf(".")
if (apos<1||dotpos-apos<2) 
  {alert(alerttxt);return false}
else {return true}
}
}

function validate_form(thisform)
{
with (thisform)
{
if (validate_email(email,"Not a valid e-mail address!")==false)
  {email.focus();return false}
}
}
</script>
</head>

<body>
<form action="submitpage.htm"onsubmit="return validate_form(this);" method="post">
Email: <input type="text" name="email" size="30">
<input type="submit" value="Submit"> 
</form>
</body>

</html>
```

# JavaScript HTML DOM

HTML DOM (文档对象模型)

当网页被加载时，浏览器会创建页面的文档对象模型 (Document Object Model)

文档对象模型被构造为对象的树。

通过可编程的对象模型，JavaScript 获得了足够的能力来创建动态的 HTML:

* JavaScript 能够改变页面中的所有 HTML 元素
* JavaScript 能够改变页面中的所有 HTML 属性
* JavaScript 能够改变页面中的所有 CSS 样式
* JavaScript 能够对页面中的所有事件做出反应

## 查找 HTML 元素

### 通过 id 查找 HTML 元素

在 DOM 中查找 HTML 元素的最简单的方法，是通过使用元素的 id。

本例查找 id="intro" 元素：

```javascript
var x=document.getElementById("intro");
```

如果找到该元素，则该方法将以对象（在 x 中）的形式返回该元素。

如果未找到该元素，则 x 将包含 null。

### 通过标签名查找 HTML 元素

本例查找 id="main" 的元素，然后查找 "main" 中的所有 <p> 元素

```javascript
var x=document.getElementById("main");
var y=x.getElementsByTagName("p");
```

**提示**：通过类名查找 HTML 元素在 IE 5,6,7,8 中无效。

## JavaScript 改变 HTML

### 直接向 HTML 输出流写内容

```javascript
<script>
document.write(Date());
</script>
```
**提示**：绝不要使用在文档加载之后使用 document.write()。这会覆盖该文档。

### 改变 HTML 内容

修改 HTML 内容的最简单的方法时使用 innerHTML 属性。

如需改变 HTML 元素的内容，请使用这个语法：

```javascript
document.getElementById(id).innerHTML=new HTML
```

实例
本例改变了 `<p>` 元素的内容：

```html
<html>
<body>

<p id="p1">Hello World!</p>

<script>
document.getElementById("p1").innerHTML="New text!";
</script>

</body>
</html>

```

本例改变了 `<h1>` 元素的内容：

```html

<!DOCTYPE html>
<html>
<body>

<h1 id="header">Old Header</h1>

<script>
var element=document.getElementById("header");
element.innerHTML="New Header";
</script>

</body>
</html>

```

### 改变 HTML 属性

如需改变 HTML 元素的属性，请使用这个语法：

```javascript

document.getElementById(id).attribute=new value
```

本例改变了 `<img>` 元素的 `src` 属性：

```html

<!DOCTYPE html>
<html>
<body>

<img id="image" src="smiley.gif">

<script>
document.getElementById("image").src="landscape.jpg";
</script>

</body>
</html>
```

## JavaScript 改变 CSS

如需改变 HTML 元素的样式，请使用这个语法：

```javascript
document.getElementById(id).style.property=new style
```

下面的例子会改变 `<p>` 元素的样式：

```html
<p id="p2">Hello World!</p>

<script>
document.getElementById("p2").style.color="blue";
</script>
```

本例改变了 `id="id1"` 的 HTML 元素的样式，当用户点击按钮时：

```javascript
<h1 id="id1">My Heading 1</h1>

<button type="button" onclick="document.getElementById('id1').style.color='red'">
点击这里
</button>
```


[HTML DOM Style 对象属性参考手册](http://www.w3school.com.cn/jsref/dom_obj_style.asp)

## JavaScript HTML DOM 事件

JavaScript 有能力对 HTML 事件做出反应。

### 对事件做出反应

如需在用户点击某个元素时执行代码，请向一个 HTML 事件属性添加 JavaScript 代码：

```javascript
onclick=JavaScript
```
HTML 事件的例子：

* 当用户点击鼠标时
* 当网页已加载时
* 当图像已加载时
* 当鼠标移动到元素上时
* 当输入字段被改变时
* 当提交 HTML 表单时
* 当用户触发按键时

在本例中，当用户在 `<h1>` 元素上点击时，会改变其内容：

```javascript
<h1 onclick="this.innerHTML='谢谢!'">请点击该文本</h1>
```

本例从事件处理器调用一个函数：

```javascript

<!DOCTYPE html>
<html>
<head>
<script>
function changetext(id)
{
id.innerHTML="谢谢!";
}
</script>
</head>
<body>
<h1 onclick="changetext(this)">请点击该文本</h1>
</body>
</html>

```


### HTML 事件属性

如需向 HTML 元素分配 事件，您可以使用事件属性。

向 button 元素分配 onclick 事件：

```javascript
<button onclick="displayDate()">点击这里</button>
```


### 使用 HTML DOM 来分配事件

HTML DOM 允许您通过使用 JavaScript 来向 HTML 元素分配事件：

```javascript
<script>
document.getElementById("myBtn").onclick=function(){displayDate()};
</script>
```

### onload 和 onunload 事件

onload 和 onunload 事件会在用户进入或离开页面时被触发。

onload 事件可用于检测访问者的浏览器类型和浏览器版本，并基于这些信息来加载网页的正确版本。

onload 和 onunload 事件可用于处理 cookie。

```javascript
<body onload="checkCookies()">
```

### onchange 事件

onchange 事件常结合对输入字段的验证来使用。

下面是一个如何使用 onchange 的例子。当用户改变输入字段的内容时，会调用 upperCase() 函数。
实例

```html
<input type="text" id="fname" onchange="upperCase()">
```


[HTML DOM Event 对象参考手册。](http://www.w3school.com.cn/jsref/dom_obj_event.asp)

## JavaScript HTML DOM 元素（节点)

### 创建新的 HTML 元素

如需向 HTML DOM 添加新元素，您必须首先创建该元素（元素节点），然后向一个已存在的元素追加该元素。

```html
<div id="div1">
<p id="p1">这是一个段落</p>
<p id="p2">这是另一个段落</p>
</div>

<script>
var para=document.createElement("p");
var node=document.createTextNode("这是新段落。");
para.appendChild(node);

var element=document.getElementById("div1");
element.appendChild(para);
</script>
```

### 删除已有的 HTML 元素

如需删除 HTML 元素，您必须首先获得该元素的父元素：

```javascript
<div id="div1">
<p id="p1">这是一个段落。</p>
<p id="p2">这是另一个段落。</p>
</div>

<script>
var parent=document.getElementById("div1");
var child=document.getElementById("p1");
parent.removeChild(child);
</script>
```

> **提示**：如果能够在不引用父元素的情况下删除某个元素，就太好了。
> 不过很遗憾。DOM 需要清楚您需要删除的元素，以及它的父元素。
 
 这是常用的解决方案：找到您希望删除的子元素，然后使用其 parentNode 属性来找到父元素：
 
```javascript
var child=document.getElementById("p1");
child.parentNode.removeChild(child);

```

如果您希望学到更多有关使用 JavaScript 访问 HTML DOM 的知识，请访问完整的 [HTML DOM 教程](http://www.w3school.com.cn/htmldom/index.asp)。

# JavaScript 对象

## JavaScript 对象

JavaScript 中的所有事物都是对象：字符串、数值、数组、函数...

此外，JavaScript 允许自定义对象。

JavaScript 提供多个内建对象，比如 String、Date、Array 等等。

对象只是带有属性和方法的特殊数据类型。

### 创建 JavaScript 对象

通过 JavaScript，您能够定义并创建自己的对象。

创建新对象有两种不同的方法：

* 定义并创建对象的实例
* 使用函数来定义对象，然后创建新的对象实例

#### 创建直接的实例

这个例子创建了对象的一个新实例，并向其添加了四个属性：

```javascript
person=new Object();
person.firstname="Bill";
person.lastname="Gates";
person.age=56;
person.eyecolor="blue";
```

#### 替代语法（使用对象 literals）：

```javascript
person={firstname:"John",lastname:"Doe",age:50,eyecolor:"blue"};
```

#### 使用对象构造器


```javascript

function person(firstname,lastname,age,eyecolor)
{
this.firstname=firstname;
this.lastname=lastname;
this.age=age;
this.eyecolor=eyecolor;
}
```

一旦您有了对象构造器，就可以创建新的对象实例，就像这样：

```javascript
var myFather=new person("Bill","Gates",56,"blue");
var myMother=new person("Steve","Jobs",48,"green");
```

### 把属性添加到 JavaScript 对象

您可以通过为对象赋值，向已有对象添加新属性：

假设 personObj 已存在 - 您可以为其添加这些新属性：firstname、lastname、age 以及 eyecolor：

```javascript
person.firstname="Bill";
person.lastname="Gates";
person.age=56;
person.eyecolor="blue";

x=person.firstname;


```

### 把方法添加到 JavaScript 对象

方法只不过是附加在对象上的函数。

在构造器函数内部定义对象的方法：

```javascript
function person(firstname,lastname,age,eyecolor)
{
this.firstname=firstname;
this.lastname=lastname;
this.age=age;
this.eyecolor=eyecolor;

this.changeName=changeName;
function changeName(name)
{
this.lastname=name;
}
}
```

现在您可以试一下：

```javascript
myMother.changeName("Ballmer");
```

### JavaScript 类 (prototype)

JavaScript 是面向对象的语言，但 JavaScript 不使用类。

在 JavaScript 中，不会创建类，也不会通过类来创建对象（就像在其他面向对象的语言中那样）。

JavaScript 基于 prototype，而不是基于类的。

[ECMAScript 面向对象技术]()

### JavaScript for...in 循环

JavaScript for...in 语句循环遍历对象的属性。

```javascript
语法
for (对象中的变量)
  {
  要执行的代码
  }
```

**注释**：for...in 循环中的代码块将针对每个属性执行一次。

循环遍历对象的属性：

```javascript
var person={fname:"Bill",lname:"Gates",age:56};

for (x in person)
  {
  txt=txt + person[x];
  }
```

## Number 对象

JavaScript 只有一种数字类型。

可以使用也可以不使用小数点来书写数字。

实例

```javascript
var pi=3.14;    // 使用小数点
var x=34;       // 不使用小数点


```

极大或极小的数字可通过科学（指数）计数法来写：

```javascript

var y=123e5;    // 12300000
var z=123e-5;   // 0.00123

```

### 所有 JavaScript 数字均为 64 位

JavaScript 不是类型语言。与许多其他编程语言不同，JavaScript 不定义不同类型的数字，比如整数、短、长、浮点等等。

JavaScript 中的所有数字都存储为根为 10 的 64 位（8 比特），浮点数。

### 精度

整数（不使用小数点或指数计数法）最多为 15 位。

小数的最大位数是 17，但是浮点运算并不总是 100% 准确：

实例

```javascript

var x=0.2+0.1;

```

### 八进制和十六进制

如果前缀为 0，则 JavaScript 会把数值常量解释为八进制数，如果前缀为 0 和 "x"，则解释为十六进制数。

```javascript
var y=0377;
var z=0xFF;
```

**提示**：绝不要在数字前面写零，除非您需要进行八进制转换。

数字属性和方法
属性：

* MAX VALUE
* MIN VALUE
* NEGATIVE INFINITIVE
* POSITIVE INFINITIVE
* NaN
* prototype
* constructor

方法：

* toExponential()
* toFixed()
* toPrecision()
* toString()
* valueOf()


### 完整的 Number 对象参考手册

如需可用于 Number 对象的所有属性和方法的完整参考，请访问[ Number 对象参考手册](http://www.w3school.com.cn/jsref/jsref_obj_number.asp)。

该参考手册包含每个属性和方法的描述和实例。

## 字符串(String)对象

### String 对象

String 对象用于处理文本（字符串）。
创建 String 对象的语法：

```javascript
new String(s);
String(s);
```

参数 s 是要存储在 String 对象中或转换成原始字符串的值。


当 String() 和运算符 new 一起作为构造函数使用时，它返回一个新创建的 String 对象，存放的是字符串 s 或 s 的字符串表示。

当不用 new 运算符调用 String() 时，它只把 s 转换成原始的字符串，并返回转换后的值。


[JavaScript String 对象参考手册](http://www.w3school.com.cn/jsref/jsref_obj_string.asp)

## Date（日期）对象

### 创建 Date 对象的语法：

```javascript

var myDate=new Date()

var strDate=Date() //返回当前日期的字符串形式
```
注释：Date 对象会自动把当前日期和时间保存为其初始值。

### 比较日期
日期对象也可用于比较两个日期。

下面的代码将当前日期与 2008 年 8 月 9 日做了比较：

```javascript

var myDate=new Date();
myDate.setFullYear(2008,8,9);

var today = new Date();

if (myDate>today)
{
alert("Today is before 9th August 2008");
}
else
{
alert("Today is after 9th August 2008");
}

```
[JavaScript Date 对象参考手册](http://www.w3school.com.cn/jsref/jsref_obj_date.asp)

## Array（数组）对象

数组对象的作用是：使用单独的变量名来存储一系列的值。

创建数组
创建数组，为其赋值，然后输出这些值。

```javascript

var mycars=new Array("Saab","Volvo","BMW")

var mycars = new Array()
mycars[0] = "Saab"
mycars[1] = "Volvo"
mycars[2] = "BMW"

var mycars = ["asd","asdasd"]

for (i=0;i<mycars.length;i++)
{
document.write(mycars[i] + "<br />")
}
```

For...In 声明
使用 for...in 声明来循环输出数组中的元素。

```javascript
var x
var mycars = new Array()
mycars[0] = "Saab"
mycars[1] = "Volvo"
mycars[2] = "BMW"

for (x in mycars)
{
document.write(mycars[x] + "<br />")
}
```

合并两个数组 - concat()
如何使用 concat() 方法来合并两个数组。

```javascript
var arr = new Array(3)
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"

var arr2 = new Array(3)
arr2[0] = "James"
arr2[1] = "Adrew"
arr2[2] = "Martin"

document.write(arr.concat(arr2))

```

用数组的元素组成字符串 - join()
如何使用 join() 方法将数组的所有元素组成一个字符串。

```javascript
var arr = new Array(3);
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"

document.write(arr.join());

document.write("<br />");

document.write(arr.join("."));
```

文字数组 - sort()
如何使用 sort() 方法从字面上对数组进行排序。

```javascript
var arr = new Array(6)
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"
arr[3] = "James"
arr[4] = "Adrew"
arr[5] = "Martin"

document.write(arr + "<br />")
document.write(arr.sort())
```

数字数组 - sort()
如何使用 sort() 方法从数值上对数组进行排序。

```javascript
function sortNumber(a, b)
{
return a - b
}

var arr = new Array(6)
arr[0] = "10"
arr[1] = "5"
arr[2] = "40"
arr[3] = "25"
arr[4] = "1000"
arr[5] = "1"

document.write(arr + "<br />")
document.write(arr.sort(sortNumber))

```

## Boolean（逻辑）对象

Boolean（逻辑）对象用于将非逻辑值转换为逻辑值（true 或者 false）。

[JavaScript Boolean 对象参考手册](http://www.w3school.com.cn/jsref/jsref_obj_boolean.asp)

### 创建 Boolean 对象

使用关键词 new 来定义 Boolean 对象。下面的代码定义了一个名为 myBoolean 的逻辑对象：

```javascript
var myBoolean=new Boolean()
```

注释：如果逻辑对象无初始值或者其值为 0、-0、null、""、false、undefined 或者 NaN，那么对象的值为 false。否则，其值为 true（即使当自变量为字符串 "false" 时）！

下面的所有的代码行均会创建初始值为 false 的 Boolean 对象。

```javascript
var myBoolean=new Boolean();
var myBoolean=new Boolean(0);
var myBoolean=new Boolean(null);
var myBoolean=new Boolean("");
var myBoolean=new Boolean(false);
var myBoolean=new Boolean(NaN);
```

下面的所有的代码行均会创初始值为 true 的 Boolean 对象：

```javascript

var myBoolean=new Boolean(1);
var myBoolean=new Boolean(true);
var myBoolean=new Boolean("true");
var myBoolean=new Boolean("false");
var myBoolean=new Boolean("Bill Gates");
```

## Math（算数）对象

Math（算数）对象的作用是：执行常见的算数任务。

### 使用 Math 的属性和方法的语法：

```javascript
var pi_value=Math.PI;
var sqrt_value=Math.sqrt(15);
```

[JavaScript Math 对象的参考手册](http://www.w3school.com.cn/jsref/jsref_obj_math.asp)

算数值
JavaScript 提供 8 种可被 Math 对象访问的算数值：

* 常数
* 圆周率
* 2 的平方根
* 1/2 的平方根
* 2 的自然对数
* 10 的自然对数
* 以 2 为底的 e 的对数
* 以 10 为底的 e 的对数

这是在 Javascript 中使用这些值的方法：（与上面的算数值一一对应）

* Math.E
* Math.PI
* Math.SQRT2
* Math.SQRT1_2
* Math.LN2
* Math.LN10
* Math.LOG2E
* Math.LOG10E

## RegExp 对象


RegExp 对象用于规定在文本中检索的内容。

[RegExp 对象参考手册](http://www.w3school.com.cn/jsref/jsref_obj_regexp.asp)
### 什么是 RegExp？
RegExp 是正则表达式的缩写。

当您检索某个文本时，可以使用一种模式来描述要检索的内容。RegExp 就是这种模式。

简单的模式可以是一个单独的字符。

更复杂的模式包括了更多的字符，并可用于解析、格式检查、替换等等。

您可以规定字符串中的检索位置，以及要检索的字符类型，等等。

### 定义 RegExp

RegExp 对象用于存储检索模式。

通过 new 关键词来定义 RegExp 对象。以下代码定义了名为 patt1 的 RegExp 对象，其模式是 "e"：

```javascript
var patt1=new RegExp("e");
```

### RegExp 对象的方法

RegExp 对象有 3 个方法：test()、exec() 以及 compile()。

#### test()
test() 方法检索字符串中的指定值。返回值是 true 或 false。
例子：

```javascript

var patt1=new RegExp("e");

document.write(patt1.test("The best things in life are free")); 

```

由于该字符串中存在字母 "e"，以上代码的输出将是：

```javascript
true
```

#### exec()

exec() 方法检索字符串中的指定值。返回值是被找到的值。如果没有发现匹配，则返回 null。

```javascript

var patt1=new RegExp("e");

document.write(patt1.exec("The best things in life are free")); 
```

您可以向 RegExp 对象添加第二个参数，以设定检索。例如，如果需要找到所有某个字符的所有存在，则可以使用 "g" 参数 ("global")。

在使用 "g" 参数时，exec() 的工作原理如下：

找到第一个 "e"，并存储其位置

如果再次运行 exec()，则从存储的位置开始检索，并找到下一个 "e"，并存储其位置

```javascript
var patt1=new RegExp("e","g");
do
{
result=patt1.exec("The best things in life are free");
document.write(result);
}
while (result!=null) 
```

由于这个字符串中 6 个 "e" 字母，代码的输出将是：

```javascript
eeeeeenull
```

#### compile()

compile() 方法用于改变 RegExp。

compile() 既可以改变检索模式，也可以添加或删除第二个参数。

```javascript
var patt1=new RegExp("e");

document.write(patt1.test("The best things in life are free"));

patt1.compile("d");

document.write(patt1.test("The best things in life are free"));
```

由于字符串中存在 "e"，而没有 "d"，以上代码的输出是：

```javascript
truefalse
```

## JavaScript Type Conversion

Original Value | Converted to Number | 	Converted to String |  Converted to Boolean
------------- | -------------| -------------| -------------
false | 	0	 | "false"	 | false	 | 
true | 	1 | 	"true" | 	true | 	
0 | 	0 | 	"0" | 	false | 	
1 | 	1 | 	"1"	 | true	
"0" | 	0	 | "0" | 	true	
"1" | 	1	 | "1"	 | true	
NaN | 	NaN | 	"NaN" | 	false	
Infinity | 	Infinity | 	"Infinity" | 	true	
-Infinity | 	-Infinity | 	"-Infinity" | true
"" | 	0 | 	"" | 	false	
"20" | 	20	 | "20" | 	true	
"twenty" | 	NaN	 | "twenty" | 	true	
[ ]	 | 0	 | "" | 	true	
[20]	 | 20	 | "20" | 	true	
[10,20] | 	NaN	 | "10,20" | 	true	
["twenty"] | 	NaN | 	"twenty" | 	true	
["ten","twenty"] | 	NaN | 	"ten,twenty" | true
function(){} | 	NaN | 	"function(){}" | true
{ } | 	NaN	 | "[object Object]" | true	
null | 	0	 | "null"	 | false	
undefined | 	NaN	 | "undefined"	 | false

# JavaScript BOM (浏览器对象模型)

浏览器对象模型（Browser Object Model）尚无正式标准。
由于现代浏览器已经（几乎）实现了 JavaScript 交互性方面的相同方法和属性，因此常被认为是 BOM 的方法和属性。

## Window 

所有浏览器都支持 window 对象。它表示浏览器窗口。

所有 JavaScript 全局对象、函数以及变量均自动成为 window 对象的成员。

全局变量是 window 对象的属性。

全局函数是 window 对象的方法。

甚至 HTML DOM 的 document 也是 window 对象的属性之一:

```javascript
window.document.getElementById("header");
```

与此相同

```javascript
document.getElementById("header");
```

### Window 尺寸

有三种方法能够确定浏览器窗口的尺寸（浏览器的视口，不包括工具栏和滚动条）。

对于Internet Explorer、Chrome、Firefox、Opera 以及 Safari：

```javascript

window.innerHeight - 浏览器窗口的内部高度
window.innerWidth - 浏览器窗口的内部宽度

```

对于 Internet Explorer 8、7、6、5：

```javascript

document.documentElement.clientHeight
document.documentElement.clientWidth

```

或者

```javascript


document.body.clientHeight
document.body.clientWidth

```

实用的 JavaScript 方案（涵盖所有浏览器）：

```javascript

var w=window.innerWidth
|| document.documentElement.clientWidth
|| document.body.clientWidth;

var h=window.innerHeight
|| document.documentElement.clientHeight
|| document.body.clientHeight;

```


一些其他方法：

* window.open() - 打开新窗口
* window.close() - 关闭当前窗口
* window.moveTo() - 移动当前窗口
* window.resizeTo() - 调整当前窗口的尺寸

## Screen

window.screen 对象包含有关用户屏幕的信息。

window.screen 对象在编写时可以不使用 window 这个前缀。

一些属性：

* screen.availWidth - 可用的屏幕宽度
* screen.availHeight - 可用的屏幕高度



### Window Screen 可用宽度

screen.availWidth 属性返回访问者屏幕的宽度，以像素计，减去界面特性，比如窗口任务栏。

```javascript

<script>

document.write("可用宽度：" + screen.availWidth);

</script>

```

## Location

window.location 对象用于获得当前页面的地址 (URL)，并把浏览器重定向到新的页面。

window.location 对象在编写时可不使用 window 这个前缀。

一些例子：

* location.hostname 返回 web 主机的域名
* location.pathname 返回当前页面的路径和文件名
* location.port 返回 web 主机的端口 （80 或 443）
* location.protocol 返回所使用的 web 协议（http:// 或 https://）

### Window Location Href

location.href 属性返回当前页面的 URL。

```javascript

<script>

document.write(location.href);

</script>

```

以上代码输出为：

```javascript

http://www.w3school.com.cn/js/js_window_location.asp

```

### Window Location Pathname

location.pathname 属性返回 URL 的路径名。

```javascript

<script>

document.write(location.pathname);

</script>

```

以上代码输出为：

```javascript

/js/js_window_location.asp

```

### Window Location Assign

location.assign() 方法加载新的文档。

```html

<html>
<head>
<script>
function newDoc()
  {
  window.location.assign("http://www.w3school.com.cn")
  }
</script>
</head>
<body>

<input type="button" value="加载新文档" onclick="newDoc()">

</body>
</html>

```

## History

window.history 对象包含浏览器的历史。

为了保护用户隐私，对 JavaScript 访问该对象的方法做出了限制。
一些方法：

* history.back() - 与在浏览器点击后退按钮相同
* history.forward() - 与在浏览器中点击按钮向前相同

## Navigator

window.navigator 对象包含有关访问者浏览器的信息。

```javascript

<div id="example"></div>

<script>

txt = "<p>Browser CodeName: " + navigator.appCodeName + "</p>";
txt+= "<p>Browser Name: " + navigator.appName + "</p>";
txt+= "<p>Browser Version: " + navigator.appVersion + "</p>";
txt+= "<p>Cookies Enabled: " + navigator.cookieEnabled + "</p>";
txt+= "<p>Platform: " + navigator.platform + "</p>";
txt+= "<p>User-agent header: " + navigator.userAgent + "</p>";
txt+= "<p>User-agent language: " + navigator.systemLanguage + "</p>";

document.getElementById("example").innerHTML=txt;

</script>

```

**警告**：来自 navigator 对象的信息具有误导性，不应该被用于检测浏览器版本，这是因为：

* navigator 数据可被浏览器使用者更改
* 浏览器无法报告晚于浏览器发布的新操作系统

### 浏览器检测

由于 navigator 可误导浏览器检测，使用对象检测可用来嗅探不同的浏览器。

由于不同的浏览器支持不同的对象，您可以使用对象来检测浏览器。例如，由于只有 Opera 支持属性 "window.opera"，您可以据此识别出 Opera。

例子：if (window.opera) {...some action...}


## PopupAlert

可以在 JavaScript 中创建三种消息框：警告框、确认框、提示框。

### 警告框

警告框经常用于确保用户可以得到某些信息。

当警告框出现后，用户需要点击确定按钮才能继续进行操作。

语法：

```javascript

alert("文本")

```

### 确认框

确认框用于使用户可以验证或者接受某些信息。

当确认框出现后，用户需要点击确定或者取消按钮才能继续进行操作。

如果用户点击确认，那么返回值为 true。如果用户点击取消，那么返回值为 false。

语法：

```javascript

confirm("文本")

```

### 提示框

提示框经常用于提示用户在进入页面前输入某个值。

当提示框出现后，用户需要输入某个值，然后点击确认或取消按钮才能继续操纵。

如果用户点击确认，那么返回值为输入的值。如果用户点击取消，那么返回值为 null。

语法：

```javascript

prompt("文本","默认值")

```

## Timing

通过使用 JavaScript，我们有能力做到在一个设定的时间间隔之后来执行代码，而不是在函数被调用后立即执行。我们称之为计时事件。

### JavaScript 计时事件

通过使用 JavaScript，我们有能力作到在一个设定的时间间隔之后来执行代码，而不是在函数被调用后立即执行。我们称之为计时事件。

在 JavaScritp 中使用计时事件是很容易的，两个关键方法是:

`setTimeout()` 未来的某时执行代码

`clearTimeout()` 取消setTimeout()


setTimeout()：

```javascript

var t=setTimeout("javascript语句",毫秒)

```

setTimeout() 方法会返回某个值。在上面的语句中，值被储存在名为 t 的变量中。假如你希望取消这个 setTimeout()，你可以使用这个变量名来指定它。

setTimeout() 的第一个参数是含有 JavaScript 语句的字符串。这个语句可能诸如 "alert('5 seconds!')"，或者对函数的调用，诸如 alertMsg()"。

第二个参数指示从当前起多少毫秒后执行第一个参数。

**提示**：1000 毫秒等于一秒。

### 实例

当下面这个例子中的按钮被点击时，一个提示框会在5秒中后弹出。

```html

<html>
<head>
<script type="text/javascript">
function timedMsg()
 {
 var t=setTimeout("alert('5 seconds!')",5000)
 }
</script>
</head>

<body>
<form>
<input type="button" value="Display timed alertbox!" onClick="timedMsg()">
</form>
</body>
</html>

```

### 无穷循环



要创建一个运行于无穷循环中的计时器，我们需要编写一个函数来调用其自身。在下面的例子中，当按钮被点击后，输入域便从 0 开始计数。

```html

<html>

<head>
<script type="text/javascript">
var c=0
var t
function timedCount()
 {
 document.getElementById('txt').value=c
 c=c+1
 t=setTimeout("timedCount()",1000)
 }
</script>
</head>

<body>
<form>
<input type="button" value="Start count!" onClick="timedCount()">
<input type="text" id="txt">
</form>
</body>

</html>

```

### setInterval

The setInterval() method repeats a given function at every given time-interval.

```javascript

window.setInterval(function, milliseconds);

```

Stop the Execution

```javascript

window.clearInterval(timerVariable)

```


## Cookies

Cookies let you store user information in web pages.

Cookies are data, stored in small text files, on your computer.

When a web server has sent a web page to a browser, the connection is shut down, and the server forgets everything about the user.

Cookies were invented to solve the problem "how to remember information about the user":

* When a user visits a web page, his name can be stored in a cookie.
* Next time the user visits the page, the cookie "remembers" his name.

Cookies are saved in name-value pairs like:

```javascript

username=John Doe

```

When a browser request a web page from a server, cookies belonging to the page is added to the request. This way the server gets the necessary data to "remember" information about users.

### Create a Cookie with JavaScript

JavaScript can create, read, and delete cookies with the document.cookie property.

With JavaScript, a cookie can be created like this:

```javascript

document.cookie="username=John Doe";

```

You can also add an expiry date (in UTC time). By default, the cookie is deleted when the browser is closed:

```javascript

document.cookie="username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC";

```

With a path parameter, you can tell the browser what path the cookie belongs to. By default, the cookie belongs to the current page.

```javascript

document.cookie="username=John Doe; expires=Thu, 18 Dec 2013 12:00:00 UTC; path=/";

```

### Read a Cookie with JavaScript

With JavaScript, cookies can be read like this:

```javascript

var x = document.cookie;

```

> document.cookie will return all cookies in one string much like: cookie1=value; cookie2=value; cookie3=value;

###  Change a Cookie with JavaScript

Deleting a cookie is very simple. Just set the expires parameter to a passed date:

```javascript

document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC";

```

Note that you don't have to specify a cookie value when you delete a cookie.

### The Cookie String

The document.cookie property looks like a normal text string. But it is not.

Even if you write a whole cookie string to document.cookie, when you read it out again, you can only see the name-value pair of it.

If you set a new cookie, older cookies are not overwritten. The new cookie is added to document.cookie, so if you read document.cookie again you will get something like:

cookie1=value; cookie2=value;

### JavaScript Cookie Example

#### A Function to Set a Cookie

First, we create a function that stores the name of the visitor in a cookie variable:

```javascript

function setCookie(cname, cvalue, exdays) {
    var d = new Date();
    d.setTime(d.getTime() + (exdays*24*60*60*1000));
    var expires = "expires="+d.toUTCString();
    document.cookie = cname + "=" + cvalue + "; " + expires;
}

```

#### A Function to Get a Cookie

Then, we create a function that returns the value of a specified cookie:

```javascript

function getCookie(cname) {
    var name = cname + "=";
    var ca = document.cookie.split(';');
    for(var i=0; i<ca.length; i++) {
        var c = ca[i];
        while (c.charAt(0)==' ') c = c.substring(1);
        if (c.indexOf(name) == 0) return c.substring(name.length,c.length);
    }
    return "";
}

```

#### A Function to Check a Cookie

```javascript

function checkCookie() {
    var username=getCookie("username");
    if (username!="") {
        alert("Welcome again " + username);
    }else{
        username = prompt("Please enter your name:", "");
        if (username != "" && username != null) {
            setCookie("username", username, 365);
        }
    }
}

```