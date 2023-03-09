---
title: jQuery特殊属性
toc: true
comments: true
tags:
  - JavaScript
  - jQuery
categories:
  - JavaScript
keywords:
  - jquery
  - val
  - html
  - text
  - width
abbrlink: cd22a746
date: 2020-11-19 14:25:33
updated: 2020-11-19 14:25:33
---

# jQuery 特殊属性操作

## val 方法

<!-- more -->

> val 方法用于设置和获取表单元素的值，例如 input、textarea 的值

```javascript
val方法的用法
val()  没有传参数，表示获取value值
val(value) 传递了参数，表示设置value值
```

## html 方法与 text 方法

> html 方法相当于 innerHTML text 方法相当于 innerText

```javascript
//设置内容
$(“div”).html(“<span>这是一段内容</span>”);
//获取内容
$(“div”).html()

//设置内容
$(“div”).text(“<span>这是一段内容</span>”);
//获取内容
$(“div”).text()
```

区别：html 方法会识别 html 标签，text 方法会那内容直接当成字符串，并不会识别 html 标签。

## width 方法与 height 方法

> 设置或者获取高度

```javascript
//带参数表示设置高度
$(“img”).height(200);
//不带参数获取高度
$(“img”).height();

innerWidth()  innerHeight()   //获取盒子的宽度 + padding值
outerWidth(false)  outerHeight(false)    //默认false  宽度 + padding + border
outerWidth(true)   outerHeight(true) //宽度 + padding + border + margin

```

获取网页的可视区宽高

```javascript
//获取可视区宽度
$(window).width();
//获取可视区高度
$(window).height();
```

## scrollTop 与 scrollLeft

在 js 中操作滚动条卷去的距离

```
获取： html和body的scrollTop  document.documentElement.scrollTop
现在的浏览器推荐： window.pageYOffset  pageYOffset是只读的属性
设置scrollTop:    修改document.documentElement.scrollTop = 0
window.scrollTo({top: 0})
```

> 设置或者获取垂直滚动条的位置

```javascript
//获取页面被卷曲的高度
$(window).scrollTop();
//获取页面被卷曲的宽度
$(window).scrollLeft();
```

## offset 方法与 position 方法

> offset 方法获取元素距离 document 的位置，position 方法获取的是元素距离有定位的父元素的位置。

```javascript
//获取元素距离document的位置,返回值为对象：{left:100, top:100}
$(selector).offset();
//获取相对于其最近的有定位的父元素的位置。
$(selector).position();
```
