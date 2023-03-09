---
title: es5核心知识点笔记
toc: true
comments: true
tags:
  - JavaScript
categories:
  - JavaScript
description:
  - js的一些必备知识点，面试题
abbrlink: a32b3768
date: 2021-05-06 18:20:26
updated: 2021-05-06 18:20:26
---

# 变量提升以及函数提升

<!-- more -->

> 变量是会变量提升的，看现象

```js
if (false) {
  var a = 3;
}
console.log(a); //undefined
/**********相当于***********/
var a;
if (false) {
  a = 3;
}
console.log(a); //undefined
```

> 函数也存在函数提升

```js
console.log(test); //ƒ test(){ console.log(1); }
test(); //打印1
function test() {
  console.log(1);
}
```

> 函数提升要注意的地方

```js
(function () {
  console.log(test); //undefined
  if (false) {
    function test() {
      console.log(1);
    }
  }
  test(); //Uncaught TypeError: test is not a function
})();

(function () {
  console.log(test); //undefined
  {
    function test() {
      console.log(1);
    }
  }
  test(); //打印 1
})();
```

> 如果函数和变量同名时，函数提升优先于变量，但有一个关键的点要注意，`变量有没有被赋值`

1. 首先看一道题

```js
console.log(a); //ƒ a(){ console.log(10);}
a(); //执行函数a 打印10
var a = 3;
function a() {
  console.log(10);
}
console.log(a); //打印3
a = 6;
a(); //Uncaught TypeError: a is not a function
```

2. 变量没有被赋值的情况

```js
console.log(a); //ƒ a(){ console.log(10);}
a(); //执行函数a 打印10
var a;
function a() {
  console.log(10);
}
console.log(a); //ƒ a(){ console.log(10);}
```

3. 变量被赋值的情况

```js
console.log(a); //ƒ a(){ console.log(10);}
a(); //执行函数a 打印10
var a = 3;
function a() {
  console.log(10);
}
console.log(a); //打印3
/**********相当于***********/
function a() {
  console.log(10);
}
var a;
console.log(a); //函数提升优先变量提升所以打印 ƒ a(){ console.log(10);}
a(); //执行函数a 打印10
a = 3;
console.log(a); //打印3
```

> 扩展：匿名函数或者被赋值的命名函数内部不能修改函数名，修改函数名也会当作无效处理，而普通函数可以在函数体内修改函数名

```js
var a = function test() {
  //这是一个表达式，因为test是赋值表达式的一部分，在外部是访问不到test的，只能在函数内部访问
  console.log(typeof test); //function
};
a(); //执行函数打印 function
console.log(test); //Uncaught ReferenceError: test is not defined
```

1. 匿名函数或者被赋值的命名函数内部修改函数名

```js
(function test() {
  test = 22; //修改无效
  console.log(typeof test); //function
})();

var a = function test() {
  test = 22; //修改无效
  console.log(typeof test); //function
};
a(); //执行函数打印 function
console.log(test); //Uncaught ReferenceError: test is not defined
```

2. 普通函数内修改函数名

```js
function test() {
  test = 22;
  console.log(typeof test); //number
}
test(); //执行函数打印 number
console.log(test); //打印22
```

# js 中的分号`;`以及换行要注意的问题

> JS 中，如若语句各占独立一行，通常可以省略语句间的分号（;），JS 解析器会根据能否正常编译来决定是否自动填充分号：

```js
//在下面情况下，为了正确解析代码，就不会自动填充分号了，
var test = 1 + 2;
console.log(test); //3
```

> 对于 return 、break、continue 等语句，如果后面紧跟换行，解析器一定会自动在后面填充分号(;)

```js
function foo1() {
  //返回{ bar: "hello" };
  return {
    bar: "hello",
  };
}

function foo2() {
  //返回undefined
  return;
  {
    bar: "hello";
  }
}
//foo2相当于
function foo2() {
  return;
  {
    bar: "hello";
  }
}
```

> JavaScript 什么时候应该加分号

- `(`或者`[` 或者 `` ` `` 开头的，则最好都在其前面补上一个分号

```js
(function () {
  console.log("hello");
})();
["苹果", "香蕉"].forEach(function (item) {
  console.log(item);
});
`hello`.toString();
```

# this 的指向问题

> this 的指向是谁调用就指向谁，即调用之前，this 还不知其指向。

### 对象调用

> 对象调用的隐式绑定， this 指向就是这个调用的对象。

```js
var test = {
  a: 40,
  init: function () {
    console.log(this.a);
  },
};
test.init(); //40 此处是对象调用
```

### 直接调用

> 直接调用的默认绑定， this 指向一定是全局对象（浏览器的话是 window）。在严格模式下其值会是 undefined。

```js
this.a = 20;
var test = {
  a: 40,
  init: function () {
    console.log(this.a);
  },
};
test.init(); //40 此处是对象调用
var fn = test.init;
fn(); //20 直接调用
/***************改造一下*****************/
this.a = 20;
var test = {
  a: 40,
  init: function () {
    function go() {
      console.log(this.a);
    }
    go();
  },
};
test.init(); //20 此处go为直接调用
```

### 箭头函数的 this 指向

> 箭头函数的 this 是父执行上下文里面的 this。 父执行上下文可以理解为是指箭头函数的父级普通函数,由`定义该函数时`的`外层函数`确定。而且箭头函数的 this 一旦被绑定，就无法改变。

```js
var name = "window";
var A = {
  name: "A",
  sayHello: () => {
    console.log(this.name);
  },
};
A.sayHello(); //输出的是window
```

改造一下

```js
var name = "window";
var A = {
  name: "A",
  sayHello: function () {
    //定义箭头函数时外层函数是sayHello this绑定为A
    var s = () => console.log(this.name);
    return s; //返回箭头函数s
  },
};
var sayHello = A.sayHello();
sayHello(); // 输出A

var B = {
  name: "B",
};

sayHello.call(B); //还是A
sayHello.call(); //还是A
```

### new 方式的绑定规则

> this 指向这个构造出的新对象。

```js
this.a = 20;
var test = {
  a: 40,
  init: () => {
    console.log(this.a);
    function go() {
      console.log(this.a);
    }
    go.prototype.a = 50;
    return go;
  },
};
//test.init()是箭头函数，此处this指向window所以先打印20
//new(test.init())(); new go的时候this指向新new的对象，但此时新new的对象中并没有a,所以沿着原型链向上找，所以再打印50
new (test.init())(); //先打印 20 再打印50

/*************改造一下***************/
this.a = 20;
var test = {
  a: 40,
  init: () => {
    console.log(this.a);
    function go() {
      this.a = 60;
      console.log(this.a);
    }
    go.prototype.a = 50;
    return go;
  },
};
new (test.init())(); //先打印20 再打印60
```

#### 补充

> ES6-对象的函数属性简写不支持 new

```js
var test = {
  a: function () {
    console.log("a");
  },
  // 简写版：
  b() {
    console.log("b");
  },
};
new test.a(); //打印 a
new test.b(); //Uncaught TypeError: test.b is not a constructor
```

改造一下

```js
this.num = 11;
var test = {
  a: function () {
    console.log(this.num + 1);
  },
};
var fn = test.a.bind(this);
fn(); //打印 12
new fn(); //打印 NAN (undefined+11)
```

### 加深理解的题

```js
function C1(name) {
  //即使没有传参函数内部也能直接找到name不过没传参电话name为undefined
  if (name) this.name = name;
}
function C2(name) {
  this.name = name;
}
function C3(name) {
  this.name = name || "33";
}
C1.prototype.name = "C1";
C2.prototype.name = "C2";
C3.prototype.name = "C3";
console.log(new C1().name + new C2().name + new C3().name); //C1undefined33
```

### 总结

![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/es5%E6%A0%B8%E5%BF%83%E7%9F%A5%E8%AF%86%E7%82%B9/this%E6%8C%87%E5%90%91.png)

---

# JS 中的 {} + [] 和 [] + {}

> 首先看浏览器调试 Console 中的现象

- []+{}    结果是  "[object Object]"

- {}+[]    结果是 0

- ({}+[])    结果是  "[object Object]"

- +[]      结果是 0   ，此处+为正号

- +{}      结果是  NaN   ，此处+为正号

- [].toString()     结果是  ""

- ({}).toString()  结果是  "[object Object]"

- {}.toString()  会出错，Uncaught SyntaxError: Unexpected token .

- 0+[]     结果是  "0"

- 0+{}     结果是  "0[object Object]"

因为 js 的弱类型，导致 js 的隐式类型转换频繁。比如像标题中的{} + []，[] + {}，我们完全不能去预测它的类型。

先来看一条在 js 里的隐式的 rule，js 在进行加法运算的时候， 会先推测两个操作数是不是 number。
如果是，则直接相加得出结果。
如果其中有一个操作数为 string，则将另一个操作数隐式的转换为 string，然后进行字符串拼接得出结果。
如果操作数为对象或者是数组这种复杂的数据类型，那么就将两个操作数都转换为字符串，进行拼接
如果操作数是像 boolean 这种的简单数据类型，那么就将操作数转换为 number 相加得出结果
知道了这些规则的话就简单多了

> []+{},按照上面的 rule，先将两个操作数转换为 string，然后进行拼接，于是

```
[] ---------------------> ''
{} ---------------------> '[object Object]'
[] + {} = '[object Object]'
```

> {}+[],这也是两个复杂数据结构相加的例子，看样子与第一个没有什么差别，按理说也应该是[object Object]，但是你相加的时候你会发现， 得出的答案是 0！
> 原因是有的 js 解释器会将开头的 {} 看作一个代码块，而不是一个 js 对象，于是真正参与运算的是+[]，就是将[]转换为 number，于是得出答案 0

```js
{} + [] 相当于
{ /*empty block*/ }
+[]

{console.log("hello")} + []
//hello
//0
```

> ({}+[]), 因为参数列表只接受 expression,所以{}会转换为'[object Object]'

```
({}+[]) -------------------> '[object Object]'+''
```

此处参考自https://blog.csdn.net/HaoDaWang/article/details/81319191
