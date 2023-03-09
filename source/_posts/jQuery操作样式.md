---
title: jQuery操作样式
toc: true
comments: true
tags:
  - jQuery
  - JavaScript
categories:
  - JavaScript
description:
  - 使用jquery进行样式操作
keywords:
  - Jquery
  - 样式
abbrlink: e124a1ea
date: 2020-11-16 21:40:49
updated: 2020-11-16 21:40:49
---

# jQuery 操作样式

<!-- more -->

## css 操作

> 功能：设置或者修改样式，操作的是 style 属性。

> 操作单个样式

```javascript
//name：需要设置的样式名称
//value：对应的样式值
css(name, value);
//使用案例
$("#one").css("background", "gray"); //将背景色修改为灰色
```

> 设置多个样式

```javascript
//参数是一个对象，对象中包含了需要设置的样式名和样式值
css(obj);
//使用案例
$("#one").css({
  background: "gray",
  width: "400px",
  height: "200px",
});
```

> 获取样式

```javascript
//name:需要获取的样式名称
css(name);
//案例
$("div").css("background-color");
```

注意：获取样式操作只会返回第一个元素对应的样式值。

隐式迭代：

1. 设置操作的时候，如果是多个元素，那么给所有的元素设置相同的值
2. 获取操作的时候，如果是多个元素，那么只会返回第一个元素的值。

## class 操作

> 添加样式类

```javascript
//name：需要添加的样式类名，注意参数不要带点.
addClass(name);
//例子,给所有的div添加one的样式。
$(“div”).addClass(“one”);

```

> 移除样式类

```javascript
//name:需要移除的样式类名
removeClass(“name”);
//例子，移除div中one的样式类名
$(“div”).removeClass(“one”);

```

> 判断是否有某个样式类

```javascript
//name:用于判断的样式类名，返回值为true false
hasClass(name)
//例子，判断第一个div是否有one的样式类
$(“div”).hasClass(“one”);

```

> 切换样式类

```javascript
//name:需要切换的样式类名，如果有，移除该样式，如果没有，添加该样式。
toggleClass(name);
//例子
$(“div”).toggleClass(“one”);

```

# jQuery 操作属性

## attr 操作

> 设置单个属性

```javascript
//第一个参数：需要设置的属性名
//第二个参数：对应的属性值
attr(name, value);
//用法举例
$(“img”).attr(“title”,”哎哟，不错哦”);
$(“img”).attr(“alt”,“哎哟，不错哦”);

```

> 设置多个属性

```javascript
//参数是一个对象，包含了需要设置的属性名和属性值
attr(obj);
//用法举例
$("img").attr({
  title: "哎哟，不错哦",
  alt: "哎哟，不错哦",
  style: "opacity:.5",
});
```

> 获取属性

```javascript
//传需要获取的属性名称，返回对应的属性值
attr(name);
//用法举例
var oTitle = $("img").attr("title");
alert(oTitle);
```

> 移除属性

```javascript
//参数：需要移除的属性名，
removeAttr(name);
//用法举例
$("img").removeAttr("title");
```

## prop 操作

> 在 jQuery1.6 之后，对于 checked、selected、disabled 这类 boolean 类型的属性来说，不能用 attr 方法，只能用 prop 方法。

```javascript
//设置属性
$(“:checked”).prop(“checked”,true);
//获取属性
$(“:checked”).prop(“checked”);//返回true或者false

```
