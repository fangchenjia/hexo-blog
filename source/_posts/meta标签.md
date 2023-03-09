---
title: meta标签
toc: true
mathjax: false
summary: html笔记
categories: html
keywords: html meta
tags:
  - html
abbrlink: 8fd588e7
date: 2020-09-25 21:40:56
---

# meta标签的组成
`meta`标签共有两个属性：
<!--more-->
```
1. http-equiv属性
2. name属性
```
不同的属性又有不同的参数值，这些不同的参数值就实现了不同的网页功能。
## http-equiv属性
`http-equiv`顾名思义，相当于http的文件头作用，它可以向浏览器传回一些有用的信息，以帮助正确和精确地显示网页内容，与之对应的属性值为`content`，`content`中的内容其实就是各个参数的变量值。

`meta`标签的`http-equiv`属性语法格式是：

`＜meta http-equiv="参数" content="参数变量值"＞`

其中http-equiv属性主要有以下几种参数：
```html
1.<meta http-equiv="Set-Cookie" content="cookievalue=xxx; expires=Friday,12-Jan-2001 18:18:18 GMT; path=/">:如果网页过期，那么存盘的cookie将被删除。必须使用GMT的时间格式。
2.<meta http-equiv='expires' content='时间' >：用于设定网页的到期时间。一旦网页过期，必须到服务器上重新传输。
3.<meta http-equiv="Refresh" content="5;URL">：告诉浏览器在【数字】秒后跳转到【一个网址】
4.<meta http-equiv="content-Type" content="text/html; charset=utf-8">：设定页面使用的字符集。
  <meta charset="utf-8">：在HTML5中设定字符集的简写写法。
5.<meta http-equiv="Pragma" content="no-cache">：禁止浏览器从本地计算机的缓存中访问页面内容。访问者将无法脱机浏览。
6.<meta http-equiv="Window-target" content="_top">：用来防止别人在iframe(框架)里调用自己的页面，这也算是一个非常实用的属性。
7.<meta http-equiv='X-UA-Compatible' content='IE=edge,chrome=1'> :强制浏览器按照特定的版本标准进行渲染。但不支持IE7及以下版本。如果是ie浏览器就用最新的ie渲染，如果是双核浏览器就用chrome内核。
```
## name属性
主要用于描述网页，与之对应的属性值为`conten`t，`content`中的内容主要是便于搜索引擎机器人查找信息和分类信息用的。

meta标签的name属性语法格式是：

`＜meta name="参数" content="具体的参数值"＞`

```html
1.<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">：在移动设备浏览器上，禁用缩放（zooming）功能，用户只能滚动屏幕。
2.<meta name="description" content="">：告诉搜索引擎，当前页面的主要内容是xxx。
3.<meta name="keywords" content="">：告诉搜索引擎，当前页面的关键字。
4.<meta name="author" content="">：告诉搜索引擎，标注网站作者是谁。
5.<meta name="copyright" content="">：标注网站的版权信息。
```

meta中name标签的功能

１、帮助主页被各大搜索引擎登录
meta标签的一个很重要的功能就是设置关键字，来帮助你的主页被各大搜索引擎登录，提高网站的访问量。

在这个功能中，最重要的就是对`Keywords`和`description`的设置。因为按照搜索引擎的工作原理,搜索引擎首先派出机器人自动检索页面中的`keywords`和`decription`，并将其加 入到自己的数据库，然后再根据关键词的密度将网站排序。

因此，我们必须设置好关键字，来提高页面的搜索点击率。下面我们来举一个例子供大家参考：

```html
<meta name="keywords" content="网页,网页制作,网页特效,建站指南,教程下载,动画制作,网页教学，网页素材，视频教程，技术论坛，免费空间，免费域名">
<meta name="description" content="网页教学网,专业的网页教学网站">
```
设置好这些关键字后，搜索引擎将会自动把这些关键字添加到数据库中，并根据这些关键字的密度来进行合适的排序。

转载自https://www.jianshu.com/p/179ddc16ef55