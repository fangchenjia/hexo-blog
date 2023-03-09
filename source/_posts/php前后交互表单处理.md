---
title: php前后交互表单处理
toc: true
comments: true
tags:
  - php
categories:
  - php
description:
  - 用php进行前后端交互时的表单处理
keywords:
  - 表单交互
  - php
abbrlink: c31afe2d
date: 2020-11-26 10:22:13
updated: 2020-11-26 10:22:13
---

# 表单处理

> 表单（form）：表单用于收集用户输入信息，并将数据提交给服务器。是一种常见的与服务端数据交互的一种方式

<!-- more -->

```javascript
//1. action：指定表单的提交地址
//2. method:指定表单的提交方式，get/post，默认get
//3. input的数据想要提交到后台，必须指定name属性，后台通过name属性获取值
//4. 想要提交表单，不能使用input:button 必须使用input:submit
```

**php 获取表单数据**

```
 //$_GET是PHP系统提供的一个超全局变量，是一个数组，里面存放了表单通过get方式提交的数据。
 //$_POST是PHP系统提供的一个超全局变量，是一个数组，里面存放了表单通过post方式提交的数据。
```

**get 与 post 的区别**

```
1. get方式
	1.1 数据会拼接在url地址的后面username=hcc&password=123456
	1.2 地址栏有长度限制，因此get方式提交数据大小不会超过4k
2. post方式
	2.1 数据不会在url中显示，相比get方式，post更安全
	2.2 提交的数据没有大小限制

根据HTTP规范，GET用于信息获取，POST表示可能修改变服务器上的资源的请求
```

### 文件上传

**html 要求**

```javascript
1. 文件上传的提交方式必须是post方式
2. 需要给form指定enctype="multipart/form-data"
  enctype(encodetype)是指编码类型。
  multipart/form-data是指表单数据有多部分构成，既有文本数据，又有文件等二进制数据。
  需要注意的是：默认情况下，enctype的值是application/x-www-form-urlencoded，不能用于文件上传，只有使用了multipart/form-data，才能完整的传递文件数据。
  application/x-www-form-urlencoded不是不能上传文件，是只能上传文本格式的文件，multipart/form-data是将文件以二进制的形式上传，这样可以实现多种类型的文件上传。
3. 指定name属性，后台才能获取到
```

**php 相关**

- 文件上传时，通过`$_FILES`才能获取到，这是一个二维数组。

```php
array (size=1)
  'myfile' =>
    array (size=5)
      'name' => string 'IMG_20130614_17445.jpg' (length=22)      //文件名
      'type' => string 'image/jpeg' (length=10)                  //文件类型
      'tmp_name' => string 'C:\wamp\tmp\php40F4.tmp' (length=23) //文件保存临时位置
      'error' => int 0      //错误码 （0表示没有错误）
      'size' => int 103350  //文件大小(字节)
```

- 上传文件时，文件会临时保存在服务器上，如果文件最终没有保存，那么临时文件会被删除，保证服务器安全。

- `sleep(10)`可以让代码延迟 10 秒钟才执行。

- `move_uploaded_file($path, $newPath);`可以保存临时图片

```php
    //服务器保存图片的思路：
	//1-判断 文件不为空 并且 上传文件没有出现错误 的情况下进行保存
    //2-获取临时文件文件路径
    //3-随机生成一个文件名
    //3-进行保存

    //error==0  表示文件上传成功
    if( !empty($_FILES['myfile']) && $_FILES['myfile']['error']==0 ){
        //获取临时文件名
        $ftmp=$_FILES['myfile']['tmp_name'];
        //文件名字随机生成，但是后缀名不能改变
        //1-获取文件原来的后缀名拓展名
        $fname=$_FILES['myfile']['name']; //aa.png
        //2-截取后缀名
        $ext=strrchr($fname,'.');
        //3-生成新的文件名
        $newName=time().rand(1000,9999).$ext;
        //4-保存文件
        move_uploaded_file($ftmp,'./upload/'.$newName);
    }
```

# 表单标签的使用

​ 常见的输入类型：文本域（type=text）、单选按钮(type=radio)、多选按钮（复选项 type=checkbox）、下拉菜单(select>option)、多行文本(textarea);

## 单选项的数据接收

> input 标记的**type** =radio，单选按钮。

> 各个选项均需要指定**name 及 value**值。

> **name 值相同，value 值不同。**

> 可以使用 checked 设置默认选项

**html 结构**

```html
<form action="./01-radio.php" method="get">
  性别：
  <input type="radio" name="sex" value="m" checked />男
  <input type="radio" name="sex" value="f" />女
  <input type="submit" value="登录" />
</form>
```

## 复选框的数据接收

> input 的**type  =checkbox,**可以同时选择多个选项。

> name 命名形式必须为：name[]，最终数据才能以数组的格式，将各个选项的值同时提交，否则只能提交最后一个勾选的属性值。不同的选项值，以数组元素的形式提交。

**html 结构**

```html
<body>
  <!-- 
            action ：指定数据提交的地址
            method:提交方式
            name:必不可少
            name="hobby[]"  复选框的name名后面跟[] 可以提交多个数据 
         -->
  <form action="./02-checkbox.php" method="get">
    兴趣：
    <input type="checkbox" name="hobby[]" value="code" checked /> 敲代码
    <input type="checkbox" name="hobby[]" value="eat" /> 吃饭
    <input type="checkbox" name="hobby[]" value="dou" /> 打豆豆
    <input type="submit" value="登录" />
  </form>
</body>
```

## 下拉列表

​ 接收选项比较多的情况：籍贯、类型。

> select >option 实现的是单选项，下拉菜单。

> name 属性必选。value 值为必选。

> selected 默认选中项

**html 结构如下：**

```html
<form action="./03-select.php" method="get">
  城市：
  <select name="city">
    <option value="1">上海市</option>
    <option value="2" selected>北京市</option>
    <option value="3">天津市</option>
    <option value="4">西红柿</option>
  </select>
  <input type="submit" value="登录" />
</form>
```

### 数据回显时的默认选中

> 当表单提交到当前页面时，希望可以看到之前用户选中的项

```html
<?php
    //如果传递了城市数据，则获取
    if(isset($_GET['city'])){
        $city=$_GET['city'];
        echo $city; //4
    }
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="./form.css">
    <title>Document</title>
</head>
<body>
        <!--
            action属性如果为空，默认把数据提交到当前页面
            //数据提交到当前页面后，返回的新页面要选中之前选择的那一项
         -->
    <form action="" method="get">
        城市：
        <!-- 根据上面获取的城市的值，设置默认选中项 -->
        <select name="city">
            <option value="1"  <?php echo isset($city)&&$city==1?"selected":"" ?> >上海市
      		</option>
            <option value="2"  <?php echo isset($city)&&$city==2?"selected":"" ?> >北京市
       		</option>
            <option value="3"  <?php echo isset($city)&&$city==3?"selected":"" ?> >天津市
  			</option>
            <option value="4"  <?php echo isset($city)&&$city==4?"selected":"" ?> >西红柿   		   </option>
       </select>
       <input type="submit" value="登录">
    </form>
</body>
</html>
```

转到一个新地址

header('Location: http://www.jbxue.com/');

延迟转向:

header('Refresh: 10; url=http://www.jbxue.com/');
