---
title: jQuery源码的简单实现方式
toc: true
comments: true
cover: 'https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/cover%20(2).png'
tags:
  - JavaScript
  - jQuery
categories:
  - JavaScript
description: "jQuery的源码从整体上看,就是执行了一个匿名函数,在这个函数里面,为window绑定了一个$函数"
keywords:
  - jquery
  - 源码
  - 实现
abbrlink: 5ff6a74a
date: 2020-11-23 12:53:51
updated: 2020-11-23 12:53:51
---

# jQuery 最基本的实现


```js
(function (global) {
  var jQuery = function (selector) {
    //工厂模式
    return new jQuery.prototype.init(selector);
  };
  jQuery.fn = jQuery.prototype = {
    init: function (selector) {
    },
  };

  //关键
  jQuery.fn.init.prototype = jQuery.fn; 
  // 相当于 jQuery.fn.init.prototype = jQuery.prototype; 
  // jQuery 没有使用 new 运算符将 jQuery 实例化，而是直接调用其函数
  // 要实现这样,那么jQuery()要返回一个正确的实例-----return new jQuery.prototype.init(selector);
  // 且实例还要能正确访问 jQuery 类原型上的属性与方法
  // jQuery 的方式是通过把 jQuery 的原型传递给jQuery.fn.init.prototype
  // 所以通过这个方法生成的实例的__proto__ 所指向的仍然是 jQuery.fn，所以能正确访问 jQuery 原型上的属性与方法
  
  

  jQuery.extend = jQuery.fn.extend = function () {
    console.log(this);
    var target = arguments[0] || {};
    for (name in target) {
      this[name] = target[name];
    }
    return this;
  };
  //实现的jquery的静态方法
  jQuery.extend({
    aa: function () {
      console.log("aa");
    },
    bb: function () {
      console.log("bb");
    },
  });
  //实现jquery的实例对象的方法
  jQuery.fn.extend({
    cc: function () {
      console.log("cc");
      return this;
    }
  });

  global.$ = global.jQuery = jQuery;
})(window);

$(".aa").cc(); //output  cc  //实例对象上面的方法
$.aa(); //output aa         //jquery函数的静态方法
```


# 学习 jQuery 源码中认为超级巧妙的实现

## 对函数的重载

> 所谓重载，就是一组相同的函数名，有不同个数的参数，在使用时调用一个函数名，传入不同参数，根据参数个数，来决定使用不同的函数！而 js 中并没有重载，因为后定义的函数会覆盖前面的同名函数，但是我们又想实现函数重载该怎么办呢？

1. 简单粗暴，就是函数内部用 switch 语句，根据传入参数的个数调用不同的 case 语句，从而功能上达到重载的效果。这也是我一开始能想到的思路，知道了 jQuery 的实现后，发现这样真的是太粗鲁了，下面是 jQuery 的采用的方法

2. jQuery 的实现：

```js
/*
*	obj 源对象
* name 要重载的方法名
* fn 重载函数
*/
function method(obj, name, fuc) {
  var old = obj[name];
  obj[name] = function () {
    if (arguments.length === fuc.length) {
      return fuc.apply(this, arguments);
    } else if (typeof old === "function") {
      return old.apply(this, arguments);
    }
  };
}
var obj = {};
function fn() {
  console.log("无参数");
  return this.values;
}
function fn1(a) {
  console.log("1个参数",a);
}
function fn2(a,b) {
  console.log("2个参数",a,b);
}
method(obj, "fn", fn);
method(obj, "fn", fn1);
method(obj, "fn", fn2);
console.log(obj.fn()); //无参数
console.log(obj.fn("a")); //一个参数 a
console.log(obj.fn("a", "b")); //两个参数 a b
```

实现过程：我们看一下上面这段代码，最重要的是 method 方法的定义：这个方法中最重要的一点就是这个 old，这个 old 真的很巧妙。它的作用相当于一个指针，指向上一次被调用的 method 函数，这样说可能有点不太懂，我们根据代码来说，js 的解析顺序从上到下为。

1.解析 method（先不管里面的东西）

2.`method(obj,"fn",fn)` 执行这句的时候，它会执行上面定义的方法，`var old = obj[name];`，此时 old 的值为空，因为你还没有定义过这个函数，所以它此时是 undefined，然后继续执行， `obj[name] = function(){...}`，此时obj.fn 已经引用了method里面的方法`function(){...}`，更重要的是该方法还调用了 method 里面的变量`fuc`，形成了闭包

3.好了第一次 method 的调用结束了，开始了第二句，`method(obj,"fn",fn1)` 然后这次使用的时候，又要执行 `old = obj[name]`此时的 `old` 是一个函数，因为上一条语句定义过了，那我这次的 old 实际上指向的是上次定义的方法，它起的作用好像一个指针，指向了上一次定义的 `obj[name]`。然后继续往下解析，又是闭包，还得留着。

4.第三此的 method 调用开始了，同理 old 指向的是上次定义的 obj[name] 同样也还是闭包，还得留着。

第一次：
	old --> undefined     
	obj[name]--> 第一次调用method时的 `function(){...}`

第二次：
	old --> 第一次调用method时的 `function(){...}`     
	obj[name]--> 第二次调用method时的 `function(){...}`

第三次：
	old --> 第二次调用method时的 `function(){...}`
	obj[name]--> 第三次调用method时的 `function(){...}`

5.到这里，内存中实际上有三个 obj[name]，因为三次 method 的内存都没有删除，这就实现了三个函数共存，同时还可以用 old 将它们联系起来

6.我们 `obj.fn` 的时候，就会最先调用最后一次调用 method 时定义的 `function(){...}`，如果参数个数相同 也就是` arguments.length === fuc.length `那么就执行就好了，也不用找别的函数了，如果不相同的话，就找到到 old , `return old.apply(this,arguments);` old 指向的是上次 method 调用时定义的函数，所以我们就去上一次的找，如果找到了，继续执行 arguments.length === fn.length 如果找不到，再次调用 old 继续向上找

总结：运用闭包的原理使三个函数共存于内存中，old 相当于一个指针，指向上一次定义的 function，每次调用的时候，决定是否需要寻找。
