---
title: BOM
categories: JavaScript
keywords: bom
tags:
  - JavaScript
abbrlink: f3d3ee5b
date: 2020-10-25 21:54:02
---
# BOM

> BOM（Browser Object Model）：浏览器对象模型，提供了一套操作浏览器功能的工具。
<!--more-->
## window对象

1. window对象是一个全局对象，也可以说是JavaScript中的顶级对象
2. 像document、alert()、console.log()这些都是window的属性，BOM中的属性和方法都是属性window的。
3. 所有定义在全局作用域中的变量、函数都是window对象的属性和方法
4. window对象下的属性和方法调用的时候可以省略window

### window.onload（掌握）

> window.onload事件会在窗体加载完成后执行，通常我们称之为入口函数。

```javascript
window.onload = function(){
	//里面的代码会在窗体加载完成后执行。
	//窗体加载完成包括文档树的加载、还有图片、文件的加载完成。
}
```

一个页面不能写两个window.onload

### window.open与window.close(了解)

> window.open() 打开一个窗口

```javascript
//语法：window.open(url, [name], [features]);
//参数1：需要载入的url地址
//参数2：新窗口的名称，可选
//参数3：窗口的属性，指定窗口的大小等信息，可选
//返回值：会返回刚刚创建的那个窗口，用于关闭
//示例：
var newWin = window.open("http://www.baidu.com","_blank", "width=300,height=300");

//参数配置：https://developer.mozilla.org/zh-CN/docs/Web/API/Window/open
```

> window.close 关闭窗口

```javascript
newWin.close()；//newWin是刚刚创建的那个窗口
window.close();//把当前窗口给关闭了
```

## 延时器与定时器

### setTimeout

> setTimeout延时器可以在延迟时间到期后执行一个指定的函数。

设置延时器

```javascript
//语法：setTimeOut(callback, time);
//参数1：回调函数，时间到了就会执行。
//参数2：延时的时间
//返回：定时器的id，用于清除
//示例：
var timer = setTimeOut(function(){
	//1秒后将执行的代码。
}, 1000);
```

清除延时器

```javascript
//语法：clearTimeOut(timerId)
//参数：定时器id
//示例：
clearTimeOut(timer);//清除上面定义的定时器
```

### setInterval

> setInterval,方法重复调用一个函数或执行一个代码段，在每次调用之间具有固定的时间延迟。定时器除非清除，否则会一直执行下去。

设置定时器

```
//语法：var intervalID = setInterval(func, delay);
//参数1：重复执行的函数
//参数2：每次延迟的毫秒数
//返回：定时器的id，用于清除
//示例：
var timer = setInterval(function(){
	//重复执行的代码。
}, 1000);
```

清除定时器

```javascript
//语法：clearInterval(intervalID)
//参数：定时器id
//示例：
clearInterval(timer);//清除上面定义的定时器
```


## location对象

> location对象也是window的一个属性，location其实对应的就是浏览器中的地址栏。

### 常用属性和方法

> location.href:控制地址栏中的地址

```javascript
location.href = “http://www.baidu.com”;//让页面跳转到百度首页
```

> location.reload()：让页面重新加载

```javascript
location.href = "";
history.go(0)
```

> location的其他属性

```javascript
console.log(window.location.hash);//哈希值 其实就是锚点   SPA（single page application）
console.log(window.location.host);//服务器 服务器名+端口号
console.log(window.location.hostname);//服务器名
console.log(window.location.pathname);//路径名
console.log(window.location.port);//端口
console.log(window.location.protocol);//协议
console.log(window.location.search);//参数
```


## 其他对象

> window.navigator的一些属性可以获取客户端的一些信息

```javascript
//navigator.userAgent：浏览器版本
```

> history对象表示页面的历史

```javascript
//后退：
history.back();
history.go(-1);
//前进：
history.forward();
history.go(1);
```

> screen对象

```javascript
console.log(screen.width);//屏幕的宽度 
console.log(screen.height);//屏幕的高度
console.log(screen.availWidth);//浏览器可占用的宽度
console.log(screen.availHeight);//浏览器可占用的高度
```


