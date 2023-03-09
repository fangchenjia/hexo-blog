---
title: javascript内置对象
toc: true
categories: JavaScript
keywords: 内置对象 Math Date Array
tags:
  - JavaScript
abbrlink: edaa3ca4
date: 2020-10-20 13:47:43
---
# 内置对象

> JS内置对象就是指Javascript自带的一些对象，供开发者使用，这些对象提供了一些常用的的功能。
>
> 常见的内置对象有Math、String、Array、Date等
<!--more-->
内置对象有很多，我们主要是记下这些内置对象的用法即可。忘了某个方法该如何使用的时候，可以通过以下方式查看。

+ [火狐开发者网站MDN](https://developer.mozilla.org/zh-CN/)
+ [W3School网站](http://www.w3school.com.cn/jsref/jsref_obj_array.asp)


## Math对象

> Math对象中封装很多与数学相关的属性和方法。

+ 属性PI

  `Math.PI`

+ 最大值/最小值

```
  Math.max();
  Math.min();
```

+ 取整（★）

```javascript
Math.ceil();//天花板，向上取整
Math.floor();//地板，向下取整
Math.round();//四舍五入，如果是.5，则取更大的那个数
```

+ 随机数（★）

```javascript
Math.random();//返回一个[0,1)之间的数，能取到0，取不到1
```

+ 绝对值

```javascript
Math.abs();//求绝对值
```

+ 次幂和平方

```javascript
Math.pow(num, power);//求num的power次方
Math.sqrt(num);//对num开平方
```

+ 练习


```javascript

随机生成一个rgb颜色？
function randomRGB(){
  var colorA = parseInt( Math.random() * 256 );
  var colorB = parseInt( Math.random() * 256 );
  var colorC = parseInt( Math.random() * 256 );
  return 'rgb('+ colorA + "," + colorB + ',' + colorC +')';
}
```

## Date对象

> Date对象用来处理日期和时间

+ 创建一个日期对象

```javascript
var date = new Date();//使用构造函数创建一个当前时间的对象
var date = new Date("2017-03-22");//创建一个指定时间的日期对象
var date = new Date("2017-03-22 00:52:34");//创建一个指定时间的日期对象
var date = new Date(2017, 2, 22, 0, 52, 34);
var date = new Date(1523199394644);//参数：毫秒值

Date构造函数的参数
1. 毫秒数 1498099000356		new Date(1498099000356)
2. 日期格式字符串  '2015-5-1'	 new Date('2015-5-1')
3. 年、月、日……				 var date = new Date(2017, 2, 22, 0, 52, 34);月份从0开始
```

+ 日期格式化(了解)

```javascript
date.toString();//默认的日期格式
date.toLocalString();//本地风格的日期格式（兼容性）
date.toDateString();
date.toLocalDateString();
date.toTimeString();
date.toLocalTimeString();
  ```

+ 获取日期的指定部分

```javascript
getMilliseconds();//获取毫秒值
getSeconds();//获取秒
getMinutes();//获取分钟
getHours();//获取小时
getDay();//获取星期，0-6    0：星期天
getDate();//获取日，即当月的第几天
getMonth();//返回月份，注意从0开始计算，0-11
getFullYear();//返回4位的年份  如 2016
```


+ 时间戳

```javascript
var date = +new Date();//1970年01月01日00时00分00秒起至现在的总毫秒数
```


## Array对象

> 数组对象在javascript中非常的常用

+ 数组转换（★）

```javascript
//语法：array.join(separator)
//作用：将数组的值拼接成字符串

var arr = [1,2,3,4,5];
arr.join();//不传参数，默认按【,】进行拼接
arr.join("-");//按【-】进行拼接
```

+ 数组的增删操作（★）

```javascript
array.push();//从后面添加元素，返回新数组的length
array.pop();//从数组的后面删除元素，返回删除的那个元素
array.unshift();//从数组的前面的添加元素，返回新数组的长度
array.shift();//从数组的最前面删除元素，返回删除的那个元素
```

+ 数组的翻转与排序

```
array.reverse();//翻转数组
array.sort();//数组的排序，默认按照字母顺序排序

//sort方法可以传递一个函数作为参数，这个参数用来控制数组如何进行排序
arr.sort(function(a, b){
  //如果返回值>0,则交换位置
  return a - b;
});
```

+ 数组的拼接与截取

```javascript
 //concat：数组合并，不会影响原来的数组，会返回一个新数组。
 var newArray = array.concat(array2);

 //slice:数组切分，复制数组的一部分到一个新数组，并返回这个数组
 //原来的数组不受影响，包含begin，不包含end
 var newArray = array.slice(begin, end);

 //splice:删除数组或者增加数据元素
 //start:开始位置  deleteCount:删除的个数  items:替换的内容
 array.slice(start, deleteCount, [items]);
```

+ 数组查找元素

```javascript
//indexOf方法用来查找数组中某个元素第一次出现的位置，如果找不到，返回-1
array.indexOf(search, [fromIndex]);

//astIndexOf()从后面开始查找数组中元素出现位置,如果找不到，返回-1
array.lastIndexOf(search, [fromIndex]);
```

+ 清空数组

```javascript
//1. array.splice(0,array.leng);//删除数组中所有的元素
//2．array.length = 0;//直接修改数组的长度
//3．array = [];//将数组赋值为一个空数组，推荐
```

## 基本包装类型

> **简单数据类型是没有方法的**。为了方便操作基本数据类型，JavaScript还提供了三个特殊的引用类型：String/Number/Boolean。

基本包装类型：把基本类型包装成复杂类型。

```javascript
var str = “abc”;
var result = str.indexOf(“a”);
//发生了三件事情
1. 把简单类型转换成复杂类型：var s = new String(str);
2. 调用包装类型的indexOf方法：var result = s.indexOf(“a”);
3. 销毁刚刚创建的复杂类型
```

### Number对象

> Number对象是数字的包装类型，数字可以直接使用这些方法

```javascript
toFixed(2)//保留2位小数
toString();//转换成字符串
```

### Boolean对象

> Boolean对象是布尔类型的包装类型。

```javascript
toString( );//转换成字符串
```

**undefined和null没有包装类型，所以调用toString方法会报错**

### String对象

> 字符串可以看成是一个字符数组（伪数组）。因此字符串也有长度，也可以进行遍历。String对象很多方法的名字和和Array的一样。

+ 查找指定字符串

```javascript
//indexOf:获取某个字符串第一次出现的位置，如果没有，返回-1
//lastIndexOf:从后面开始查找第一次出现的位置。如果没有，返回-1
```

+ 去除空白

```javascript
trim();//去除字符串两边的空格，内部空格不会去除
```

+ 大小写转换


```javascript
//toUpperCase：全部转换成大写字母
//toLowerCase：全部转换成小写字母
```

+ 字符串拼接与截取

```javascript
//字符串拼接
//可以用concat，用法与数组一样，但是字符串拼串我们一般都用+

//字符串截取的方法有很多，记得越多，越混乱，因此就记好用的就行
//slice ：从start开始，end结束，并且取不到end。
//substring ：从start开始，end结束，并且取不到end
//substr ： ：从start开始，截取length个字符。
```

+ 字符串切割

```javascript
//split:将字符串分割成数组（很常用）
//功能和数组的join正好相反。
var str = "张三,李四,王五";
var arr = str.split(",");
```

+ 字符串替换

```javascript
replace(searchValue, replaceValue)
//参数：searchValue:需要替换的值    replaceValue:用来替换的值
```



