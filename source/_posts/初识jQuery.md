---
title: 初识jQuery
toc: true
comments: true
tags:
  - JavaScript
  - jQuery
categories:
  - JavaScript
description:
  - jQuery的基本概念及选择器
keywords:
  - javascript
  - jquery
  - 选择器
  - 基本概念
abbrlink: c1e02dc1
date: 2020-11-12 22:51:38
updated: 2020-11-12 22:51:38
---

# jQuery 基本介绍

使用原生 js 操作 DOM 的时候，会遇到以下的一些缺点：

<!-- more -->

```javascript
//1. 获取元素的方法太少且长，麻烦。
//2. 遍历很麻烦，通常要嵌套一大堆的for循环。
//3. 注册的事件会覆盖。
//4. 有兼容性问题。
//5. 实现动画很麻烦
```

使用 jQuery 的优点

```javascript
//1. jQuery对获取元素的方法进行了封装，使用非常简洁
//2. jQuery的隐式迭代特性，不再需要书写for循环语句。
//3. 使用jQuery完全不用考虑兼容性问题。
//4. jQuery封装了一系列动画相关的函数，使用非常简单。
```

## 什么是 jQuery?

> jQuery 是一个快速的、轻量的、功能丰富的 js 库。

jQuery 的官网 [http://jquery.com/](http://jquery.com/)

jQuery 的实质： 一个封装了很多很多 DOM 操作的 js 文件，这个 js 文件中提供了非常多的方法供我们使用。使用 jQuery 提供的这些方法，非常简洁，而且不用考虑浏览器的兼容性问题。

## 版本介绍

> 官网下载地址：[http://jquery.com/download/](http://jquery.com/download/)
>
> jQuery 版本有很多，分为 1.x 2.x 3.x

大版本分类：

```javascript
1.x版本：能够兼容IE678浏览器（最终版本1.12.4）
2.x版本：不兼容IE678浏览器（最终版本2.2.4）
//jQuery目前正在更新的版本
3.x版本：不兼容IE678，更加的精简（在国内不流行，因为国内使用jQuery的主要目的就是兼容IE678）,3.x版本只是在原来的基础上增加了一些新的特性。
```

关于压缩版和未压缩版

```javascript
jquery-1.12.4.min.js:压缩版本，适用于生产环境，因为文件比较小，去除了注释、换行、空格等东西，但是基本没有可阅读性。
jquery-1.12.4.js:未压缩版本，适用于学习与开发环境，源码清晰，易阅读。
```

## 入口函数

```js
05 - jquery的入口函数.html;
06 - jQuery的入口函数与window.onload的对比.html;
```

入口函数的好处：

```javascript
1. 等待文档加载完成，保证能够获取到元素
2. 形成了一个沙箱，防止全局变量污染。
```

两种写法：

```javascript
//第一种写法
$(document).ready(function () {});
//第二种写法
$(function () {});
```

jQuery 入口函数与 js 入口函数的对比

```javascript
1.	JavaScript的入口函数要等到页面中所有资源（包括图片、文件）加载完成才开始执行。
2.	jQuery的入口函数只会等待文档树加载完成就开始执行，并不会等待图片、文件的加载。
```

## jQuery 对象与 DOM 对象

基本概念：

```javascript
1. DOM对象：使用JavaScript中的方法获取页面中的元素返回的对象就是dom对象。
2. jQuery对象：jquery对象就是使用jquery的方法获取页面中的元素返回的对象就是jQuery对象。
3. jQuery对象其实就是DOM对象的包装集（包装了DOM对象的集合（伪数组））
```

jQuery 对象与 DOM 对象的区别：

```javascript
1. DOM对象与jQuery对象的方法不能混用。
2. DOM对象可以和jQuery对象相互转化
```

DOM 对象转换成 jQuery 对象：

```javascript
var $obj = $(domObj);
// $(document).ready(function(){}); 就是典型的DOM对象转jQuery对象
```

jQuery 对象转换成 DOM 对象：

```javascript
var $li = $(“li”);
//第一种方法（推荐使用）
$li[0]
//第二种方法
$li.get(0)
```

# 选择器

## 什么是 jQuery 选择器

jQuery 选择器是 jQuery 为我们提供的一组方法，让我们更加方便的获取到页面中的元素。注意：jQuery 选择器返回的是 jQuery 对象。

jQuery 选择器有很多，基本兼容了 CSS1 到 CSS3 所有的选择器，并且 jQuery 还添加了很多更加复杂的选择器。

## css 选择器

> jQuery 完全兼容 css 选择器

| 名称       | 用法               | 描述                                                           |
| ---------- | ------------------ | :------------------------------------------------------------- |
| ID 选择器  | $(“#id”);          | 获取指定 ID 的元素                                             |
| 类选择器   | $(“.class”);       | 获取同一类 class 的元素                                        |
| 标签选择器 | $(“div”);          | 获取同一类标签的所有元素                                       |
| 并集选择器 | $(“div,p,li”);     | 使用逗号分隔，只要符合条件之一就可。                           |
| 交集选择器 | $(“div.redClass”); | 获取 class 为 redClass 的 div 元素                             |
| 子代选择器 | $(“ul>li”);        | 使用>号，获取儿子层级的元素，注意，并不会获取孙子层级的元素    |
| 后代选择器 | $(“ul li”);        | 使用空格，代表后代选择器，获取 ul 下的所有 li 元素，包括孙子等 |

> 跟 CSS 的选择器一模一样。

## 过滤选择器

> 这类选择器都带冒号:

| 名称         | 用法                               | 描述                                                                |
| ------------ | ---------------------------------- | :------------------------------------------------------------------ |
| :eq（index） | $(“li:eq(2)”).css(“color”, ”red”); | 获取到的 li 元素中，选择索引号为 2 的元素，索引号 index 从 0 开始。 |
| :odd         | $(“li:odd”).css(“color”, ”red”);   | 获取到的 li 元素中，选择索引号为奇数的元素                          |
| :even        | $(“li:even”).css(“color”, ”red”);  | 获取到的 li 元素中，选择索引号为偶数的元素                          |
| :first       | $(“li:first”).css(“color”, ”red”); | 获取到的 li 元素中的第一个                                          |
| :last        | $(“li:last”).css(“color”, ”red”);  | 获取到的 li 元素中的最后一个                                        |

了解更多可参考<a href="https://www.w3school.com.cn/jquery/jquery_ref_selectors.asp">选择器</a>

## 筛选选择器(方法)

> 筛选选择器的功能与过滤选择器有点类似，但是用法不一样，`筛选选择器`主要是方法。

| 名称               | 用法                        | 描述                                  |
| ------------------ | --------------------------- | :------------------------------------ |
| children(selector) | $(“ul”).children(“li”)      | 获取当前元素的所有子元素中的 li 元素  |
| find(selector)     | $(“ul”).find(“li”);         | 获取当前元素中的后代元素中的 li 元素  |
| siblings(selector) | $(“#first”).siblings(“li”); | 查找兄弟节点，不包括自己本身。        |
| parent()           | $(“#first”).parent();       | 查找父亲                              |
| eq(index)          | $(“li”).eq(2);              | 相当于`$(“li:eq(2)”)`,index 从 0 开始 |
| next()             | $(“li”).next()              | 找下一个兄弟                          |
| prev()             | $(“li”).prev()              | 找上一次兄弟                          |

# 其他补充

## mouseover 与 mouseenter

> mouseover 和 mouseoverenter 都有鼠标经过的意思，但是在注册鼠标经过事件的时候，推荐使用`mouseenter`

[mouseenter 与 mouseover 的不同](http://www.w3school.com.cn/tiy/t.asp?f=jquery_event_mouseenter_mouseover)

1. mouseover 与 mouseout 是一对事件，当鼠标经过当前元素或者当前元素的子元素的时候，mouseover 事件都会触发。
2. mouseenter 与 mouseleave 是一对事件，只有当鼠标经过当前元素时，事件会触发，鼠标经过子元素，mousenter 事件是不会触发的。

## index 方法

> `index()`方法返回的是当前元素在所有兄弟元素里面的索引。

## 区分 jQuery 与 Javascript

JavaScript 是一门编程语言，jQuery 仅仅是用 JavaScript 实现的一个 JavaScript 库，目的是简化我们的开发。

摘抄自黑马
