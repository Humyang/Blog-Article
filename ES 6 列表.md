最近在看 ES 6 的教程，内容很多，其中大部分是平常用不到的，在这里记录学到的知识点

# Class

类其实就是一个 function。

```javascript
class Point{
  // ...
}

typeof Point // "function"
Point === Point.prototype.constructor // true
```

在类的实例中调用方法，等于调用原型上的方法。
```javascript
class B {}
let b = new B();

b.constructor === B.prototype.constructor // true
```

类内部定义的方法是不可以枚举的。

由于类的方法是定义在 prototype 上面的，所以类的新方法可以添加到 prototype 上，Object.assign 可以很方便的一次性向 class 添加多个方法。

```javascript
class Point {
  constructor(){
    // ...
  }
}

Object.assign(Point.prototype, {
  toString(){},
  toValue(){}
})
```

prototype 对象的 constructor 属性直接指向 class 本身。

```javascript
Point.prototype.constructor === Point // true
```

类的属性名，可以采用表达式

```javascript
let methodName = "getArea";
class Square{
  constructor(length) {
    // ...
  }

  [methodName]() {
    // ...
  }
}
```

constructor 是类的默认方法，通过 new 命令生成对象时默认调用该方法。一个类必须有 constructor 方法，如果没有会默认添加一个空的 constructor 方法。

constructor 方法默认返回实例对象 (this)。完全可以指定返回另一个对象。

生成 class 对象一定要使用 new 关键字。

类的属性除非显式的定义在自身 (this)，否则都是定义在 prototype 上。

```javascript
//定义类
class Point {

  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '('+this.x+', '+this.y+')';
  }

}

var point = new Point(2, 3);

point.toString() // (2, 3)

point.hasOwnProperty('x') // true
point.hasOwnProperty('y') // true
point.hasOwnProperty('toString') // false
point.__proto__.hasOwnProperty('toString') // true
```

与 ES 5 一样，类的所有实例共享一个原型对象。
