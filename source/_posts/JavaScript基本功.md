---
title: JavaScript基本功
comments: true
tags:
  - JavaScript
categories:
  - JavaScript
description:
  - 作为一名前端基本功不扎实怎么行嘞。
abbrlink: 34ad279a
thumbnail: 'https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/cover%20(1).png'
banner: false
date: 2021-08-28 08:34:39
updated: 2021-08-28 08:34:39
---

<!-- more -->
## 数据类型

### 基本数据类型
基本类型：
字符串`String`、数字`Number`、布尔`Boolean`、空`Null`、未定义`Undefined`、符号`Symbol`、ES11-BigInt`BigInt`
引用数据类型（对象类型）：
对象`Object`、数组`Array`、函数`Function`。还有两个特殊的对象：正则`RegExp`和日期`Date`。

###  数据类型判断

> js 本身就自带一些可以检测数据类型的方法，但各有缺点

#### typeof

> `typeof`可以用于判断`null`以外的基本数据类型，对于引用数据类型均返回`object`,函数返回`function`

```js
/**************** 判断除null以外的基本数据类型 ****************/
console.log(typeof 'xxxx'); //string
console.log(typeof 1); //number
console.log(typeof true); //boolean
console.log(typeof undefined); //undefined
console.log(typeof Symbol()); // symbol
console.log(typeof 10n); // bigint
/**************** null 特殊情况 ****************/
console.log(typeof null); //object
/**************** 引用数据类型 ****************/
console.log(typeof new Number(1)); //object
console.log(typeof []); //object
console.log(typeof function () {}); //function
```

#### instanceof

##### instanceof 的使用

> `instanceof`可以方便检测引用数据类型
> 注意`左侧`如果是`基本数据类型`，直接返回`false`
> 右侧必须是`引用数据类型`，否则报错
```js
/**************基本数据类型*****************/
let num = 1;
num instanceof Number; // false 基本数据类型直接返回false
num = new Number(1); 
num instanceof Number; // true 

null instanceof Object // false

/**************引用数据类型*****************/
let arr = [];
arr instanceof Array; // true
arr instanceof Object; // true

/**************顺便检验校验你对原型链的掌握*****************/
function A() {}
let a = new A();
a instanceof Function; // false
a instanceof Object; // true
A instanceof Function; // true
```
##### instanceof 原理并手写

> 检测某个实例的原型链上是否含有这个类的原型属性

```js
function myInstanceof(left, right) {
  let proto = left.__proto__;
  while (true) {
    if (proto == null) {
      return false;
    }
    if (proto == right.prototype) {
      return true;
    }
    proto = proto.__proto__;
  }
}
```
#### Object.prototype.toString
> 适用于所有数据类型，但需要手动截取判断
> 通过`Object.prototype.toString`然后截取，可以方便获取各种数据的类型

```js
function myTypeof(obj) {
  let res = Object.prototype.toString.call(obj);
  res = res.substring(7, res.length - 1).toLowerCase();
  return res;
}
console.log(myTypeof([])); //array
console.log(myTypeof({})); //object
console.log(myTypeof(1)); //number
console.log(myTypeof(null)); // unll
```

## 手写继承

### 原型链继承(类式继承)

```js
//声明父类
function SupClass() {
  this.superValue = "我是父类";
}
//为父类添加共有方法
SuperClass.prototype.getSuperValue = function () {
  return this.superValue;
};
//声明子类
function SubClass() {
  this.subValue = "我是子类";
}
//继承父类
SubClass.prototype = new SupClass();
//为子类添加共有方法
SubClass.prototype.getSubValue = function () {
  return this.subValue;
};
```

#### 类式继承的缺点

1. 父类中的共有属性如果是引用类型，就会在子类中被所有实例所公用

```js
function SupClass() {
  this.superValue = [1, 2];
}
function SubClass() {}
SubClass.prototype = new SupClass();
let s1 = new SubClass();
let s2 = new SubClass();
console.log(s1.superValue); // [1,2]
s2.superValue.push(3);
console.log(s1.superValue); // [1,2,3]
```

2. 子类实例化的时候无法向父类构造函数传递参数

### 构造函数实现继承

> 解决了引用类型共享问题以及传参问题

```js
//声明父类
function SuperClass(id) {
  this.id = id;
  this.superValue = [1, 2];
}
//为父类添加原型方法
SuperClass.prototype.getSuperValue = function () {
  return this.superValue;
};
//声明子类
function SubClass(id) {
  SuperClass.call(this, id);
}
//创建子类实例
let s1 = new SubClass(11);
let s2 = new SubClass(12);

console.log(s1.superValue); //[1,2]
console.log(s2.superValue); //[1,2]
s1.superValue.push(3);
console.log(s1.superValue); //[1,2,3]
console.log(s2.superValue); //[1,2]
// 构造函数继承的问题
// 父类的原型方法不会被子类继承
s1.getSuperValue(); // Uncaught TypeError: s1.getSuperValue is not a function
```

### 组合继承
> 原型链继承和构造函数继承相结合
```js
//声明父类
function SuperClass(id) {
  this.id = id;
  this.superValue = [1, 2];
}
//父类添加原型方法
SuperClass.prototype.getSuperValue = function () {
  return this.superValue;
};
//声明子类
function SubClass(id, time) {
  SuperClass.call(this, id);
  this.time = time;
}
//类式继承
SubClass.prototype = new SuperClass();
SubClass.prototype.constructor = SubClass;
//子类的原型方法
SubClass.prototype.getTime = function () {
  return this.time;
};

//测试一下
let s1 = new SubClass(1, "2018");
let s2 = new SubClass(2, "2022");

console.log(s1.superValue); //[1,2]
console.log(s2.superValue); //[1,2]
s1.superValue.push(3);
console.log(s1.superValue); //[1,2,3]
console.log(s2.superValue); //[1,2]

console.log(s1.getSuperValue()); //[1,2,3]
console.log(s1.getTime()); //2018
```

> 组合继承已经是相对完善了，但还是存在问题：调用了俩次父类构造函数，第一次是 `new SuperClass()`,第二次是 `SuperClass.call()`,所以需要下面的终极解决方案，寄生式组合继承

### 寄生式组合继承

> 解决方案是不直接`调用父级构造函数`给子类原型赋值,而是通过创建空函数 F 获取父类原型的副本

```js
//组合继承是这样做的
SubClass.prototype = new SuperClass();
SubClass.prototype.constructor = SubClass;
// 寄生式组合继承
function F() {}
F.prototype = SpuerClass.prototype;
let f = new F();  // 这样就不会重复执行父构造函数
f.constructor = SubClass;
SubClass.prototype = f;
//可以进行封装一下
function inheritObject(o) {
  function F() {};
  F.prototype = o;
  return new F();
}
//inheritObject 相当于 Object.create()
function inheritPrototype(subClass, superClass) {
  let p = inheritObject(superClass.prototype);
  p.constructor = subClass;
  subClass.prototype = p;
}
inheritPrototype(subClass, superClass);
// 当然也可以直接这样
SubClass.prototype = Object.create(SuperClass.prototype);
SubClass.prototype.constructor = SubClass;
```

### es6 的 class 实现继承

```js
class SuperClass {
  constructor(id) {
    this.id = id;
  }
  showId() {
    console.log(this.id);
  }
}
class SubClass extends SuperClass {
  constructor(id, time) {
    super(id);
    this.time = time;
  }
}
let s1 = new SubClass(1, 22);
s1.showId(); //1
```

## 函数去重

> 利用数组的 filter 方法去重

```js
function unique(arr) {
  return arr.filter((item, index, array) => {
    return array.indexOf(item) === index;
  });
}

let arr = [1, 1, 1, 1, 3, 4, 2];
console.log(unique(arr)); //[1,3,4,2]
```

> 利用 ES6 中的 Set 方法去重

```js
function unique(arr) {
  return [...new Set(arr)];
  //return Array.from(new Set(arr));
}
let arr = [1, 1, 1, 1, 3, 4, 2];
console.log(unique(arr)); //[1,3,4,2]
```

## 数组扁平化

1. es6 提供的新方法 flat(depth)

```js
let arr = [1, [1, [2, 3]], [2, 4]];
arr.flat(); //[1, 1, [2,3], 2, 4]
arr.flat(Infinity); //[1, 1, 2 ,3 , 2, 4]
```

2. 如果数组的项全为数字，可以使用 join()，toString()

```js
let arr = [1, [1, [2, 3]], [2, 4]];

function flat(arr) {
  //return arr.toString().split(',').map(item=>+item);
  return arr
    .join()
    .split(",")
    .map((item) => +item);
}
flat(arr); //[1, 1, 2, 3, 2, 4]
```

3. 用 reduce 实现数组的 flat 方法

```js
let arr = [1, [2, [3, 4, [5, 6]]], [7, [8, 9, [10, 11]]]];

function flat(arr, deep) {
  if (deep === undefined) {
    deep = 1;
  }
  return arr.reduce((res, cur) => {
    //注意 deep-1 和 --deep的区别 以及 使用concat时 cur 和 [cur] 的区别
    return res.concat(
      Array.isArray(cur) && deep > 0 ? flat(cur, deep - 1) : [cur]
    );
    //下面这行代码也可以
    //return [...res,...(Array.isArray(cur) && deep > 0 ? flat(cur, deep - 1) : [cur])]
  }, []);
}
flat(arr); //[1, 2, Array(3), 7, Array(3)]
flat(arr, 1); //[1, 2, Array(3), 7, Array(3)]
flat(arr, 2); //[1, 2, 3, 4, Array(2), 7, 8, 9, Array(2)]
flat(arr, Infinity); //[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
```

## 手写深拷贝

### 递归的方式实现深拷贝

```js
function deepClone(target) {
  //定义一个返回变量
  let res;
  //如果target是对象如null，array等
  if (typeof target === "object") {
    if (Array.isArray(target)) {
      //target为数组
      res = [];
      for (let i in target) {
        res.push(deepClone(target[i]));
      }
    } else if (target === null) {
      //target为null
      res = null;
    } else if (target.constructor === RegExp) {
      //target为正则对象
      res = target;
    } else {
      // target为普通对象
      res = {};
      for (let item in target) {
        res[item] = deepClone(target[item]);
      }
    }
    //target为基本数据类型或者为函数，直接赋值
  } else {
    res = target;
  }
  //返回结果
  return res;
}
```

测试一下

```js
var testObj = {
  arr: [{ a: 1 }, null, 3],
  obj: {
    name: "zlh",
    age: 100,
  },
  fn: function () {
    console.log("hello");
  },
  reg: /a(b)/,
};

let cloneObj = deepClone(testObj);
testObj.arr = [];
testObj.obj.name = "fcj";
console.log(testObj.arr); //[]
console.log(cloneObj.arr); //[{ a: 1 }, null, 3]
console.log(testObj.obj.name); //fcj
console.log(cloneObj.obj.name); //zlh
```

这样就简单的实现了一个深拷贝，可以进行多级的深拷贝，而且 function，unll 等特殊的值也能全部拷贝成功，修改里边的值也不会有任何问题

###  利用 JSON.stringify()以及 JSON.parse()

> 使用 JSON.stringify()以及 JSON.parse()还是挺简单的，但不可以拷贝 `undefined` ， `function`， `RegExp` 等类型

```js
function clone(target) {
  return JSON.parse(JSON.stringify(target));
}
/*********测试************/
let obj = {
  a: 1,
  b: { a: 1 },
  c: function () {},
  d: /a(b)/
};
let cloneObj = clone(obj);
console.log(cloneObj.c); //undefined
console.log(cloneObj.d); //{}
```

## 观察者与发布订阅者模式

### 1. 观察者模式

> 观察者模式实现的，其实就是当目标对象的某个属性发生了改变，所有依赖着目标对象的观察者都将接到通知，做出相应动作。 所以在目标对象的抽象类里，会保存一个观察者序列。当目标对象的属性发生改变生，会从观察者队列里取观察者调用各自的方法。

```js
//目标对象
class Subject {
  constructor() {
    this.observers = [];
  }
  add(observer) {
    this.observers.push(observer);
  }
  notify(...args) {
    this.observers.forEach((observer) => observer.update(...args));
  }
}
//观察者对象
class Observer {
  constructor(name) {
    this.name = name;
  }
  update(...args) {
    console.log(this.name + "收到信息" + args);
  }
}

// 创建观察者ob1
let ob1 = new Observer("观察者1");
// 创建观察者ob2
let ob2 = new Observer("观察者2");
// 创建目标对象
let sub = new Subject();
// 目标sub添加观察者ob1 （目标和观察者建立了依赖关系）
sub.add(ob1);
// 目标sub添加观察者ob2
sub.add(ob2);
// 目标sub触发事件（目标主动通知观察者）
sub.notify("我更新了");
// 观察者1收到信息我更新了
// 观察者2收到信息我更新了
```

### 2. 发布订阅者模式
   > 发布-订阅是一种消息范式，消息的发送者（称为发布者）不会将消息直接发送给特定的接收者（称为订阅者）。而是将发布的消息分为不同的类别，无需了解哪些订阅者（如果有的话）可能存在。同样的，订阅者可以表达对一个或多个类别的兴趣，只接收感兴趣的消息，无需了解哪些发布者（如果有的话）存在。

```js
class PubSub {
  constructor() {
    this.subscribes = {};
  }
  //订阅
  subscribe(topic, fn) {
    if (!this.subscribes[topic]) {
      this.subscribes[topic] = [fn];
    } else {
      this.subscribes[topic].push(fn);
    }
  }
  //取消订阅
  unSubscribe(topic, fn) {
    if (!this.subscribes[topic] || !fn) {
      return false;
    }
    this.subscribes[topic].forEach((item, index) => {
      if (item == fn) {
        this.subscribes[topic].splice(index, 1);
      }
    });
  }
  //发布
  publish(topic, ...args) {
    let fns = this.subscribes[topic] || [];
    fns.forEach((fn) => fn(...args));
  }
}

let pubSub = new PubSub();
// A订阅了SMS事件（A只关注SMS本身，而不关心谁发布这个事件）
pubSub.subscribe("SMS", (...arg) => {
  console.log("A" + arg);
});
// B订阅了SMS事件
pubSub.subscribe("SMS", (...arg) => {
  console.log("B" + arg);
});
// C发布了SMS事件（C只关注SMS本身，不关心谁订阅了这个事件）
pubSub.publish("SMS", "I published `SMS` event");
```

我的理解：如果只是从意图来看，这俩种模式是一样的，`他们都是实现了对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都将得到通知，并自动更新`,但是从结构上来说的话是不一样的，`发布订阅模式相比观察者模式多了一个中间件订阅器`,在**观察者**模式中，观察者是知道 Subject 的，Subject 一直保持对观察者进行记录。然而，在**发布订阅**模式中，发布者和订阅者**不知道对方的存在**。它们只有通过消息代理进行通信。
