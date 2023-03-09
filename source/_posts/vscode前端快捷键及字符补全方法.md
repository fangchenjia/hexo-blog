---
title: vscode前端快捷键及字符补全方法
categories: tool
toc: true
tags:
  - vscode
keywords: vscode 快捷键 字符补全
abbrlink: ba36578f
date: 2020-10-08 20:25:40
---
# 1.快捷键的使用
<!--more-->
|快捷键|说明|
|----|----|
|Tab|补全代码|
|Alt + Tab|切换windows窗口|
|Ctrl + A|	选择全部代码| 
|Ctrl + C|	复制|
|Ctrl + V|	粘贴|
|Ctrl + X|	剪切|
|Ctrl + Z|	返回上一次操作|
|Ctrl + F|	查找|
|Ctrl + /|	添加或取消注释|
|Ctrl + + / -|	放大/缩小|
|Ctrl + F1	|打开浏览器|
|F12	|浏览器中为启用调试模式|
|F11	|浏览器中为全屏|

# 2.字符补全

## 多项：`*`
缩写：`ul>li*5`
```html
<ul>
   <li></li>
   <li></li>
   <li></li>
   <li></li>
   <li></li>
</ul>
```
## Class类：`.`
缩写：`div.top*2`（Class类可以多次使用）
```html
<div class="top"></div>
<div class="top"></div>
```
缩写：`p.class1.class2.class3`
```html
<p class="class1 class2 class3"></p>
```
## Id类：`#`
缩写：`div#top`(一个Id类只能使用一次)
```html
<div id="top"></div>
```
缩写：`form#search.wide`
```html
<form id="search" class="wide"></form>
```
## 自增符号：`$`
缩写：`ul>li.item$*5`
```html
<ul>
    <li class="item1"></li>
    <li class="item2"></li>
    <li class="item3"></li>
    <li class="item4"></li>
    <li class="item5"></li>
</ul>
```
## 子元素：`>`
缩写：`nav>ul>li`
```html
<nav>
    <ul>
        <li></li>
    </ul>
</nav>
```
## 兄弟元素：`+`
缩写：`div+div>p>span+em`
```html
<div></div>
<div>
    <p><span></span><em></em></p>
</div>
```

## 自定义属性：`[]`
缩写：`p[title=”Hello world”]`
```html
<p title="Hello world"></p>
```
缩写：`td[rowspan=2 colspan=3 title]`
```html
<td rowspan="2" colspan="3" title=""></td>
```
## 文本：`{}`
缩写：`a{Click me}`
```html
<a href="">Click me</a>
```
