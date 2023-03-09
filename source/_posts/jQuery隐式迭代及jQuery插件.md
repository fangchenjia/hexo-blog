---
title: jQuery隐式迭代及jQuery插件
toc: true
comments: true
tags:
  - JavaScript
  - jQuery
categories:
  - JavaScript
description:
  - each方法，链式编程，jQuery插件
keywords:
  - Jquery
  - each
  - 链式编程
  - 插件
abbrlink: 6694a831
date: 2020-11-22 19:45:07
updated: 2020-11-22 19:45:07
---

# jQuery 补充知识点

## 隐式迭代

### 基本概念

> 隐式迭代：jQuery 在设置属性时会自动的遍历，因此我们不需要再遍历

1. jQuery 在执行设置性操作时，会给所有的元素都设置上相同的值。
2. jQuery 在执行获取性操作时，只会返回第一个元素对应的值。
3. 如果想要给每一个元素都设置不同的值，需要手动进行遍历 jQuery 对象。

### each 方法

> 遍历 jQuery 对象集合，为每个匹配的元素执行一个函数

语法：

```javascript
// 参数一表示当前元素在所有匹配元素中的索引号
// 参数二表示当前元素, 在function中this也表示当前元素。
$(selector).each(function (index, element) {});
```

## 链式编程

> 链式编程的原理：设置性操作会返回一个 jQuery 对象，因此可以继续调用 jQuery 的方法。

1. 设置操作的时候，可以使用链式编程。
2. 获取操作的时候，无法使用链式编程。

```javascript
end(); // 筛选选择器会改变jQuery对象的DOM对象，回到上一次的状态，并且返回匹配元素之前的状态。
```

```javascript
prevAll(); //获取前面所有的兄弟元素
nextAll(); //获取后面所有的兄弟元素
siblings(); //获取所有的兄弟元素
prev(); //获取前一个兄弟
next(); //获取后一个兄弟。
```

## 多库共存

> jQuery 使用`$`作为标示符，但是如果与其他框架中的$冲突时，jQuery可以释放`$`符的控制权.

```javascript
var c = $.noConflict(); //释放$的控制权,并且把$的能力给了c
```

# jQuery 插件

> 插件：jquery 不可能包含所有的功能，我们可以通过插件扩展 jquery 的功能。

jQuery 有着丰富的插件，使用这些插件能给 jQuery 提供一些额外的功能。

## 使用插件

```javascript
1. 引入jQuery文件
2. 引入插件（如果有用到css的话，需要引入css）
3. 使用插件
```

常用插件的使用

- jquery.color.js 的使用

  - https://github.com/jquery/jquery-color

- jquery.lazyload.js 的使用
  - https://github.com/tuupola/jquery_lazyload

## 制作 jQuery 插件

> 制作 jQuery 插件的核心思想：给 jQuery 的原型增加方法即可。

```javascript
$.fn.pluginName = function () {};
```
