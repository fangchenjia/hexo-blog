---
title: "手写call,apply,bind"
toc: true
comments: true
tags:
  - JavaScript
categories:
  - JavaScript
description:
  - 参考了一些网上的文章，然后根据自己的理解自己实现的call，apply，bind，虽然不是特别完善，但还是选择记录下来，也是一个成长的过程
keywords:
  - call
  - apply
  - bind
  - 手写
abbrlink: "84198221"
date: 2021-05-13 19:32:13
updated: 2021-05-13 19:32:13
---

# call 与 apply 与 bind 异同

1. 作用：均为改变 this 指向
2. call/bind 传参为多个参数，apply 传参为一个参数数组
3. bind 的时候 function 函数不执行，需手动执行，call/apply 的时候函数自动执行
<!-- more -->

# 手写 call

```js
Function.prototype.myCall = function (obj, ...arr) {
  // 基本原理就是用传进来的对象obj来调用 调用call的函数
  let context = obj || globalThis;
  //谁调用Call this指向谁，而Call在Function的原型上,所以如调用obj.fn.myCall()时此函数this指向obj.fn
  context.func = this;
  let res = context.func(...arr);
  delete context.func;
  return res;
};

this.a = "window";
var obj = {
  a: "obj",
  fn: function () {
    console.log(this.a);
  },
};
let fn = obj.fn;
fn(); //window
fn.myCall(obj); //obj
obj.fn(); //obj
```

# 手写 apply

> 和 call 基本类似

```js
Function.prototype.myApply = function (obj, arr) {
  let context = obj || globalThis;
  context.func = this;
  let res = context.func(...arr);
  delete context.func;
  return res;
};
```

# 手写 bind

> bind 的第一个参数会作为原函数运行时的 this 指向，而第二个开始的参数是可选的，当绑定函数被调用时，这些参数加上绑定函数本身的参数会按照顺序作为原函数运行时的参数。当使用 new 操作符调用绑定函数时，bind 的第一个参数无效

```js
Function.prototype.myBind = function (obj, ...arr) {
  let context = obj || globalThis;
  let self = this;
  //返回一个新的方法
  let res = function (...arr2) {
    //判断是否是new
    if (this instanceof res) return self.call(this, ...arr, ...arr2);
    else return self.call(context, ...arr, ...arr2);
  };
  //绑定原型链
  res.prototype = Object.create(self.prototype);
  return res;
};
window.a = "window";
var obj = {
  a: "obj",
  fn: function () {
    console.log(this.a);
  },
};
let fn = obj.fn;
let fn2 = obj.fn.myBind(obj);
fn(); //window
fn2(); //obj

//当使用 new 操作符调用绑定函数时，bind 的第一个参数无效
var person = function (name) {
  this.name = name;
};
let p1 = person.myBind(obj);
let p = new p1("zlh");
console.log(p); //{name: "zlh"}

var add = function (a = 0, b = 0, c = 0) {
  return a + b + c;
};
let add2 = add.myBind(null, 2); //返回的函数第一个参数已经被2“内定”了
console.log(add(), add2()); //0,2
console.log(add(1, 1, 1), add2(1, 1, 1)); //3,4
```
