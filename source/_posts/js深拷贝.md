---
title: js深拷贝与浅拷贝
toc: true
comments: true
tags:
  - JavaScript
categories:
  - JavaScript
description:
  - 把数组以及对象的各种拷贝方法整合起来
keywords:
  - 深拷贝
  - assign
  - create
  - splice
abbrlink: 2836dd7e
date: 2021-05-13 21:34:58
updated: 2021-05-13 21:34:58
---

# 对象的深拷贝和浅拷贝

<!-- more -->

## 递归的方式实现深拷贝

```js
function deepClone(target) {
  //定义一个返回变量
  let res;
  //如果target是对象如null，array等
  if (typeof target === "object") {
    if (Array.isArray(target)) {
      //target为数组
      res = [];
      for (let i in target) {
        res.push(deepClone(target[i]));
      }
    } else if (target === null) {
      //target为null
      res = null;
    } else if (target.constructor === RegExp) {
      //target为正则对象
      res = target;
    } else {
      // target为普通对象
      res = {};
      for (let item in target) {
        res[item] = deepClone(target[item]);
      }
    }
    //target为基本数据类型，直接赋值
  } else {
    res = target;
  }
  //返回结果
  return res;
}
```

测试一下

```js
var testObj = {
  arr: [{ a: 1 }, null, 3],
  obj: {
    name: "zlh",
    age: 100,
  },
  fn: function () {
    console.log("hello");
  },
  reg: /a(b)/,
};

let cloneObj = deepClone(testObj);
testObj.arr = [];
testObj.obj.name = "fcj";
console.log(testObj.arr); //[]
console.log(cloneObj.arr); //[{ a: 1 }, null, 3]
console.log(testObj.obj.name); //fcj
console.log(cloneObj.obj.name); //zlh
```

这样就简单的实现了一个深拷贝，可以进行多级的深拷贝，而且 function，unll 等特殊的值也能全部拷贝成功，修改里边的值也不会有任何问题

## 利用 JSON.stringify()以及 JSON.parse()

> 使用 JSON.stringify()以及 JSON.parse()还是挺简单的，但不可以拷贝 undefined ， function， RegExp 等类型

```js
function clone(target) {
  return JSON.parse(JSON.stringify(target));
}
/*********测试************/
let obj = {
  a: 1,
  b: { a: 1 },
  c: function () {},
};
let cloneObj = clone(obj);
console.log(cloneObj.c); //undefined
```

## Object.assign(target, source)

> 语法: `Object.assign(target, ...sources)` target: 目标对象,sources: 源对象
> 用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

> 当对象中只有一级属性，没有二级属性的时候，此方法为深拷贝，但是对象中有对象的时候，此方法，在二级属性以后就是浅拷贝。

```js
let obj = {
  a: 1,
  b: ["111"],
  c: { name: "zlh" },
};

let obj2 = Object.assign({}, obj);
console.log(obj2.b[0]); //111
console.log(obj2.c.name); //zlh
obj.b[0] = "222";
obj.c.name = "fcj";
console.log(obj2.b[0]); //222
console.log(obj2.c.name); ///fcj
```

## 拓展运算符语法

> 在 ES6 中新增了扩展运算符可以对数组和对象进行操作。但是扩展运算符为浅拷贝

```js
let obj = {
  a: 1,
  b: ["111"],
  c: { name: "zlh" },
};

let obj2 = { ...obj };
console.log(obj2.b[0]); //111
console.log(obj2.c.name); //zlh
obj.b[0] = "222";
obj.c.name = "fcj";
console.log(obj2.b[0]); //222
console.log(obj2.c.name); ///fcj
```

## lodash 函数库实现深拷贝

```js
import _ from "lodash";
var obj = { id: 1, name: { a: "xx" }, fn: function () {} };
var obj2 = _.cloneDeep(obj);
obj2.name.a = "obj2";
console.log(obj.name.a, obj2.name.a); //xx,obj2
```

## Object.create()

> 感觉把这个方法说成是拷贝有点牵强，但还是记录一下

> Object.create()方法创建一个新的空对象，使用现有的对象来提供新创建的对象的`__proto__`。

```js
let obj = {
  a: 1,
  b: ["111"],
  c: { name: "zlh" },
};

let obj2 = Object.create(obj);
console.log(obj2); // {}
//通过原型链访问
console.log(obj2.__proto__ === obj); //true
console.log(obj2.b[0]); //111
console.log(obj2.c.name); //zlh
```

# 数组的一些拷贝方法

## ES6 的 Array.from()

> Array.from()方法就是将一个类数组对象或者可遍历对象转换成一个真正的数组。所谓类数组对象，最基本的要求就是具有 length 属性的对象。

```js
let arr = [1, 2, 3, 4];
let arr2 = Array.from(arr);
console.log(arr2); //[1,2,3,4]
console.log(arr == arr2); //false
```

当然这只是最简单的用法，其实还可以用`Array.from()`做很多事情:

1. 将字符串转换为数组：

```js
let str = "hello world!";
console.log(Array.from(str)); // ["h", "e", "l", "l", "o", " ", "w", "o", "r", "l", "d", "!"]
```

2. 将类数组对象转换为真正数组：

```js
/*
1.该类数组对象必须具有length属性，用于指定数组的长度。如果没有length属性，那么转换后的数组是一个空数组。

2.该类数组对象的属性名必须为数值型或字符串型的数字

3.该类数组对象的属性名可以加引号，也可以不加引号*/
let arrayLike = {
  0: "fcj",
  1: "21",
  2: "男",
  3: ["jane", "john", "Mary"],
  length: 4,
};
let arr = Array.from(arrayLike);
console.log(arr); // ['fcj','21','男',['jane','john','Mary']]
```

## ES6 的扩展运算符(...)

> 这个上面拷贝对象时已经介绍了，使用比较简单

```js
var arr = [1, 2, 3];
var arr2 = [...arr];
```

## slice()方法

> array 对象的 slice 函数，返回一个数组的一段。（仍为数组）
> `arrayObj.slice(start, [end])`

```js
var arr = [1, 2, 3];
var arr2 = arr.slice(0);
console.log(arr2); //[1,2,3]
```

## concat()方法

> concat() 方法用于连接两个或多个数组。该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。
> `arrayObject.concat(arrayX,arrayX,......,arrayX)`

```js
var arr = [1, 2, 3];
var arr2 = arr.concat();
console.log(arr2); //[1,2,3]
```

## 注意

> 上述拷贝数组方法其实都是浅拷贝
