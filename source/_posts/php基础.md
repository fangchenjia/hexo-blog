---
title: php基础
toc: true
comments: true
tags:
  - php
categories:
  - php
description:
  - php的数据类型以及基本语法
keywords:
  - php
  - 数据类型
  - 变量
  - 数组
abbrlink: 68d5e0fd
date: 2020-11-24 12:44:56
updated: 2020-11-24 12:44:56
---

# PHP 基础

<!-- more -->

**PHP 简介**

- 开源（open source）软件，跨平台，常用操作系统稳定执行。Windows / Linux。做 WEB 开发的经典组合  WAMP,LAMP 基本都是开源软件。
<!--more-->
- 入门简单,用户只需要关注应用，开发成本低。

- 支持的大多数主流数据库。MySQL，oracle,Redis 等
  ​
  > 文件以.php 后缀结尾，所有程序包含在`<?php 这里是代码 ?>`
  > 避免使用中文目录和中文文件名
  >
  > php 页面无法直接打开需要运行在服务器环境当中

## 变量

> php 是一门弱类型语法，变量的类型可以随意改变。
> 变量其实就是存储数据的容器

**变量的命名规则**

```php
//1. 不需要关键字进行声明，变量在第一次赋值的时候被创建。
//2. 必须以$符号开始
//3. $后面的命名规则与js的变量命名规则一致。
$name = "zhangsan";
echo $name;
```

### 变量操作

**删除变量**

```php
$var = '666'
unset($var);
```

​ 销毁指定的变量

**判断变量是否为空**

```php
empty($var);
```

​ 判断变量是否为空。PHP 中认为变量的值为：""、0、"0"、NULL、FALSE、[]时，变量虽然赋值了，但是无实际的意义。为空。

## 数据类型

### 简单数据类型

**字符串**

```php
$str = "I'm a String";
echo $str;
```

**整数**

```php
$num = 100;
echo $num;
```

**浮点型**

```php
$float = 11.11;
echo $float;
```

**布尔类型**

```php
$flag = true;
//当布尔类型值为true时，输出1
echo $flag;
$flag = false;
//当布尔类型为false时，输出空字符串
echo $flag;
```

**字符串连接符**

```php
//1. 在php中，+号只有算数的功能，并不能拼串
//2. 在php中，拼串使用.
$name = "mr_Fang";
echo "大家好，我是" . $name . "，今年18岁";
```

**php 中的单引号与双引号**

```php
//1. 字符串的定义可以使用单引号，也可以使用双引号
$name = "mr_Fang";
$desc = '很帅';
//2. 双引号可以解析变量
//3. 单引号的性能会高于双引号（了解）

$name = "mr_Fang";//mr_Fang
echo $name;
$desc = '很帅';
echo $desc;//很帅

$str = '$name 很帅';//$name 很帅
echo $str;

$str = "$name 很帅";//mr_Fang 很帅
echo $str;
```

### 数组

> 在 php 中，数组分为两种，索引数组和关联数组
>
> 计算数组长度的方法： count(数组名);

**索引数组（类似与 JS 中的数组）**

```php
$arr = array("张飞","赵云","马超");
echo $arr;//echo只能打印基本数据类型
echo $arr[0];//张飞
```

**关联数组（类似与 JS 中的对象）**

```php
//属性名必须用引号引起来
$arr = array("name"=>"zhangsan", "age"=>18);
echo $arr["name"];
```

**输出语句**

```php
//1. echo 输出简单数据类型
//2. print_r 输出数据结构，一般用于输出复杂类型。
print_r($arr);//print_r是一个函数，不要忘记小括号
//3. var_dump 输出完整的数据结构，包括类型，一般用于精准调试
var_dump($arr);
```

**二维数组**

> 数组中的每个元素又是一个数组
> 二维数组的存取元素，需要两次访问，依次确定行和列`$arr[x][y]`;

```php
    // 二维数组
    $arr=[
        [1,2,3],
        [4,5,6],
        [7,8,9]
    ];
    // 取值
    echo $arr[2][2]; //9
    // 存储一个人信息

    $info=[
        "name"=>"zs",
        "age"=>100
    ];

    // 存储一个班信息
    $infos=[
        [
            "name"=>"zs",
            "age"=>100
        ],
        [
            "name"=>"ls",
            "age"=>100
        ],
        [
            "name"=>"ww",
            "age"=>100
        ]

    ];
	// 取值
    echo $infos[1]["name"];
```

### 对象

> 在 php 以及其他高级语言中，都有类的概念，表示一类对象，跟 js 中构造函数类似。

```php
//定义一个类（类似js的构造函数）
class Person {
  public $name = "小明";
  public $age = 12;
  private $sex = "男";
}

$zs = new Person;
print_r($zs);//打印对象的结构信息
echo $zs->name;//对象中取值用 ->
echo $zs->age;
echo $zs->sex;//私有属性，无法获取
```

## 语句

### 判断语句

基本上来说，所有语言的 if..else 语法都是一样

### 循环语句

**遍历索引数组**

```php
$arr = array("张三", "李四", "王五", "赵六", "田七", "王八");
//获取数组的长度： count($arr)
for($i = 0; $i < count($arr); $i++) {
  echo $arr[$i];
  echo "<br>";
}
```

**遍历关联数组**

```php
//遍历关联数组
$arr = array(
  "name"=>"zs",
  "age"=>18,
  "sex"=>20
);
foreach($arr as $key => $value) {
  echo $key . "=" . $value . "<br>";
}
```

### 函数

```php
<?php
    header("content-Type:text/html;charset=utf-8");
    //php中函数的语法与js中函数的语法基本一样，不同点在于
    //1. 函数名大小写不敏感
    //2. 函数的参数可以设置默认值
    function sayHello ($name="周杰伦") {
        echo "大家好，我是$name";
        echo "<br>";
    }
    sayHello();//不传参数，会使用默认值
    sayHello("泰勒");//传参数，默认值不生效，和less差不多。
?>
```

## 常量

**常量的定义**

​ 脚本执行周期内，值不会发生改变的量。常量不可以修改及删除。定义为常量可以节省存储空间。英文为：`constant`

**语法**

```php
define(常量名，常量值);
```

```php
define('VERSION','1.2.0'); //常量默认全部字母大写
define('PI',3.1415926);
echo 'PI:',PI;             //使用时直接使用常量名
```

- 常量默认区分大小写。

- 按照开发惯例，常量名推荐全部字母大写。

- 常量不可以重复定义及修改数据。

- 常量值为标量数据类型（整型、浮点型、布尔类型、字符串）。

# PHP 内置函数

### 数学函数

- max(),min() 分别返回一组数的最大值及最小值；

- abs() 返回绝对值。

- floor() 向下取整。

- ceil() 向上取整。

- round() 四舍五入。

- rand()  返回随机数，可以取到两端的值。

### 日期函数

- time() 返回当前的 时间戳(1970 到现在的时间的秒数)

- date(format,time) 格式化一个本地时间或日期

  格式：Y(年) m(月) d(日) H(时) i(分) s 秒

```php
	$time=time();//获取时间戳
	echo date('Y-m-d H:i:s',$time); //格式化时间戳
```

### 字符串函数

- str_replace(查找的值，替换的值，执行替换操作的字符) 字符串替换
- trim(字符串); 去除字符串首尾处的空白字符
- explode(分割符，执行分割的字符串); 使用一个分隔符 分割 一个字符串 返回一个数组
- implode(连接符，执行连接的数组); 将一个一维数组的值拼接为字符串
- substr( 字符串，起始索引，截取长度 );   返回字符串的子串
