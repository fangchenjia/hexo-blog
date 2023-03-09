---
title: a标签的用法
summary: html的<a>标签用法
categories: html
keywords: html a 超链接
tags:
  - html
abbrlink: 89b00366
date: 2020-09-26 23:10:32
---
## 1.构建外部超链接
### 基本语法：
`<a href="url">Link text</a>`
<!--more-->
### target属性:
|值|描述
|-----|-----
|_blank|在新窗口中打开被链接文档。
|_self|默认。在相同的框架中打开被链接文档。
|_parent|在父框架集中打开被链接文档。
|_top|在整个窗口中打开被链接文档。能跳出框架。
|framename|在指定的框架中打开被链接文档。
### title属性
利用title属性可以给超链接添加简短说明
`<a href="https://www.baidu.com" title="https://www.baidu.com" target="_blank">百度</a>`
## 2.构建锚点（即标记本html页面中的一个点，通过点击a标签，直接跳转到那个位置。）
### id方式
```html
<a href="#cosy" >爱代码的阿拉</a>
<p id="cosy">爱代码的阿拉，正在努力学习中</p>
```
### 特殊锚点
```html
<a href="#">回到网页最顶部</a>
<a href="javascript:void(0)">不跳转</a>
```



