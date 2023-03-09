---
title: js获取元素的方法
categories: JavaScript
keywords: 获取元素
tags:
  - JavaScript
abbrlink: 4eadaa44
date: 2020-10-22 21:04:11
---
# 获取元素的方法

## 根据id获取
<!--more-->
```javascript
//参数：元素的id
//返回值：一个元素，如果id不存在，返回null
document.getElementById("id");
```

## 根据标签名获取

```javascript
//参数：标签名
//返回值：伪数组，无论有几个元素，返回都是伪数组
document.getElementsByTagName("tagName");
box.getElementsByTagName("tagName");
```

这两个方法是没有任何兼容性问题的。



## 根据类名获取

```javascript
//参数：字符串类型的类名
//返回值：伪数组
document.getElementsByClassName("class")
```

**注意：这个方法ie678不支持**



## 根据name获取

```javascript
//只适用于表单元素
var ps = document.getElementsByName("aa");
```



## 根据css选择器获取

```java
//参数：是一个css选择器，，   如果是类选择器，  .demo   如果是id选择器：  #aa
//返回值：只会返回一个对象，如果有很多个，会返回第一个
document.querySelector();

//参数：是一个css选择器
//返回值：会返回伪数组，不管有多少个，都会返回伪数组
document.querySelectorAll();
```

