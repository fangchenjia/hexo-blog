---
title: vue笔记
toc: true
comments: true
tags:
  - vue
categories:
  - JavaScript
description:
  - vue的基本使用
keywords:
  - vue
  - 笔记
  - 黑马
abbrlink: 882edeea
date: 2021-02-11 15:10:49
updated: 2021-02-11 15:10:49
---

## 一 : 介绍

<!-- more -->

1. Vue 基础知识 (指令 + todomvc )

2. Vue 全家桶 ( vue /vue-router / vuex + axios )

3. 组件化开发 : 比较流行的一种开发模式 , 原生 =>模块化 => 组件化

   > 把一个完成的项目划分成一个小小的组件

4. webpack - 前端模块化打包构建工具

## 二 : Vue 介绍

1. [vue 中文网](https://cn.vuejs.org/)
2. [github 下载地址](https://github.com/vuejs/vue)
3. Vue.js (读音 /vju:/ view)
4. 渐进式 JavaScript 框架
   3.1 渐进式 :
   > 小型项目 就可以使用 vue 就高度了
   > 随着页面的复杂程序提高,就要学习 vue-rouer 来管理更多的页面
   > 再随着项目的数据越来越多,管理数据也变得麻烦起来了,就开始使用 vuex 来管理数据

3.2 框架 : 一整套的解决方案

### 框架和库的区别 (面试)

####1. 库(Library) , 代表 : jquery

- 库就是一系列函数的集合, 我们开发人员在使用库的时候,想要完成什么样的功能,就调用库中提供的某个方法

比如 : 想要添加样式, 就调用 jquery 中的 .css() / .addClass()

- 库起到了一个辅助的作用, 在使用库的是时候,是由开发人员说了算, 也是由开发人员起主导作用.

`比如 : 想给 A:设置样式 A.css(), B:addClass() C:style.background='red'`

####2. 框架 (Framework), 代表:vue

- 在使用框架的时候,是由框架说了算,由框架起到了主导作用,
- 框架是一套完整的解决方案,框架中制定了一套规则,使用框架的时候,只需要按照规则,把代码放到合适的地方,然后框架会在合适的时机,主动调用开发人员的代码

比如 : 想用 vue,组件里遍历就得使用 v-for, 下次不用 v-for 了,使用 for 不行 v-for='item in list'

#### 3. 主要区别 : 控制反转

> 也就是 : 谁起到了主导作用

- 使用库的时候 : 开发人员起主导作用
- 使用框架的时候:框架起到了主导作用
- 从体量上看,框架一般比库大
- 会发现使用框架的时候,会受到很多限制

## 三 : MVC + MVVM (面试)

### 第 3.1 MVC

1. MVC 是一种软件架构模式,也有人叫做设计模式
2. M : Model 数据模型 (专门用来操作数据,数据的 CRUD)
3. V : View 视图 (对于前端来说,就是页面)
4. C : Controller 控制器 (是视图和数据模型沟通的桥梁,用于处理业务逻辑)
5. 看图

### 第 3.2 MVVM

> Vue 使用的是 MVVM 模式
> 为什么要学习 MVVM ?

- MVVM ===> M / V / VM
- M : model 数据层
- V : view 视图层
- VM : ViewModel 视图模型
- 核心 : M <===> VM <===> V

### 第 3.3 MVVM 优势

- MVC 模式 将应用程序划为三个部分,实现职责分离
  - 但是,在前端中,经常要通过 js 代码来进行一些逻辑操作,最终还要把这些逻辑操作展示页面中, 也需要`频繁的操作DOM`
  - DOM 是前端性能的瓶颈
  - 比如 : ajax 请求、添加、修改、设置样式、动画
- MVVM 提出来的思想 通过 `数据双向绑定` 让数据自动的双向同步
  - V (修改视图) --> M
  - M (修改数据) --> V

### 第 3.4 Vue 中的 MVVM

- 注意 : 不推荐直接手动操作 DOM
  > 每个人操作 DOM 的方法不一样,会造成性能不一样
  > 官网 : 虽然没有完全遵循 MVVM 模型，但是 Vue 的设计也受到了它的启发。因此在文档中经常会使用 vm (ViewModel 的缩写) 这个变量名表示 Vue 实例。

### 第 3.5 学习 Vue 要转化思想

- 采用的是 : **数据驱动视图**的思想, **数据是核心**
- 以后如果想要操作 DOM, 立马想到的不是应该是拿到元素设置,而是数据

- **数据驱动视图** : 不要再想着怎么操作 DOM, 而是想着如何操作数据

## 四 : 起步 - Hello Vue

### 第 4.1 : 基本使用

1. 安装 : `npm i vue` (小写)
2. 导入 : `<script src='./vue.js'></script>`
3. 实例 vue

```js
// 引入的 vue.js 里 暴露出来一个 构造函数 Vue
const vm = new Vue({
  // 指定 vue 管理的边界
  el: "#app",
  // 提供视图中 需要的数据
  // 视图可以直接使用data中的数据
  data: {
    msg: "xxx",
  },
});
```

### 使用注意点

1. vm 官网建议
2. Vue 构造函数首字母大写
3. 参数是一个对象
4. id='#app', 其他也可以
5. 边界外的无法使用 msg

### 插值表达式

```
1. 解释：使用{{}}（插值表达式）从data中获取数据，并展示在模板中
2. 说明：{{}}中只能出现JavaScript表达式
3. 说明：数据对象的属性值发生了改变，插值处的内容都会更新

- 表达式
  - 运算符 : {{  msg + 500}}
  - 调用方法 : {{ [1,4,7].join('-') }}
  -  三元 :  {{  true ? '真':''假 }}
- 不能使用语句 `if语句 for语句`

```

## 五 : 数据双向绑定演示

## 第 5.1 : 一个 input + v-model

```js
 v-model 指令 : 数据双向绑定的指令
 作用 : 把data中的msg值 和  input上的值 绑定到一起
 注意 : v-model只能用在 表单控件上 (input checkbox 等)
 > 可以在浏览器分别演示 V => M  和 M =>V

```

## 第 5.2 : Object.defineProperty

> 内在-响应式原理

```js
/**
 *
 * 1. vue的数据双向绑定 是通过 `数据劫持` Object.defineProperty() 来实现的  ,
 *     Object.defineProperty()  是 es5 提出来的一个 无法 shim(兼容) 的特性 , 无法兼容ie8以下
 *
 * 2.  Object.defineProperty()  添加/修改属性
 *
 */

let obj = {};
let temp;

obj.name = "zhanhgsan";

// 参数1 : 要给哪个对象设置属性
// 参数2 : 给对象设置什么属性
// 参数3 : 属性的修饰符
Object.defineProperty(obj, "name", {
  set: function (newVal) {
    console.log("赋值了", newVal);
  },
  get: function () {
    console.log("取值了");
    return temp;
  },
});
```

## 第 5.3 : 数据双向绑定的原理简单实现

> 通过数据劫持来实现的

1. `<input type="text" id="txt" />`
2. 演示 : V ==> M

```js
//1. 拿到文本框
const txt = document.getElementById("txt");
//2. 时刻监听txt ,拿到最新的值
txt.oninput = function () {
  console.log(this.value);
  obj.name = this.value;
};

//3. 数据模型
var obj = {};
let temp;

Object.defineProperty(obj, "name", {
  // 给属性赋值的时候会掉
  set: function (newVal) {
    console.log("调用了set", newVal);
    temp = newVal;

    txt.value = newVal;
  },
  get: function () {
    console.log("调用了get");
    return temp;
  },
});
```

3. V => M

```js
//1. 获取 input的值,最新值
//2. 通过监听oninput 拿到最新值
//3. 把最新值赋值给 obj.name
//4. 就会掉了set方法,就会修改了数据
```

4. M => V

```js
//1. obj.name = 'xxx'
//2. 调用 set方法
//3. 把值赋值给input元素
```

## 六 : 指令学习

- 解释：指令 (Directives) 是带有 `v-` 前缀的特殊属性，可以在 html 标签中使用，可以看成特殊的 html 属性
- 作用：指令提供了一些特殊的功能，当指令绑定到标签上时，可以给标签增加一些特殊的行为
- 比如 : v-model v-bind v-if v-for 等等

### 第 6.1 v-model (常用)

> 说明 : 用在`表单`元素中, 用来实现`数据双向绑定` (input checkbox 等等)
> 作用 : 将 `数据txt` 和 `文本框的值` 绑定到一起, 任何一方发生改变,都会引起对方的改变
> 注意 : v-model 在不同类型的表单元素中,该指令的作用不同

```html
<!-- 文本输入框 绑定的是值 -->
<input type="text" v-model="txt" />
<!-- 多选框  绑定的选中状态 -->
<input type="checkbox" v-model="isChecked" />
```

### 第 6.2 v-text 和 v-html

> 说明 : 设置文本内容

```
1. v-text : 相当于之前的 innerText , 设置文本内容(不识别 html 标签) == 标签内部{{}}
2. v-html : 相当于之前的 innerHTML , 设置文本内容(是被 html 标签)
3. 数据
```

```js
   msg1: '<a>这是一条信息</a>',
   msg2: '<a href="#">我也是一条信息</a>'
```

### 第 6.3 v-bind (常用)

> 说明 : 动态绑定数据 (单向)
> 出现原因 : 在 HTML 属性中, 无法使用插值表达式
> 步骤:

```js
// 加载静态数据
 <a href="https://wbaidu.com">aaa</a>
// 想加载动态数据  {{ }}可以获取data中的数据
// 但是 {{}} 不能使用在属性中, 只能出现的标签内容里
<a href="{{ src }}">aaa</a>
// 所以使用v-bind
<a v-bind:href="{{ src }}">aaa</a>   ok
 <img v-bind:src="src">   ok
```

> 缩略 : v-bind 全部省略 只留下一个`:`
> 改为 :

```html
<a :href="src">aaa</a> ok <img :src="src" /> ok
```

> 以后 使用
> 静态加载数据 : `<a href="https://wbaidu.com">aaa</a>`
> 动态加载数据 : `<a :href="href">aaa</a>`

### 第 6.3.1 v-bind 和 v-model 的区别

```html
// v-model : 数据双向绑定 表单元素上 // : : 动态绑定数据(单向)
任意元素动态读取属性 容易出错点 :
<!-- v-model 数据双向绑定 -->
<!--场景 :  表单元素中 -->
<input type="checkbox" v-model="isChecked1" /> <br />
<!--  v-bind 数据动态绑定 (单向) -->
<!--场景 :  主要用在属性中 -->
<input type="checkbox" :checked="isChecked2" />*
```

### 第 6.4 操作样式

1.操作样式

```html
<!-- 1. 静态类名 -->
<h1 class="red">哈哈</h1>

<!-- 2. 动态类名 -->
<h1 :class="cls">哈哈</h1>

<!-- 3. 最常用 -->
<!-- :class 里的值是一个对象 
      键 : 类名 (可能会要,也可以不要)
      值 : 布尔值, true/false 确定类要不要
     -->
<h1 :class="{ red:isRed , fz:isFZ}">哈哈</h1>

<!-- 4. style -->
<h1 :style="{ color : 'red', fontSize : fz + 'px' }">哈哈</h1>
```

2.其他操作

```html
<!-- 1 -->
<!-- 重点 -->
<div :class="{ active: true }"></div>
===>
<div class="active"></div>

<!-- 2 -->
<div :class="['active', 'text-danger']"></div>
===>
<div class="active text-danger"></div>

<!-- 3 -->
<div :class="[{ active: true }, errorClass]"></div>
===>
<div class="active text-danger"></div>

--- style ---
<!-- 1   -->
<h1 :style="{ color : 'red', fontSize : fz + 'px' }">哈哈</h1>
<!--  fz : 80 -->

<!-- 2 将多个 样式对象 应用到一个元素上-->
<!-- baseStyles 和 overridingStyles 都是对象 -->
<!-- 如果有相同的样式，以后面的样式为准 -->
<div :style="[baseStyles, overridingStyles]"></div>
```

### 第 6.5 v-on 指令

> 注册事件/绑定事件

1. v-on:click 绑定了一个单击事件
   > : 后面是事件名称

```html
<button v-on:click="fn">按钮</button>
```

2. 缩写 : @click='fn'
   `<button @click='fn'>按钮</button>`

3. 函数写在 `methods` 里面

```js
fn : function(){ ... }
fn() { ... }
```

4. 函数里面的 this 指的就是 vm 实例

```js
> 在函数里面操作数据
- 获取数据  this.msg
- 修改数据  this.msg = 'XXX'
```

5. 传参
   5.1 正常传参

```js
@click='fn(123)'
```

5.2 事件对象 \$event

```html
<!-- 4.1 绑定事件对象的时候, 没有添加小括号,此时,直接在方法中,通过参数 e 就可以获取到事件对象 -->
<!-- 4.2 如果添加小括号,就拿不到事件对象了,vue留了一个$event -->
<button @click="fn1($event,123)">我是按钮</button>
```

### 6.5 v-for

1.  v-for 指令： 遍历数据，为数据中的每一项生成一个指令所在的标签
2.  代码

```html
<!-- 需求1 : 最常用 遍历数组 -->
<!-- 作用 : 遍历 list1 数据, 为数据中的每一项生成一个li标签 -->
<!-- item 数组里的每一项元素 -->
<ul>
  <li v-for="(item,index) in list1">{{ item }} - {{ index }}</li>
</ul>
<!-- 需求2 : 遍历元素是对象的数组 -->
<ul>
  <li v-for="item in list2">{{ item.name }} - id:{{ item.id }}</li>
</ul>

<!-- 需求3 : 遍历对象 -->
<ul>
  <li v-for="(item,key) in obj">{{ item }}-{{key}}</li>
</ul>

<!-- 需求4 : 想要生成10个h1 -->
<h1 v-for="item in 10">我是h1 {{ item }}</h1>
```

### v-if 和 v-show

1. 代码

2. ```html
   <h1 v-if="isShow">我是h1 v-if</h1>

   <h1 v-show="isShow">我是h1 v-show</h1>
   ```

3. 异同点

4. ```js
   v-if 和 v-show 的异同点

   1. 相同点 : 可以切换元素的显示与隐藏

   2. 不同点 : 切换显示和隐藏的实现不同

       v-if :  显示:创建节点  隐藏: 删除节点

       v-show : 显示: display:block  隐藏 : display:none

   3. 使用场景 :

       v-if因为要不断的创建和删除来切换显示与隐藏 ,所以性能不高

       v-if : 切换次数不频繁的时候,

           v-show : 切换次数频繁的时候

   ```

### 计算属性 computed

> 计算属性其实就是一个属性

- **说明** : 计算属性只跟随相关的数据变化而变化 ,解决底部显示隐藏问题,

- **怎么使用?**

  - 在 computed 里面
  - 写起来像一个方法
  - 用起来像一个属性

- **特点 :**

  - 计算属性一定要有返回值, 返回的值,就会标签要展示的内容

  - 计算属性可以使用 data 里之前已知的值

  - (重要) 只要 计算属性 `相关的数据` 发生了变化,计算属性会 `重新计算`

  - (说一下 :) num1 就是 totalNum 计算属性的相关属性,所以 num1 变了,计算属性会重新计算,

    ​ 但是 num2 不是相关的属性,所以不管你 num2 怎么变,计算属性都不会重新计算

- **注意点 :**

  - 4.1. 一定要有返回值
  - 4.2. 用起来的时候,不能当方法用,因为它本来就是一个属性
  - 4.3. 计算属性(computed 里面的属性) 不能和 data 里的属性重名

- **什么时候使用 计算属性?**

- 根据已知的值,得到一个新值
- 并且 , 新值只想跟相关的数据(已知的值)的变化而变化 (实时更新)

### key

- **说明 :**
  - Vue 中推荐, 在使用 v-for 的时候,添加 key 属性

> 看官网

- 介绍 **就地复用**

```html
<!-- 显示组件 -->
<p v-for="(item,index) in list" :key="index">
  {{ item.name}} <input type="text" />
</p>
<!-- 数据 -->
data: { list : [ { id : 1, name : '老罗' }, { id : 2, name : '涛涛' }, { id : 3,
name : '聪聪' } ]}

<!-- 演示  -->
vm.list.unshift({id:4,name:'马哥'})
```

- 怎么使用 key
  - 如果数组的元素是一个对象 : 使用对象里固定属性,唯一
  - 一般情况下,对象里都有 id, 99%都是取 `item.id`
  - 如果数组的元素是一个简单类型,不是一个对象, 就可以取索引作为 key
  - 语法 : `:key='item.id'`
  - 以后,写了`v-for`之后,立马写好 `:key`

### 其他指令 v-else-if 和 v-else

1. v-else : 两种情况的

```html
<h1 v-if="num > 40">第一个</h1>
<h1 v-else>第三个</h1>
```

2. v-else-if : 三种以上情况

```html
<h1 v-if="num >= 40">第一个</h1>
<h1 v-else-if="num >= 30 && num < 40">第二个</h1>
<h1 v-else>第三个</h1>
```

## 异步 DOM 更新

1. **Vue 中采用了 `异步DOM更新` 的机制**

- 数据发生改变后, vue 没有立即将数据的改变更新到视图中,

- 而是等到数据不再变化的时候 一次性的 将 数据的改变更新到视图中

  ```js
  //1. 验证了
  for (let i = 0; i < 1000; i++) {
    this.count++;
  }
  ```

- 性能的考虑
- 因为对于前端来说, 修改数据进行 DOM 操作是常有的事情,如果频繁操作 DOM,会严重影响页面的加载性能
- DOM 操作这是前端的性能的瓶颈
- 比如 : for (let i = 1; i < 10000; i++>) 如果同步 就要重新渲染 1000 次

4. **验证 异步 DOM 更新 :**

```js
//2. 直接获取data 中的值 ,会立马获取成功
console.log(this.count);
this.count++;
console.log(this.count);

// 但是 通过dom来获取count的值,因为DOM更新这个count值是异步的,是需要一点时间的
console.log(document.querySelector("h1").innerText); // 0
this.count = 100;
console.log(document.querySelector("h1").innerText); // 0
```

5. 需求 : 在数据更新后,立即获取到更新后的内容???>

   > **DOM 更新后,会执行 this.\$nextTick() 的回调函数,所以能拿到值**

```js
// setTimeout(() => {
//      console.log(document.querySelector('h1').innerText)
//   }, 1000)
this.$nextTick(() => {
  console.log(document.querySelector("h1").innerText); // 100
});
```

## 监听 watch

1. **说明** : Vue 中可以通过 **watch** 配置项,来监听 vue 实例中数据的变化

2. **基本使用**

   ```js
   watch: {
       // 监听name属性的数据变化
       // 作用 : 只要name的值发生变化,这个方法就会被调用
       // 第一个参数 : 新值
       // 第二个参数 : 旧值,之前的前
       name(newVal,oldVal){
               console.log('新 :',newVal);
               console.log('旧 :',oldVal);
       }
   }
   ```

3. **基本使用案例 :**
   需求 : 监听用户名文本框字符个数(3-6),并显示格式验证

```html
<input type="text" v-model="name" />
<span v-show="isShow">用户名的字符 在 6-12之间</span> if
(/^[0-9a-zA-Z]{3,6}$/.test(newVal)) { 验证 }
```

4. **监听对象 (数组也属于对象)**

```js
// data :
 data: {
   obj: {
   name: 'zs'
   }
},
// 组件
<input type="text" v-model="obj.name" />
// 监听
```

5. **开始监听对象的属性**

```js
// 从对象的角度来监听的
 因为对象和数组都是引用类型,引用类型变量存的是地址,地址没有变,所以不会触发watch
obj:{
    // 深度监听 属性的变化
    deep:true,
    // 立即处理 进入页面就触发
    immediate: true,
    // 数据发生变化就会调用这个函数
    handler( newVal ) {
      console.log( newVal.name );
     }
  },
 // 从属性的角度来监听
 'obj.name' ( newVal ) {
      console.log('监听对象的属性',newVal);
 }
```

6. 计算属性和 watch 的区别

```js
computed 和 watch的区别
computed :  计算属性
    - 1.根据已知值 ,得到一个新值
        - 2. 新值随着已知值(相关的数据)变化而变化
        1. 计算属性 ==> (得到的是)新值
        2. 计算属性(num)  ==> 是别人影响了我

watch : 监听器
1. 监听 ==> (监听)已知值
2. 监听数据 (num2) => 是我影响到了别人
```

## 生命周期函数

- 所有的 vue 组件,都是 vue 实例, 一个组件对应一个实例,并且接收相同的选项对象(一些根实例特有的选项除外)
- 实例生命周期也叫做 : 组件生命周期
- 组件 :
  - 看做成是一个个可复用的 ui 模块
  - 组件本质上是一个 vue 实例

![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/Vue%E5%AE%9E%E4%BE%8B%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%9B%BE%20-%20%E6%96%B0%E7%89%88.png)

### 生命周期介绍

- 简单说 : 一个组件(实例) 从开始到最后消灭所经历的各种状态,就是一个组件(实例)的生命周期
- 生命周期钩子函数的定义 : 从组件被创建,到组件挂在到页面上运行,再到页面关闭组件被销毁,这三个阶段总是伴随着组件各种的事件,这些事件,统称为组件的生命周期函数 (简称 : 钩子函数)
- 开发人员可以通过 vue 提供的钩子函数,让我们写的代码参与到 vue 的生命周期里面来,让我们的代码在合适的阶段起到相应的作用

#####注意 :

1. 注意 : vue 在执行过程中 会**自动调用** `生命周期钩子函数`, 我们只需要提供这些钩子函数即可
2. 注意 : 钩子函数的名称都是 vue 中**规定好的**

### 5.0 学习 vue 组件生命周期

1. Vue 内部执行的流程(难)
2. 钩子函数如何使用 (两个重要的钩子函数 created mounted)

### 5.1 钩子函数 - beforeCreate

- 说明 : 在实例初始化之前,数据观测 和 event/watcher 事件配置之前被调用

- 组件实例刚被创建,组件属性计算之前, 例如 data 属性 methods 属性

- 注意 : 此时,无法获取 data 中的数据 和 methoids 中的方法

- 场景 : 几乎不用

### 5.2 钩子函数 - created (掌握)

- 说明 : 组件实例创建完成,属性已绑定, 可以调用 methods 中的方法、可以获取 data 值

- **使用场景 : 1-发送 ajax 2-本地存储获取数据**

- ```js
   beforeCreate() {
       // 无法获取数据和事件
       console.warn('beforeCreate', this.msg, this.fn)
   },
   created() {
     console.warn('created', this.msg, this.fn)
   },
  ```

---

### Has 'el' option ?

1. YES => 就是正常的 el 边界
2. NO => 可以注释,但是必须要手动添加 `vm.$mount(el)` 去指定边界

```js
vm.$mount("#app");
```

### Has `template` option?

1. No => 将 el 的 outerHtml 作为模板进行编译 ( outerHTML = 自身 + innerHTML )
2. YES =>

```js
 // 如果提供了 template, 那么 vue 就会将 template 的内容进行编译,编译后,替换页面中 vue 管理的边界
   template : `
      <h1>嘻嘻</h1>
   `,
```

---

### 5.3 钩子函数 - beforeMounted()

- 说明 : 在挂载开始之前被调用 (挂载:可以理解 DOM 渲染)

---

### 5.3 钩子函数 - mounted() (掌握)

- 说明 : 挂载之后, DOM 完成渲染

- **使用场景 : 1-发送 ajax 2-操作 DOM**

- ```js
  记得把template去掉
  // 渲染DOM之前
   beforeMount() {
       // 渲染之前的  <h1 id="h1" @click="fn">{{ msg }}</h1>
     console.log(document.querySelector('h1'))
   },
   // 渲染DOM之后  <h1 id="h1">测试</h1>
   mounted() {
     console.log(document.querySelector('h1'))
   }
  ```

---

### 5.4 钩子函数 - beforeUpdated()

- 说明：数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。你可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。
- 注意：此处获取的数据是更新后的数据，但是获取页面中的 DOM 元素是更新之前的
  > 小提示 : 打印 this.\$el ,打开小三角是之后的,是因为打印是有监听的功能,展示的是后面更改之后的

---

### 5.5 钩子函数 - updated()

- 说明：组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。

- ```js
   beforeUpdate() {
       // 更新之前的值  :  信息
     console.warn('beforeUpdate',document.querySelector('h1').innerText)
   },
   updated() {
       // 更新之后的值 : 信息1111
     console.warn('updated', document.querySelector('h1').innerText)
   }
  ```

---

### 5.6 钩子函数 - beforeDestroy()

- 说明：实例销毁之前调用。在这一步，实例仍然完全可用。
- 使用场景：实例销毁之前，执行清理任务，比如：清除定时器等

```js
  created() {

   this.timerId =   setInterval(() => {
      console.log(1111);

      }, 500);
   },

 // 如果当组件销毁了,还不清除定时器会出现性能问题
 // 在浏览器中可以尝试销毁  vm.$destroy()
 // 最后销毁
beforeDestroy() {
      clearInterval(this.timerId)
 },
```

---

### 5.7 钩子函数 - destroyed()

说明：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

## 过滤器

1. **概念 :**

- vue 中的过滤器(filter) : 数据格式化 ,
- 也就是说,让数据按照我们规定的一种格式输出
- 比如 : 对于日期来说,将日期格式化转化为 `年-月-日 小时:分:秒` 格式的过程

```js
 // 直接显示
 <h1>{{ date  }}</h1>
 显示 :   2019-01-11T10:11:19.566Z
 不是我们想要的
 我们想要的 : 2019-01-11 18-11-53
```

2. **全局过滤器 和 局部过滤器**

- 说明 : 通过**全局方式创建的过滤器**，在任何一个 Vue 实例中都可以使用 (一般情况下,为了项目方便管理,都是一个 vue 实例)
- 注意点: 使用全局过滤器的时候，应该先创建全局过滤器，再创建 Vue 实例
- **局部创建的过滤器** 只能在当前 vue 实例中使用

3. **怎么注册 全局过滤器**

```js
// 第一个参数 : 过滤器的名字
// 第二个参数 : 是一个回调函数,只要使用过滤器的时候,这个回调函数就会执行
///           通过回调函数的返回值得到格式化后的数据
Vue.filter("date", (res) => {
  return "嘻嘻";
});
```

4. **使用过滤器 示例 :**

```js
// 组件
 <h1>时间戳-格式 {{ date2 | date }}</h1>

// js
  Vue.filter('date', res => {
         return `${res.getFullYear()}-${res.getMonth()}-${res.getDate()} ${res.getHours()}:${res.getMinutes()}:${res.getSeconds()}`
      })
```

5. **moment 插件**

- [moment 地址](http://momentjs.cn/)

- 使用

  ```
  1. 安装 : `npm i moment`
  2. 引入 :
  3. 使用
  ```

- 日期 => 指定格式 `moment(res).format('YYYY-MM-DD HH-mm-ss')`

- 时间戳 => 指定格式 `moment(res).format('YYYY-MM-DD HH-mm-ss')`

- ```js
  // 全局
  Vue.filter("date", (res) => {
    return moment(res).format("YYYY-MM-DD HH-mm-ss");
  });
  ```

6. **参数问题**

- 示例

```js
<h1>时间戳-格式 {{ date2 | date('YYYY-MM-DD HH-mm-ss',888) }}</h1>

// 默认值
Vue.filter('date', (res, format = 'YYYY-MM-DD', arg) => {
  console.log(arg)
  return moment(res).format(format)
})
```

7. **局部过滤器**
   > 在 vm 的配置项里写一个 `filters`
   > 对应的是一个对象

```js
 filters: {
    date(res, format = 'YYYY-MM-DD', arg) {
      return moment(res).format(format)
    }
  }
```

## 使用接口的形式发送数据

### 一 : json-server 提供假数据接口

1. **json-server 作用** : 根据指定的 JSON 文件, 提供假数据接口

2. **地址** : [json-server](https://github.com/typicode/json-server)

3. **使用步骤**

   ```js
   1. 全局安装 json-server  : `npm i -g json-server`
   2. 准备一个json数据
   3. 执行 :  `json-server data.json`

   > json数据参考
   json数据可以参考 :
   {
     "todos": [
       {
         "id": 1,
         "name": "吃饭",
         "age": 20
       }
     ]
   }
   ```

4. **REST API 格式**

```js
* 1. 查询 : GET
* 2. 添加 : POST
* 3. 删除 : DELETE
* 4. 更新 : PUT 或者 PATCH(打补丁)
```

5. **具体接口**

```js
* 1. 查询全部数据 http://localhost:3000/todos
*    查询指定数据 http://localhost:3000/todos/2
*
*  2. 添加一个对象 //localhost:3000/todos
*     POST
*     id 会自动帮我们添加
*
* 3. 更新数据 http://localhost:3000/todos/3
*    PUT 或者 PATCH
*    PUT 需要提供该对象的所有数据
*    PATCH 只需要提供要修改的数据即可
*
* 4. 删除数据
*    http://localhost:3000/todos/3
*    DELETE
```

6. **可以借助 `postman` 测试接口;**

## 二 : axios 发送请求 (重点掌握)

> 读音 : /艾克笑丝/

1. **作用** : 一个专门用来发送 ajax 请求的库, 可以在浏览器或者 node.js 中使用

   ```js
   Promise based HTTP client for the browser and node.js
   	以Promise为基础的HTTP客户端，适用于：浏览器和node.js
   	封装ajax，用来发送请求，异步获取数据
   ```

2. **使用步骤**

   ```js
   1. 本地安装 axios : `npm i axios`
   2. 导入 axios
   3. 使用
   ```

3. [axios 使用说明](https://github.com/axios/axios)

4. **GTE 方式发送请求**

   ```js
   // 方式1
   axios.get("http://localhost:3000/todos/3").then((res) => {
     console.log("获取到数据了：", res.data);
   });
   // 方式2
   axios
     .get("http://localhost:3000/menus", {
       params: {
         id: 003,
       },
     })
     .then((res) => {
       console.log("获取到数据了：", res.data);
     });
   ```

   5、 **POST 方式发送请求**

   ```js
        // post 请求
        axios
            // 第一个参数：表示接口地址
            // 第二个参数：表示接口需要的参数
            .post('http://localhost:3000/todos', {
              name: 'axios添加数据',
              done: true
            }).then ( res =>  打印 res)
   ```

## 组件 (重难点)

### 一 : 组件

- 组件可以看作是一些可复用的 ui 模块

  - 小到一个标签 : `<div>哈哈</div>`
  - 大到一个页面 :`<div><div><div><div><div></div></div></div></div></div>`

- 一个组件对应 一个实例

- 组件 === Vue 实例 == new Vue ( options )

- 官网 : 组件是可复用的 Vue 实例

### 二 : 组件化开发

- 概念 :将一个完整的页面,抽离成一个个独立的组件,最终,通过这一个个独立组件完成整个的页面(项目)的功能
- 组件化开发的优势/作用 : 复用

### 三 : 组件的基本使用

> 先注册, 再使用

- **Vue 中的两种注册组件的方法** 1.全局注册 2.局部注册

```
全局组件在所有的vue实例中都可以使用
局部组件在所有的当前实例中可以使用
```

- **注册全局组件 - 基本使用**

```js
/**
 * 第一个参数 : 组件名
 * 第二个参数 : 是一个配置对象, 该配置对象与 Vue 实例的配置对象几乎完全相同
 *        也就是说: vue实例中用到的配置项,和组件中的配置项几乎相同
 */
Vue.component("child", {
  template: `
      <h1 class="red">这是child组件</h1>
      `,
});
```

- **注意点**
  - 注册全局组件也是放到 vm 实例之前
  - 模板只能有一个根节点
  - 组件的配置项和 vue 实例 的配置项一样 (如：data、methods、filters、watch、computed、钩子函数等)
  - 组件的 data 是一个函数 , 并且返回一个对象

```js
// 演示为什么vue在组件中的数据采用函数,而不是对象
// 原因 : 只想让组件复用,不想让数据复用
var Component = function () {};
// 使用对象
Component.prototype.data = {
  demo: 123,
};
// 使用函数
Component.prototype.data = function () {
  return {
    demo: 111,
  };
};
var component1 = new Component();
var component2 = new Component();
component1.data().demo = "8888";
console.log(component2.data().demo); // 456
```

- **使用组件**
  - 当标签一样使用 `<child></child>`

### 组件通讯 (介绍)

> 导入 : 演示子组件访问父组件数据,发现报错

- 组件是一个独立、封闭的个体

  - 也就是说 : 组件中的数据默认情况下, 只能在组件内部使用,无法直接在组件外部使用

  - 可以将 vue 实例看做一个组件

- 对于组件之间需要相互使用彼此的情况,应该使用 **组件通讯 机制**来解决
- 组件通讯的三种情况 :

  1. 父组件将数据传递给子组件(父 -> 子)
  2. 子组件将数据传递给父组件 (子 => 父)
  3. 非父子组件(兄弟组件)

### 父 ==> 子 (重点) 两步

1. 通过属性, 父组件将要传递的数据,传递给子组件

```html
<child :msg="pmsg"></child>
```

2. 子组件通过 props 配置项,来指定要接收的数据

```js
props: ['msg']

// 以后使用
- 组件内 :  msg
- 事件中 : this.msg
```

> **完善 TodoMVC => 完成 传值 + 渲染列表页**

### 子 ==> 父 (重点) 三步

1. 父组件中提供一个方法

```js
pfn(arg) {

    console.log('父组件中接受到子组件传递过来的数据：', arg)
 }
```

2. 通过自定义事件, 父组件将这个方法传递给子组件

```html
// 自定义事件 <child @fn="pfn"></child>
```

3. 子组件调用这个方法（ 触发父组件中传递过来的自定义事件 ）

```js
// 在钩子函数里演示也可以,自己调用
 created() {
    // 调用父组件中的方法 pfn
    // 注意：通过 $emit 方法来触发事件 fn
    // 第一个参数：表示要触发的自定义事件名称，也就是 @fn
    // 第二个参数：表示要传递给父组件的数据
    this.$emit('fn', 'child msg')
}
```

> **完善 TodoMVC => 完成 传值 +添加+ 删除+修改数据+清除完成**

## 目前为止存属性的地方

1. data
2. 计算属性
3. props

## props 的特点 : 只读

- 演示验证 props 只读
- - 传的是简单类型 : 修改会报错
  - 传的复杂类型 (地址) : 修改不会报错,是因为地址没有变 ,测试 `obj={}`立马报错
- 修改`父组件传给子组件的`数据

> 思路 : 把接收过来的数据,保存到 data 中一个临时值 (适用在该组件接收数据只会在当前组件内使用)

```js
Vue.component("child", {
  template: `
      <div>子组件 {{ cmsg }} </div>
       `,
  data() {
    return {
      cmsg: this.msg,
    };
  },
  props: ["msg"],
  created() {
    this.cmsg = 666;
  },
});
```

## prop 的大小写

- 官 : HTML 中的特性名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。
  - html 的标签和 **属性** 都是一样,忽略大小写
  - `<H1 TITLE="哈哈">我是h1</H1>`
- 官 : 这意味着当你使用 DOM 中的模板时，camelCase (驼峰命名法) 的 prop 名不好使了
  - `<child :cMsg="pmsg"></child>` 会报警告,父传子也接收不到了
  - 原因是 : 接收的属性是:cMsg, 因为忽略大小写,已为 : cmsg
  - 所以已经准备要读取的 是 cmsg 的值,否则要报警告
    `You should probably use "c-msg" instead of "cMsg".`
- 方式 1 : 全用小写,不要使用驼峰命名

  - 接收 : `cmsg`
  - props/读取 :`cmsg`

- 方式 2 官 : 需要使用其等价的 kebab-case (短横线分隔命名) 命名： **(推荐)**

  - 接收 : `:c-msg='pmsg'`
  - props/读取 : `cMsg / this.cMsg`

- **大小写在 父传子和 子传父中的应用 (都是要 带 - 的)**

- - 父传子 : ` :c-msg ==> cMsg` 改驼峰 - 因为 props
  - 子传父 : `@todo-head = 'pAddTodo' ==> this.$emit('todo-head')` 不改驼峰

- **完善 TodoMVC : 底部隐藏+剩余完成数+清除完成**

  - 计算属性 : 已知值(todoList 在 根组件) ==> 得到一个新值(子组件里使用)
  - 父 => 子通讯

- 番外篇 : 方法当属性传、传过来的带:得到的原型

## 非父子之间通讯 ( 组件 => 组件 ) (重点)

> 需求 : 组件 jack ===> 恁弄啥哩 ===> 组件 rose

- 是通过 `事件总线 (event bus 公交车) 的机制` 来实现的
- 事件总线 : 实际上就是一个 `空Vue实例`
- 可以实现任意两个组件之间的通讯,而不管两个组件到底有什么样的层级关系
- 看图
- 示例 :

```js
// 第一步 : 事件总线
var bus = new Vue();

// 第二步 : 发送数据   可在点击事件里 触发事件
// 参数1 : 唯一标识  参数2:参数
bus.$emit("todo", "恁弄啥哩?");

// 第三步 : 接收数据    可在 created 里 注册事件
bus.$on("todo", (arg) => {
  console.log("接收过来的", arg);
});
```

## 注册局部组件

- 局部组件只能在当前 vue 实例中使用
- 示例 :

```js
// 注册局部组件：
components: {
  // child表示组件名称
  // 值为配置对象，与 Vue.component 中的第二个参数相同
  // 注意：子组件child属于 Vue实例，因此，只能在 Vue实例的模板中使用
  child: {
    template: `
            <div>这是局部组件 child</div>
          `;
  }
}
```

## 获取组件（获取 DOM 元素） - refs

- 说明 : `vm.$refs` 一个对象, 持有已注册过 ref 的所有子组件 ( HTML 元素)

- 使用 :

  1. 注册

  ```html
  // $refs = { div : div元素, child:child组件 } // 标签
  <div ref="div">哈哈</div>
  // 组件
  <child ref="child"></child>
  ```

  2. 注意 : **mounted** 中使用

  ```js
  // mounted 操作DOM
  * this.$refs.div
  * this.$refs.child

  ```

- 注意点 : 如果获取的是一个子组件,那么通过 ref 就能获取到子组件中的 `data` 和 `methods`

  ```js
  this.$refs.child.num;
  this.$refs.child.fn;
  ```

- 场景 : 一般在第三方的组件中, 可能会用到这个功能

- 示例 :

```html
// 组件
<div ref="div">哈哈</div>
<child ref="child"></child>
// js mounted() { console.log(this.$refs.div) console.log(this.$refs.child.fn) }
```

## 单页面应用程序

- **SPA : Single Page Application 单页面应用程序**

  - MPA : Multiple Page Application 多页面应用程序

- **单页 web 应用**

  就是只有一个 web 页面的应用,
  是加载单个 HTML 页面,
  并在用户与应用程序交互时, 动态更新该页面的 web 应用程序

- **区别**

  - 对于传统的多页面应用程序来说, 每次请求服务器返回的都是一个完整的页面

  - 对于单页应用程序来说,

    只有第一次会加载页面,
    以后的每次请求,
    仅仅是获取必要的数据.然后,
    由页面中 js 解析获取的数据,
    展示在页面中

- **单页面优势 :**
  1. 减少了请求体积，**加快页面响应速度**，降低了对服务器的压力
  2. **更好的用户体验**，让用户在 web app 感受 native app 的流畅, (局部刷新)
- **单页面劣势 :**
  1. **开发成本高** (需要学习路由)
  2. **不利于 SEO**
- 演示 : https://music.163.com/

## 介绍路由

- **路由** : 是浏览器 **URL 中的哈希值**( # hash) 与 **展示视图内容** 之间的对应规则
  - 简单来说,路由就是一套映射规则(一对一的对应规则), 由开发人员制定规则.-
  - 当 URL 中的哈希值( `#` hash) 发生改变后,路由会根据制定好的**规则**, 展示对应的视图内容
- **为什么要学习路由?**
  - 渐进式 =>vue => vuer-router (管理多个页面)
  - 在 web App 中, 经常会出现通过一个页面来展示和管理整个应用的功能.
  - SPA 往往是功能复杂的应用,为了有效管理所有视图内容,前端路由 应运而生.
- **vue 中的路由** : 是 **hash** 和 **component** 的对应关系, **一个哈希值对应一个组件**

## 一 : 路由的基本使用

#### 准备工作 (3 个)

- **安装** : `npm i vue-router`
- **引入** :

```html
<script src="./vue.js"></script>
// 千万注意 :引入路由一定要在引入vue之后,因为vue-router是基于vue工作的
<script src="./node_modules/vue-router/dist/vue-router.js"></script>
```

- **实例路由对象 + 挂载到 vue 上**
  - 实例路由对象 : `const router = new VueRouter()`
  - 挂载到 vue 上 : `new Vue({ router,data,methods })`
  - 验证路由是否挂载成功, 就看打开页面,最后面有没有个 `#/`

#### 具体步骤 (4 个)

- 1.**入口**

- 2.**路由规则**

- 3.**组件**

- 4.**出口**

```js
# 1. 入口
	 // 方式1 : url地址为入口   调试开发用
	 输入url地址 改变哈希值 `01-路由的基本使用.html#/one`
	 // 方式2 : 声明式导航 : router-link+to (见下面介绍)
# 2. 路由规则
// path : 路由路径
// component : 将来要展示的路由组件
routes: [
    { path: '/one', component: One },
    { path: '/two', component: Two }
]
# 3. 组件
// 使用返回值的这个组件名称
const One = Vue.component('one', {
  template: ` <div> 子组件 one </div> `
})
# 4. 出口
<!--  出口 组件要展示的地方-->
<router-view></router-view>

# 总结
拿到入口哈希路径, 根据路由匹配规则,找到对应的组件,显示到对应的出口位置
```

## 二 : 由使用注意事项

- **入口**
  - 最常用的入口 是 **声明式导航 router-link**

```html
<!-- 
router-link 组件最终渲染为 a标签, to属性转化为 a标签的href属性
to 属性的值 , 实际上就是哈希值,将来要参与路由规则中进行与组件匹配
  -->
<router-link to="/one">首页</router-link>
```

- **组件**

```js
const One = {
  template: `<div> 子组件 one </div> `,
};
```

- **演示 : 多个组件匹配**

```js
<div id="app">
  <!-- 1 路由入口：链接导航 -->
  <router-link to="/one">One</router-link>
  <router-link to="/two">Two</router-link>

  <!-- 4 路由出口：用来展示匹配路由视图内容 -->
  <router-view></router-view>
</div>

<!--  导入 vue.js -->
<script src="./vue.js"></script>
<!--  导入 路由文件 -->
<script src="./node_modules/vue-router/dist/vue-router.js"></script>
<script>
  // 3 创建两个组件
  const One ={
    template: '<h1>这是 one 组件</h1>'
  }
  const Two =  {
    template: '<h1>这是 two 组件</h1>'
  }

  // 0 创建路由对象
  const router = new VueRouter({
    // 2. 路由规则
    routes: [
      { path: '/one', component: One },
      { path: '/two', component: Two }
    ]
  })

  const vm = new Vue({
    el: '#app',
    //0. 不要忘记，将路由与vue实例关联到一起！
    router
  })
</script>
```

## 三 : 入口导航菜单高亮处理

- **点击导航 =**> 元素里添加了两个类

```html
<a href="#/one" class="router-link-exact-active router-link-active">One</a>
<a href="#/two" class="">Two</a>
```

- **修改方式 1 : 直接修改类的样式**

```css
.router-link-exact-active,
.router-link-active {
  color: red;
  font-size: 50px;
}
```

- **修改方式 2 : 使用存在过的类样式 => 修改默认高亮类名**

```js
const router = new VueRouter({
  routes: [],
  // 修改默认高亮的a标签的类名
  // red 是已经存在过的
  linkActiveClass: "red",
});
```

### 精确匹配和模糊匹配

- 精确匹配 : router-link-exact-active 类名 : 只有当 `浏览器地址栏中的哈希值 与 router-link 的 to 属性值,完全匹配对,才会添加该类`
- 模糊匹配: router-link-active 类名 : 只要 `浏览器地址栏中的哈希值` 包含 router-link 的 to 属性值,就会添加该类名
- 解决办法 : 加个 exact

```js
<router-link to="/" exact>
  One
</router-link>
```

- 注意 : 精确匹配和模糊匹配，只对添加类名这个机制有效，与路由的匹配规则无关！！！

## 四: 路由配置

### 4.1 动态路由 => 详情列表

> 导入 : 列表三个手机都要点击进去详情页, 只需要一个组件,显示不同的数据即可

```js
# 入口
<router-link to="/detail/1">手机1</router-link>
<router-link to="/detail/2">手机2</router-link>
<router-link to="/detail/3">手机3</router-link>

<router-link to="/detail">手机4</router-link>  没有参数如何????

# 规则
routes: [
  // 2 . 路由规则
  { path: '/detail/:id?', component: Detail }
]

# 获取参数的三种方式
const Detail =  {
    template: `
        // 方式1 : 组件中直接读取
        <div> 显示详情页内容....{{ $route.params.id  }} </div>
    `,
    created() {
        // 方式2 : js直接读取
        // 打印只会打印一次,因为组件是复用的,每次进来钩子函数只会执行一次
        console.log(this.$route.params.id)
    },
    // 方式3 : 监听路由的参数,为什么不需要深度监听,因为一个路径变化,就会对应一个对新的路由对象(地址变)
    watch: {
        $route(to, from) {
            console.log(to.params.id)
        }
    }
}

```

### 4.2 路由对象 - $route

- 一个**路由对象 (route object)**  表示当前激活的路由的状态信息，包含了当前 URL 解析得到的信息

- 一个哈希值路径 ==> 一个路由对象

- **$route.path**

  - 类型: `string`
  - 字符串，对应当前路由的路径，总是解析为绝对路径，如 `"/foo/bar"`。
  - `# 后面?前面的内容`

- **$route.params**

  - 类型: `Object`
  - 一个 key/value 对象，包含了动态片段和全匹配片段，如果没有路由参数，就是一个空对象。
  - 一个 key/value 对象，包含了动态片段和全匹配片段，如果没有路由参数，就是一个空对象。

- **$route.query**

  - 类型: `Object`
  - **参数对象**
  - 一个 key/value 对象，表示 URL 查询参数。例如，对于路径 `/foo?user=1`，则有 `$route.query.user == 1`，如果没有查询参数，则是个空对象。

- **$route.hash**

  - 类型: `string`

    当前路由的 hash 值 (带 `#`) ，如果没有 hash 值，则为空字符串。

- **$route.fullPath**

  - 类型: `string`
  - **全路径**
  - 完成解析后的 URL，包含查询参数和 hash 的完整路径。

```js
# 演示 :
<router-link to="/detail/4?age=21#one">detail</router-link>
{ path: '/detail/:id?', component: detail }
在组件内 created打印 this.$route
> fullPath: "/detail/4?id=001#one"
> hash : "#one"
> params : {id:'4'}
> query : {age : 21}
> path : '/detail/4'
```

### 4.3 嵌套路由 => children

> 导入 : url 测试 parent 和 child, 想让 child 在 parent 中显示

- parent 的内部 添加 : ` <router-view> </router-view>`
- 规则里添加 children
- **/child 和 child 的区别**
  - 如果是`/child` => 那么访问就可以直接访问`#/child`就可以访问 子组件
  - 如果是`child` => 那么访问就应该访问`#/parent/child`才可以访问子组件

```js
const parent = {
  template: `<p>parent  <router-view> </router-view> </p>`,
};
const child = {
  template: `<p>child</p>`,
};

const router = new VueRouter({
  routes: [
    {
      path: "/parent",
      component: parent,
      children: [{ path: "/child", component: child }],
    },
  ],
});
```

### 4.4 命名路由

- 有时候，通过一个名称来标识一个路由显得更方便一些，
- 特别是在**链接一个路由**，或者是执行一些**跳转**的时候。 ===> 场景
- 你可以在创建 Router 实例的时候，在  `routes`  配置中给某个路由设置名称。 ==> 如何命名

```js
# 命名
routes: [
    {
        path: '/parent',
        name: 'parent',
        component: parent
    }
]

# 入口链接 + 跳转  (使用 path 和 name 的转换)
<!-- 方式1 : url手动写 -->

<!-- 方式2 : 入口链接 声明式导航 -->
<router-link to="/parent">点击</router-link>
<router-link :to="{ name : 'parent' }">点击</router-link>  # 忘了 带 : 原始对象类型

<!-- 方式3 : 编程式导航 -->
 fn() {
     // this.$router.push('/parent')
     this.$router.push({
         name: 'parent'
     })
 }
```

### 4.5 命名视图

> 导入 : 有时候想同时 (同级) 展示多个视图，
>
> 需求 : 访问 / 根目录 同时展示以下三个组件

- **三个组件**

```js
const header = {
  template: `<p>header  </p>`,
};
const main = {
  template: `<p>main  </p>`,
};
const footer = {
  template: `<p>footer  </p>`,
};
```

- **规则**

```js
# 以前的那个方式只能显示三个 header
# 演示之前的效果

routes: [
    {
        path: '/',
        components: {
            default: header,
            m: main,
            f: footer
        }
    }
]
```

- **出口**

```html
<router-view> </router-view>
<router-view name="m"> </router-view>
<router-view name="f"> </router-view>
```

### 4.6 重定向

```js
redirect: "/header";
redirect: {
  name: "header";
}
redirect: (to) => {
  // console.log(to)
  return {
    name: "about",
  };
};
```

### 4.7 组件传参

- **原始方式使用 $route 获取**

```js
# 入口
    <router-link to="/header/3">123</router-link>
# 规则
routes: [
    {
        path: '/header/:id',
        component: header,
    }
]
# 获取参数
const header = {
    template: `<p>header  {{ $route.params.id }}  </p>`
}
```

- **布尔模式**

```js
# 入口
    <router-link to="/header/3">123</router-link>

# 规则
routes: [
    {
        path: '/header/:id',
        component: header,
        // 如果 props 被设置为 true，route.params 将会被设置为组件属性
        props: true
    }
]

# 获取参数
const header = {
    // 参数 id 当成参数
    props: ['id'],
    template: `<p>header   {{ id }} </p>`
}
```

- **对象模式**

```js
# 入口
 <router-link to="/header">123</router-link>

# 规则
 routes: [
     {
         path: '/header',
         component: header,
         props: { foo: '0000' }
     }
 ]
# 组件
 const header = {
        props: ['foo'],
        template: `<p>header   {{ foo }} </p>`
 }
```

- **函数模式**

```js
# 同对象模式一样
# 区别是props值不一样
 props: to => {
     return { foo: '0000' }
 }
```

- 注意 : 对象模式和函数模式参数 在 props 里,所以声明式导航那里就不要传参了

## 五 : 路由进阶

### 5.1 元信息

- **规则声明**

```js
routes: [
  {
    path: "/header",
    component: header,
    meta: {
      title: "XXXX",
    },
  },
];
```

- **获取**

```js
 created() {
    document.title = this.$route.meta.title
 }
```

- **作用 :**

- ```
  在路由导航的时候,可以用作判断
  ```

### 5.2 编程式导航

```js
const one = {
  template: ` 
<div> <button @click="handleClick('back')">返回 上一页</button>
<button @click="handleClick('push')">跳转 two页</button>
<button @click="handleClick('replace')">替换 two页</button> 
</div>`,
  methods: {
    handleClick(type) {
      if (type == "back") {
        // 返回
        this.$router.back();
      } else if (type == "push") {
        // 跳转 有历史记录
        this.$router.push("/two");
      } else {
        // 替换 没有历史记录
        this.$router.replace("/two");
      }
    },
  },
};
const two = {
  template: `<p>two </p>`,
};
```

### 5.3 导航守卫

```js
router.beforeEach((to, from, next) => {
    // 访问 login

    if (to.name == 'login') {
        // 下一步
        next()
    } else {
        // 停止跳转
        next(false)
        // 跳转到下一步
        next({ name: 'login' }) 或者 使用路径  next('/login')
    }
})
```
