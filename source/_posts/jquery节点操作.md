---
title: jquery节点操作
toc: true
comments: true
tags:
  - jQuery
  - JavaScript
categories:
  - JavaScript
keywords:
  - jquery
  - 节点
description:
  - jquery进行节点的添加，删除等操作
abbrlink: 1f934ad9
date: 2020-11-17 19:04:03
updated: 2020-11-17 19:04:03
---

# jQuery 节点操作

## 创建节点

<!-- more -->

> $() $('div') $(document)  
> 如果参数是一个选择器， 获取页面中的元素
> 如果参数是一个 DOM 对象， 把 DOM 对象变成 jq 对象
> 如果参数是一段 html， 把 html 创建成 jq 对象

```javascript
//$(htmlStr)
//htmlStr：html格式的字符串
$(“<span>这是一个span元素</span>”);

```

## 添加节点

```javascript
parent.append(child);
child.appendTo(parent);
parent.prepend(child); //把child添加到parent的子元素的最前面
child.prependTo(parent); //把child添加到parent的子元素的最前面
A.before(B); //把B添加到a的前面，作为兄弟元素
A.after(B); //把B添加到A的后面
```

append 的特殊用法 append 参数可以允许直接是一段 html

appendTo 的特殊用法: 允许 appendTo 的参数直接是一个选择器

## 清空节点与删除节点

> empty：清空指定节点的所有元素，自身保留(清理门户)

```javascript
$(“div”).empty();//清空div的所有内容（推荐使用，会清除子元素上绑定的内容，源码）
$(“div”).html(“”);//使用html方法来清空元素，不推荐使用，会造成内存泄漏，绑定的事件不会被清除。
```

> remove：相比于 empty，自身也删除（自杀）

```javascript
$(“div”).remove();
```

## 克隆节点

> 作用：复制匹配的元素

```javascript
$(selector).clone();
// 参数： true 或者 false
// 如果参数是false，也是深克隆， 也会克隆所有的内容
// 如果参数为true, 不仅是深克隆，把元素本身所有的事件也会克隆
```
