---
title: javaScript对象
categories: JavaScript
keywords: 对象
tags:
  - JavaScript
abbrlink: e66813
date: 2020-10-19 13:11:23
---
## 创建对象

### 对象字面量
<!--more-->
> 字面量：11 “abc”  true  [] {}等

```javascript
var o = {};
var o = {
  name : "zs",
  age : 18,
  sex : true,
  sayHi : function() {
    console.log(this.name);
  }
};
```

### 通过Object构造函数创建

```javascript
var hero = new Object();//创建一个空的对象
```

### 设置对象的属性

```
//语法  对象名.属性 = 值;
var obj = new Object();
obj.name = "zs";
obj.age = 18;
obj.gender = "男";

//给对象设置添加一个方法
obj.sayHi = function() {
  console.log("大家好，我是"+obj.name);
}
```

### 获取对象的属性

```javascript
//语法：  对象名.属性
console.log(obj.name);
console.log(obj.age);
console.log(obj.gender);

//如果是方法，可以调用
obj.sayHi();
```

## 批量创建对象

> 在实际开发中，经常需要创建多个相同类型的对象，比如游戏中的怪物，班级的学生等。

### 使用工厂函数创建对象

优点：可以同时创建多个对象

缺点：创建出来的没有具体的类型，都是object类型的

### 构造函数

> 构造函数 ，是一种特殊的函数。主要用来在创建对象时初始化对象， 即为对象成员变量赋初始值，总与new运算符一起使用在创建对象的语句中。

1. 构造函数首字母要大写（推荐做法）。
2. 构造函数要和new一起使用才有意义。
3. 构造函数的作用是用于实例化一个对象，即给对象添加属性和方法。

new在执行时会做四件事情

```javascript
new会做4件事情
1. new会创建一个新的空对象，类型是Teacher
2. new 会让this指向这个新的对象
3. 执行构造函数  目的：给这个新对象加属性和方法
4. new会返回这个新对象
```

总结：创建对象的几种方式

```javascript
1. new Object()
2. 对象字面量
3. 工厂函数
4. 自定义构造函数
```

### 查看一个对象的类型

```javascript
typeof 只能判断基本数据类型的类型
instanceof 判断对象的具体类型
constructor.name也可以获取到对象的具体类型
```

关于typeof

- typeof用于查看基本的数据类型， number string boolean undefined
- typeof如果查看复杂数据类型，返回的都是object类型。
- typeof null比较特殊，结果是object
- typeof 函数的结果是function:因为函数是一等公民

## 操作对象的属性

### .语法

```javascript
// 获取对象属性的语法：
	// 对象.属性：对象的属性
    // 1. 如果有这个属性，直接返回属性值
    // 2. 如果没有这个属性，返回undefined
// 设置对象的属性的语法
    // 对象.属性 = 值
    // 1. 如果对象有这个属性，修改这个属性
    // 2. 如果对象没有这个属性，添加这个属性
```

### []语法

也叫关联数组的方式，其实说白了就是把对象当成数组看待。在中括号中可以是一个变量或者是字符串。

```javascript
//获取对象属性
	// 对象['下标']   ：把对象的属性当成下标
//设置对象的属性
	// 对象['下标'] = "值";
```

二者的区别：当属性名是一个字符串存储在变量中的时候，只能使用关联数组的方式。

## 遍历对象

> 通过for..in语法可以遍历一个对象

```
var obj = {};
for (var i = 0; i < 10; i++) {
	obj[i] = i * 2;
}
for(var key in obj) {
	console.log(key + "==" + obj[key]);
}
```

## 删除对象属性

> delete关键字可以删除对象的属性

```
var obj = {name:"zs", age:18}
delete obj.name;//删除obj的name属性
```
