---
title: ajax
toc: true
comments: true
tags:
  - ajax
categories:
  - ajax
description:
  - 可以在页面不刷新的情况下，请求服务器，局部更新页面的数据
abbrlink: c5a6a264
date: 2020-12-12 19:50:38
updated: 2020-12-12 19:50:38
---

## AJAX 技术

<!-- more -->

> 即 Asynchronous Javascript And XML，AJAX 不是一门的新的语言，而是对现有持术的综合利用。

- 本质:是在 HTTP 协议的基础上通过 js 的 XMLHttpRequest 对象与服务器进行通信。

- 作用：可以在页面不刷新的情况下，请求服务器，局部更新页面的数据；

### 异步 与 同步(了解)

> 指某段程序执行时不会阻塞其它程序执行，其表现形式为程序的执行顺序不依赖程序本身的书写顺序，相反则为同步。

> 同步：同一时刻只能做一件事，上一步完成才能开始下一步

- 异步：同时做多件事，效率更高,做一件事情时，不影响另一件事情的进行。

XMLHttpRequest 可以以异步方式的处理程序。

## XMLHttpRequest

> 浏览器内建对象，用于在后台与服务器通信(交换数据) ， 由此我们便可实现对网页的部分更新，而不是刷新整个页面。

### 发送 get 请求

XMLHttpRequest 以异步的方式发送 HTTP 请求，因此在发送请求时，一样需要遵循 HTTP 协议。

```javascript
//使用XMLHttpRequest发送get请求的步骤
//1. 创建一个XMLHttpRequest对象
var xhr = new XMLHttpRequest();
//2. 设置请求行
//第一个参数:请求方式  get/post
//第二个参数:请求的地址 需要在url后面拼上参数列表
xhr.open("get", "08.php?name=hucc");
//3. 设置请求头
xhr.setReqeustHeader("content-type", "text/html");
//浏览器会给我们默认添加基本的请求头,get请求时无需设置
//4. 设置请求体
//get请求的请求体为空,因为参数列表拼接到url后面了
xhr.send(null);
```

- get 请求,设置请求行时,需要把参数列表拼接到 url 后面
- get 请求不用设置请求头
- get 请求的请求体为 null

### 发送 post 请求

```javascript
var xhr = new XMLHttpRequest();
//1. 设置请求行 post请求的参数列表在请求体中
xhr.open("post", "09.php");
//2. 设置请求头, post请求必须设置content-type,不然后端无法获取到数据
xhr.setRequestHeader("content-type", "application/x-www-form-urlencoded");
//3. 设置请求体
xhr.send("name=hucc&age=18");
```

- post 必须设置请求头中的 content-type 为 application/x-www-form-urlencoded

- post 请求需要将参数列表设置到请求体中

### 获取响应

HTTP 响应分为 3 个部分，状态行、响应头、响应体。

```javascript
//给xhr注册一个onreadystatechange事件，当xhr的状态发生状态发生改变时，会触发这个事件。
xhr.onreadystatechange = function () {
  if (xhr.readyState == 4) {
    //1. 获取状态行
    console.log("状态行:" + xhr.status);
    //2. 获取响应头
    console.log("所有的相应头:" + xhr.getAllResponseHeaders());
    console.log("指定相应头:" + xhr.getResponseHeader("content-type"));
    //3. 获取响应体
    console.log(xhr.responseText);
  }
};
```

**readyState**

> readyState:记录了 XMLHttpRequest 对象的当前状态

```javascript
//0：请求未初始化（还没有调用 open()）。
//1：请求已经建立，但是还没有发送（还没有调用 send()）。
//2：请求已发送，正在处理中
//3：请求在处理中；通常响应中已有部分数据可用了，但是服务器还没有完成响应的生成。
//4：响应已完成；您可以获取并使用服务器的响应了。(我们只需要关注状态4即可)
```
