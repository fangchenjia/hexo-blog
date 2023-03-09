---
title: js事件
categories: JavaScript
keywords: 事件
tags:
  - JavaScript
abbrlink: 9fabc801
date: 2020-10-30 18:38:23
---
# 事件对象

## 事件对象的概述

> 在触发某个事件的时候，都会产生一个事件对象Event，这个对象中包含所有与事件相关的一些信息，包括触发事件的元素，事件的类型以及其他与事件相关的信息。
<!--more-->
鼠标事件触发时，事件对象中会包含鼠标的位置信息。

键盘事件触发时，事件对象中会包含按下的键相关的信息。


## 获取事件对象

> 既然事件对象中存储了这么多的信息，我们首先需要做的就是获取到这个事件对象。获取事件对象的时候，存在浏览器的兼容问题。

对于现代浏览器，获取事件对象非常的简单，只需要在注册事件的时候，指定一个形参即可。这个形参就是我们想要获取到的事件对象。

```
btn.onclick = function(event){
    //event就是事件对象，里面包含了事件触发时的一些信息。
	console.log(event);
}
```

对于IE678来说，获取事件对象则是另一种方式，在事件里面，通过window.event来获取事件对象

```
btn.onclick = function(){
	//IE678通过window.event获取事件对象
	var event = window.event;
	console.log(event);
}
```

兼容性封装

```
btn.onclick = function(event){
  	//只要用到了事件对象，就要记得处理浏览器兼容性
	event = event || window.event;
}
```

## 事件对象的常用属性

> 事件对象中有很多很多的属性，但是很多属性并不常用。我们经常用到的是***鼠标位置信息*** 和***键盘码***  相关的信息。


记录了鼠标位置信息的相关属性

```javascript
clientX与clientY：鼠标相对于可视区左上角的水平位置和垂直位置。
pageX与pageY：鼠标相对于网页（文档document）左上角的水平位置与垂直位置（推荐使用）
screenX与screenY：鼠标相对于屏幕左上角的水平位置与垂直位置。
```

记录了键盘码的属性

```javascript
event.keyCode:键盘按下的那个键的键盘码
```

# 注册事件的方式

## on+事件名称

> onclick、onmouseover这种on+事件名称的方式注册事件几乎所有的浏览器都支持。

注册事件：

```
box.onclick = function(){
	//事件处理程序	
}
```

移除事件：

```javascript
box.onclick = null;	
```

on+事件名称注册事件的缺点：

同一个元素同一类型的事件，只能注册一个，如果注册了多个，会出现覆盖问题。

## 注册事件的新方式

**addEventListener与removeEventListener**

> 现代浏览器支持的注册事件的新方式，这种方式注册的事件不会出现覆盖问题。

addEventListener的语法

```javascript
//第一个参数：事件的类型：click mouseover
//第二个参数：函数，监听者，每次事件触发，这个函数就执行。
//第三个参数：可选，默认值是false
addEventListener(type, func, useCapture);
```

<font color="red">tips：如果想要让你注册的事件能够移除，不能使用匿名函数。</font>

```
function fn1() {
    alert("hehe");
}
//如果想让注册的事件能移除，不能用匿名函数。
box.addEventListener("click", fn1);
```

removeEventListen的语法

```javascript
//第一个参数：参数类型
//第二个参数：要移除的那个函数
//第三个参数：false
removeEventListener(type, func, useCapture);
```

**attachEvent与detachEvent**

> IE678不支持addEventListener与removeEventListen两个方法，但是支持attachEvent与detachEvnet

attachEvent的用法：

```javascript
//type:事件类型   需要加上on   onclick  onmouseenter
//func:需要执行的那个事件
attachEvent(type, func)
```

detachEvent的用法

```javascript
//type:事件类型   需要加上on   onclick  onmouseenter
//func:需要执行的那个事件
detachEvent(type, func)
// 同样，如果需要移除使用attachEvent注册的事件，那么事件处理函数需要给一个函数名，这样才能移除掉。
```

# 事件流

## 事件冒泡

> 当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素中依次被触发。这一过程被称为事件冒泡。

说白了就是：当我们触发了子元素的某个事件后，父元素对应的事件也会触发。 ![bubble](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/js%E4%BA%8B%E4%BB%B6/bubble.png)

通常情况，事件冒泡对于我们来说是没有问题的，我们直接不管就行了，但是如果当事件冒泡给我们带来影响的时候，我们需要阻止事件冒泡。


```javascript
link.onclick = function (event) {
    //stop :停止  propagation：传播
    event.stopPropagation();
}
```

## 事件捕获（了解）

> 事件捕获是火狐浏览器提出来的，IE678不支持事件捕获（基本上，我们都是用事件冒泡）
> 事件的处理将从DOM层次的根开始，而不是从触发事件的目标元素开始，事件被从目标元素的所有祖先元素依次往下传递

 ![capture](	https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/js%E4%BA%8B%E4%BB%B6/capture.png)

```
//当addEventListener第三个参数为true时，表示事件捕获
arr[i].addEventListener("click", function () {
    console.log(this);
},true);
```



## 事件的三个阶段

1. 事件的捕获阶段
2. 事件的目标阶段（触发自己的事件）
3. 事件的冒泡阶段

 ![three](	https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/js%E4%BA%8B%E4%BB%B6/three.png)



事件有三个阶段，首先发生的是捕获阶段，然后是目标阶段，最后才是冒泡阶段，让`addEventLinstener`第三个参数为true时，表示该事件在捕获阶段发生，如果第三个参数为false，表示该事件在冒泡阶段发生。

## 常见的事件

> 常见的鼠标事件

onmousedown:鼠标按下事件

onmouseup:鼠标弹起事件

onclick:单击事件

ondblclick：双击事件

onmouseover：鼠标经过事件

onmouseout：鼠标离开事件

onmousemove：鼠标移动事件

onfocus：鼠标获得焦点事件

onblur：鼠标失去焦点事件



> 常见的键盘事件

onkeydown:键盘按下时触发

onkeyup:键盘弹起时触发

> 对于鼠标事件，事件对象中有一系列的XY记录了鼠标的位置信息。而键盘事件中，事件对象有一个event.keyCode属性，记录了按下去的键的键盘码



