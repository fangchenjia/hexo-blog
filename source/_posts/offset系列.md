---
title: offset系列
categories: JavaScript
keywords: offset
tags:
  - JavaScript
abbrlink: a8c42e27
date: 2020-10-26 22:35:33
---
# offset系列

> offset系列用于用于获取元素自身的大小和位置，在网页特效中有广泛应用
> offset系列主要有：offsetHeight、offsetWidth、offsetParent、offsetLeft、offsetTop
<!--more-->
## offsetHeight与offsetWidth

> offsetHeight与offsetWidth
```javascript
1.	获取的是元素真实的高度和宽度
2.	获取到的是数值类型，方便计算
3.	offsetHeight与offsetWidth是只读属性，不能设置。
```

> style.height与style.width

```javascript
1.	只能获取行内样式
2.	获取到的是字符串类型，需要转换
```

> ***结论***

```javascript
1. 设置宽度高度使用style.width与style.height
2. 获取宽度和高度offsetWidth与offsetHeight
```

## offsetParent

> parentNode和offsetParent

```javascript
1. parentNode始终是父元素
2. offsetParent是离当前元素最近的定位元素(absolute、relative)，如果没有，那就找body
```


## offsetLeft与offsetTop

> offsetLeft: 自身左侧到offsetParent左侧的距离：left + margin-left
> offsetTop:自身顶部到offsetParent顶部的距离 :  top + margin-top

> offsetLeft与offsetTop
```javascript
1.	元素自身与offsetParent真实的距离
2.	获取到的是数值类型，方便计算
3.	只读属性，只能获取，不能设置
```

> style.left与style.top

```javascript
1.	只能获取行内样式
2.	获取到的是字符串，需要转换
3.	可以获取，也可以设置
```

> **结论**

```javascript
获取操作：用offset系列
设置操作：用style.xxx进行设置。
```
