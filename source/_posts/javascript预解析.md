---
title: javascript预解析
summary: javascript预解析
categories: JavaScript
keywords: JavaScript 预解析
tags:
  - JavaScript
abbrlink: ce274c7b
date: 2020-09-28 10:35:19
---
# 预解析
## 预解析的相关概念
JavaScript 代码是由浏览器中的 JavaScript 解析器来执行的。JavaScript 解析器在运行 JavaScript 代码的时候分为两步：预解析和代码执行。
<!--more-->
预解析：在当前作用域下, JS 代码执行之前，浏览器会默认把带有 var 和 function 声明的变量在内存中进行提前声明或者定义。

代码执行： 从上到下执行JS语句。

**预解析会把变量和函数的声明在代码执行之前执行完成。**
## 变量预解析
预解析也叫做变量、函数提升。

变量提升（变量预解析）： 变量的声明会被提升到当前作用域的最上面，变量的赋值不会提升。
```js
console.log(num);  // 结果是多少？
var num = 10;      // ？
```
结果：undefined
	
注意：**变量提升只提升声明，不提升赋值**
## 函数预解析
函数提升： 函数的声明会被提升到当前作用域的最上面，但是不会调用函数。
```
fn();
function fn() {
    console.log('打印');
}
```
结果：控制台打印字符串 --- ”打印“ 
	
注意：函数声明代表函数整体，所以函数提升后，函数名代表整个函数，但是函数并没有被调用！	
## 函数表达式声明函数问题
函数表达式创建函数，会执行变量提升，此时接收函数的变量名无法正确的调用：
```
fn();
var  fn = function() {
    console.log('想不到吧');
}
```
结果：报错提示 ”fn is not a function"
	
解释：该段代码执行之前，会做变量声明提升，fn在提升之后的值是undefined；而fn调用是在fn被赋值为函数体之前，此时fn的值是undefined，所以无法正确调用
## 注意：
预解析的注意点:

(1) 将所有的 var 声明提升, 提升到当前作用域的最前面, 只提升声明, 不提升赋值
    如果有同名 var 声明, 后面的会被忽略

(2) 将所有的 function 声明提升, 提升到当前作用域的最前面, 只提升声明, 不提升调用
    如果有同名的 function 函数声明, 后面会将前面的覆盖

(3) 如果和 函数名 和 var 同名, 函数优先

## 预解析案例
### 案例1
```
var num = 10;
fun();

function fun() {
    console.log(num);
    var num = 20;
}
```
相当于以下代码
```
var num; //变量提升

function fun() {   //函数提升 函数里边也是一个作用域，也有变量提升
     var num;   //变量提升 
     console.log(num); //undefined
     num = 20;
 }
-----------------上面是预解析
num = 10;
fun();

```

结果undefined,因为调用函数时，函数内部num提升到console.log(num)之前，还没有被赋值，根据作用域链，谁离的近调用谁，所以输出undefined
### 案例2
```
var num = 10;

function fn() {
    console.log(num);
    var num = 20;
    console.log(num);
}
fn();
```
相当于以下代码
```
var num;  //变量提升

function fn() {    //函数提升
    var num;     //变量提升 
    console.log(num); //undefined
    num = 20;
    console.log(num); //20
}
-----------------上面是预解析
num = 10;
fn();

```
结果 undefined 20
### 案例3
```
var a = 18;
f1();

function f1() {
    var b = 9;
    console.log(a);
    console.log(b);
    var a = '123';
}
```
相当于以下代码
```
var a;    //变量提升
function f1() {   //函数提升
    var b;   //变量提升 
    var a;   //变量提升 
    b = 9;
    console.log(a); //undefined
    console.log(b); //9
    a = '123';
}

a = 18;
f1();
```
结果 undefined 9
### 案例4
```
f1();
console.log(c);
console.log(b);
console.log(a);

function f1() {
    var a = b = c = 9;
    console.log(a);
    console.log(b);
    console.log(c);
}
```
相当于以下代码
```
function f1() {  //函数提升
    var a;       //变量提升 
    a = b = c = 9;
    // 相当于 var  a  = 9; b = 9; c = 9; b 和 c 直接赋值 没有var 声明 当 全局变量看
    // 集体声明  var a = 9, b = 9, c = 9;  a,b,c均有var声明
    console.log(a); //9
    console.log(b); //9
    console.log(c); //9
}
f1();
console.log(c); //9
console.log(b); //9
console.log(a); //a is not defined

```
结果 9，9，9，9，9，a is not defined

黑马pink老师的笔记