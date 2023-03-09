---
title: text文本相关属性
toc: true
categories: CSS
tags:
  - CSS
keywords: css text
abbrlink: 7fe1f322
date: 2020-10-07 11:25:10
---
# text- 文本相关属性

### text-indent：文本的缩进

> 设置文字的缩进
<!--more-->
**取值：**

- px（像素）
- em（一个文字的大小）

**注意：**

- 单位是 em，1em代表一个文字的宽度 ，2em标签首行缩进两个字符。

### text-align：文本的对齐方式

> 设置文字的对齐方式（水平居中）

**取值：**

- left：设置`内容`在盒子中 **靠左**

- center：设置`内容`在盒子中 **水平居中**
- right：设置`内容`在盒子中 **靠右**

**注意：**

- 能让哪些元素位置居中???

  文本、图片（行内块），span（行内）



### text-decoration：文本的修饰

> 设置文字的修饰（下划线、删除线等）

**取值：**

- none：没有任何装饰（去掉多余的样式）
- underline：下划线
- line-through：删除线

**注意：**

- 一般用的最多的是用text-decoration：none，取消a标签的默认下划线。



**总结：**strong、ins、em、del已经全部都可以被css替换

- strong--------font的bold：加粗
- ins---------underline：下划线
- em--------font的italic：斜体
- del--------line-through：删除线


