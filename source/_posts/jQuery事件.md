---
title: jQuery事件
toc: true
comments: true
tags:
  - JavaScript
  - jQuery
categories:
  - JavaScript
description:
  - jQuery对JavaScript事件进行了封装，增加并扩展了事件处理机制。
keywords:
  - jquery
  - bind
  - unbind
  - "on"
  - "off"
  - delegate
  - undelegate
abbrlink: f7b3a86d
date: 2020-11-19 16:33:28
updated: 2020-11-19 16:33:28
---

# jQuery 事件机制

> JavaScript 中已经学习过了事件，但是 jQuery 对 JavaScript 事件进行了封装，增加并扩展了事件处理机制。jQuery 不仅提供了更加优雅的事件处理语法，而且极大的增强了事件的处理能力。

<!-- more -->

## jQuery 事件发展历程(了解)

简单事件绑定>>bind 事件绑定>>delegate 事件绑定>>on 事件绑定(推荐)

> 简单事件注册

```javascript
click(handler)			单击事件
mouseenter(handler)		鼠标进入事件
mouseleave(handler)		鼠标离开事件
```

缺点：不能同时注册多个事件

> bind 方式注册事件

```javascript
//第一个参数：事件类型
//第二个参数：事件处理程序
$("p").bind("click mouseenter", function () {
  //事件响应方法
});
```

缺点：不支持动态事件绑定

> delegate 注册委托事件

```javascript
// 第一个参数：selector，要绑定事件的元素
// 第二个参数：事件类型
// 第三个参数：事件处理函数
$(".parentBox").delegate("p", "click", function () {
  //为 .parentBox下面的所有的p标签绑定事件
});
```

> on 注册事件

## on 注册事件(重点)

> jQuery1.7 之后，jQuery 用 on 统一了所有事件的处理方法。
>
> 最现代的方式，兼容 zepto(移动端类似 jQuery 的一个库)，强烈建议使用。

on 注册简单事件

```javascript
// 表示给$(selector)绑定事件，并且由自己触发，不支持动态绑定。
$(selector).on("click", function () {});
```

on 注册委托事件

```javascript
// 表示给$(selector)绑定代理事件，当必须是它的内部元素span才能触发这个事件，支持动态绑定
$(selector).on( "click",“span”, function() {});

```

on 注册事件的语法：

```javascript
// 第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件（标准事件或者自定义事件）
// 第二个参数：selector, 执行事件的后代元素（可选），如果没有后代元素，那么事件将有自己执行。
// 第三个参数：data，传递给处理函数的数据，事件触发的时候通过event.data来使用（不常使用）
// 第四个参数：handler，事件处理函数
$(selector).on(events, [selector], [data], handler);
```

## 事件解绑

> unbind 方式（不用）

```javascript
$(selector).unbind(); //解绑所有的事件
$(selector).unbind("click"); //解绑指定的事件
```

> undelegate 方式（不用）

```javascript
$( selector ).undelegate(); //解绑所有的delegate事件
$( selector).undelegate( “click” ); //解绑所有的click事件
```

> off 方式（推荐）

```javascript
// 解绑匹配元素的所有事件
$(selector).off();
// 解绑匹配元素的所有click事件
$(selector).off("click");
```

## 触发事件

```javascript
$(selector).click(); //触发 click事件
$(selector).trigger("click");
```

## jQuery 事件对象

jQuery 事件对象其实就是 js 事件对象的一个封装，处理了兼容性。

```javascript
//screenX和screenY	对应屏幕最左上角的值
//clientX和clientY	距离页面左上角的位置（忽视滚动条）
//pageX和pageY	距离页面最顶部的左上角的位置（会计算滚动条的距离）

//event.keyCode	按下的键盘代码
//event.data	存储绑定事件时传递的附加数据

//event.stopPropagation()	阻止事件冒泡行为
//event.preventDefault()	阻止浏览器默认行为
//return false:既能阻止事件冒泡，又能阻止浏览器默认行为。
```
