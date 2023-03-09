---
title: jQuery动画
toc: true
comments: true
tags:
  - jQuery
  - JavaScript
categories:
  - JavaScript
keywords:
  - jquery
  - 动画
  - animate
description:
  - jquery提供了三组基本动画，这些动画都是标准的、有规律的效果，jquery还提供了自定义动画的功能。
abbrlink: 41a23917
date: 2020-11-17 18:41:17
updated: 2020-11-17 18:41:17
---

# jQuery 动画

<!-- more -->

> jquery 提供了三组基本动画，这些动画都是标准的、有规律的效果，jquery 还提供了自定义动画的功能。

## 三组基本动画

> 显示(show)与隐藏(hide)是一组动画：
> 滑入(slideUp)与滑出(slideDown)与切换(slideToggle)，效果与卷帘门类似
> 淡入(fadeIn)与淡出(fadeOut)与切换(fadeToggle)

```javascript
show([speed], [callback]);
//speed(可选)：动画的执行时间
//1.如果不传，就没有动画效果。如果是slide和fade系列，会默认为normal
//2.毫秒值(比如1000),动画在1000毫秒执行完成(推荐)
//3.固定字符串，slow(200)、normal(400)、fast(600)，如果传其他字符串，则默认为normal。
//callback(可选):执行完动画后执行的回调函数
```

## 自定义动画

> animate: 自定义动画

```javascript
$(selector).animate({ params }, [speed], [easing], [callback]);
// {params}：要执行动画的CSS属性，带数字（必选）
// speed：执行动画时长（可选）
// easing:执行效果，默认为swing（缓动）  可以是linear（匀速）
// callback：动画执行完后立即执行的回调函数（可选）
```

## 动画队列与停止动画

> 在同一个元素上执行多个动画，那么对于这个动画来说，后面的动画会被放到动画队列中，等前面的动画执行完成了才会执行（联想：火车进站）。

```javascript
//stop方法：停止动画效果
stop(clearQueue, jumpToEnd);
//第一个参数：是否清除队列
//第二个参数：是否跳转到最终效果
```
