---
title: php文件引入
toc: true
comments: true
tags:
  - php
categories:
  - php
description:
  - 不同的页面中有相同的代码部分，可以将其分离为单个文件。需要调用时，引入对应的文件即可调用。提高代码的复用率。
keywords:
  - php
  - include
  - include_once
  - require
  - require_once
abbrlink: bf8e8cab
date: 2020-11-25 16:58:40
updated: 2020-11-25 16:58:40
---

# 文件引入

​ 不同的页面中有相同的代码部分，可以将其分离为单个文件。需要调用时，引入对应的文件即可调用。提高代码的复用率。

<!-- more -->

**语法**

```php
include | include_once   "文件的路径";
require | require_once   "文件路径";
```

**include 与 rinclude_once 区别**

> 都是语言结构，不是函数。

- include 可以重复引入文件

- include_once 只引入一次，防止多次引入文件

require 和 require_once 同理

**require 和 include 区别**

- include 如果引入文件存在，后面代码还会继续执行；

- require 引入的文件不存在，后面代码就不执行了；

# 页面动态渲染

- PHP 本身支持与 HTML 混编

- 混编的文件后缀必须为.php，Apache 才会调用 PHP 解析

- PHP 与 HTML 混编时，服务器中的 PHP 引擎 只会执行 php 标签内部的 PHP 代码，非 PHP 的代码(PHP 标签外部的内容)直接忽略，最后会将 PHP 的执行结果和非 PHP 代码 一起返回给浏览器,由浏览器进行解析

- ​

  ```php
  <?php
      header('content-type:text/html;charset=utf-8');
      echo 2+3;
      //php的引擎 只会执行php代码块中代码，代码块外面的代码会被忽略
      //最后 服务器会将php执行的结果 和代码块外面的内容一起返回给 浏览器，
      //由浏览器进行解析
  ?>
  <a href="http://www.baidu.com">百度一下</a>
  ```
