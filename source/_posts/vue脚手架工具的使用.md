---
title: vue脚手架工具的使用
toc: true
comments: true
tags:
  - vue
categories:
  - JavaScript
description:
  - vue脚手架工具的使用
keywords: [vue, vue脚手架, 单文件组件, es6模块语法]
abbrlink: e849fe70
date: 2021-02-16 14:05:06
updated: 2021-02-16 14:05:06
---

## 一 : 单文件组件

<!-- more -->

1. 什么是单文件组件 ? 后缀为 .vue 的文件
2. 单文件组件的三个组成部分 (代码块 : scaffold 自动提示)

- template (模板结构)
- script 组件的代码逻辑
- style 样式

3. 注意点 :
   - 单文件组件,无法直接在浏览器中使用,必须经过 webpack 这种打包工具,处理后,才能在浏览器中使用
   - vue-loader 其他配置

## 二 : 脚手架 介绍

> 2.X - 后台管理系统
>
> 3.X - vuex

1. **vue-cli** 是 vue 的脚手架工具

2. **作用 :** vue-cli 提供了一条命令, 我们直接通过这条命令就可以快速的生成一个 vue 项目 (`vue init XX`) 。
   项目的基本结构、以及 webpack 配置项 **全部配置** 好了

3. **为什么会有脚手架工具 ???**

   因为 webpack 配置繁琐, 阻止一批想用 vue 但是不会 webpack 的开发人员,所以作者直接将所有 vue 项目中用到的配置全部帮你写好了,这样,就不需要开发人员再去配置基础 webpack 配置项了

4. 也就是说,使用 vue-cli 这个脚手架工具后,再也不用担心 webpack 配置问题了, 我们前端只需要写 vue 代码, 来实现功能即可

## 三 : 脚手架工具使用

- 安装 : `npm i -g vue-cli`
- 初始化 vue 项目 : `vue init webpack 项目名称`
  - 比如 : `vue init webpack vue-demo01`
- 项目安装过程 :

```js
? Project name # 回车
? Project description # 回车
? Author  # 回车
? Vue build standalone  # => 运行时+编译 => 详见下面的问题1
? Install vue-router? # Yes
? Use ESLint to lint your code? # Yes => 详见下面的问题2
? Pick an ESLint preset Standard  # standard
? Set up unit tests # No
? Setup e2e tests with Nightwatch? # No
? Should we run `npm install` for you after the project has been created? # (recommended) npm
```

- 如何开始

```js
To get started:

cd vue-demo01
npm run dev
```

- `"dev": "webpack-dev-server --inline --progress --config build/webpack.dev.conf.js",`
  - --inline 意思是信息显示在哪里
  - -progress 进度条
  - 指定哪个文件作为 webpack 的配置文件 开发的

## 四 : 文件项目介绍

> 第一遍:文件夹, 第二遍再细化文件

```js
# build - webpack 相关配置

- build.js - 生产环境构建代码
- check-version.js 检查 node、npm 等版本
- util.js 构建工具相关
- vue-loader.config.js vue-loader 的配置文件
- webpack.base.conf.js - webpack 的基础配置
- webpack.dev.conf.js - webpack 开发环境配置
- webpack.prod.conf.js - webpack 发布环境配置

# config - vue 基本配置文件(比如:监听端口(17), 使用 eslint:(26))

- dev.env.js - 开发环境变量
- index.js 项目的一些配置
- prod.env.js 生成环境变量

# node_modules - node 安装的依赖包

# src - 资源文件夹, 以后我们就在这个目录下写代码

- assets - 静态资源 (图片 css 都放在这)
- components - 公用组件
- router - 路由
- App.vue - 项目的根组件
- main.js - 项目的入口文件(总逻辑)

# static - 静态资源不要打包的文件 (图片 json 数据之类的)

- .gitkeep git 保持文件,因为 git 上传,会忽略空文件夹

# .babelrc - babel 配置文件, (es6 语法编译配置,将 es6 转化为浏览器能够识别的代码)

# .editorconfig - 定义代码格式

- charset = utf-8 编码 utf8
- indent_style = space 缩进 空格
- indent_size = 2 缩进字符
- end_of_line = lf 回车作为换行的标记
- insert_final_newline = true 最近一空白行作为结尾
- trim_trailing_whitespace = true 清除最结尾的空白
- 如果使用 ?
- 1. 安装 vscode 的 editorConfig for vscode
- 2. eslint 检测修复后

# .eslintignore - eslint 检测忽略的地方

- /build/
- /config/
- /dist/
- /\*.js 根目录下带.js 的

# .eslintrc.js - eslint 的配置文件

# .gitignore - git 的忽略文件

# .postcssrc.js - css 配置文件 (啥也没有处理)

# index.html - 页面入口

# package.json - 项目配置文件

```

### 4.1 参考 : standard

- [standard 代码规范](https://standardjs.com/readme-zhcn.html)

### 4.2 参考 : src

- assets 静态资源

- components 组件

- App.vue 根组件 => 指定路由出口

  - 脚手架之后,所有的组件都将渲染到 app.vue 中

- app 中的 #app 还是 index.html 中的 #app, app.vue 中的会覆盖前者
  可以通过分别添加 title 属性验证一下

- <router-view/> 路由出口要写在 app.vue 组件模板中

- main.js

  - 入口 js 文件
  - 作用 : 创建 vue 实例,导入其他组件并挂在到 vue 实例上
  - `Vue.config.productionTip = false` 不要打印提示
  - 检测 no new : 见后面的检测警告

  ```js
  new Vue({
    el: "#app", // 目标显示
    router, // 挂载路由
    components: { App }, // 注册组件 App
    template: "<App/>", // 模板显示组件 app
  });
  ```

- route/index.js => 路由

- 一定要记住 :`Vue.use(Router)` 模块化公工程中一定要安装路由插件 .js 就是一个模块

- 官网里 也提到 `https://router.vuejs.org/zh/installation.html`

## 五 : 问题处理

### 5.1 - 问题 1 : 两种编译模式 和 @

> 参考 : vue.js => 安装 => 对不同构建本版本的解释

- 我们选择的是 **Runtime + Compiler** 模式 : ( 运行时 + 编辑器)
- **运行时模式** : 用来创建 Vue 实例、渲染并处理虚拟 DOM 等的代码。基本上就是除去编译器的其它一切。
- **编译器**：用来将模板字符串编译成为 JavaScript 渲染函数的代码。

```js
// 需要编译器
new Vue({
  template: "<div>{{ hi }}</div>",
});

// 不需要编译器
new Vue({
  render(h) {
    return h("div", this.hi);
  },
});
```

- **完整版版本选用** : ES Module (基于构建工具使用) : vue.esm.js
  - build => webpack.base.config.js => 37 行 alias(别名) 'vue$': 'vue/dist/vue.esm.js',
- **@** : 就是 src 的绝对路径
  - build => webpack.base.config.js => 38 行 alias(别名) '@': resolve('src'),

```js
router/index.js =>
	import HelloWorld from '@/components/HelloWorld'
	import HelloWorld from 'C:/users/.../src/components/HelloWorld'
```

### 5.2 - 问题 2 : ESLint

- **概念 :** ESLint 是在 JavaScript 代码中识别和报告模式匹配的工具，它的目标是保证代码的一致性和避免错误。

  - 在 vscode 等编辑工具 中, 可以提示语法错误

  - 在许多方面，它和 JSLint、JSHint 相似，除了少数的例外：

- **如何使用 eslint ?**

  - 1-安装 vscode 插件 ESlint
  - 2-vscode 设置里添加一些配置

  ```js
   "vetur.format.defaultFormatterOptions": {
      "prettier": {
        "semi": false,
        "singleQuote": true,
        "wrap_attributes": "force-aligned"
      }
    },

    // 从这里往下大家都给加上
    "editor.formatOnSave": true, //#每次保存的时候自动格式化
    "eslint.autoFixOnSave": true, // #每次保存的时候将代码按eslint格式进行修复
    "eslint.validate": [
      { "language": "html", "autoFix": true },
      { "language": "vue", "autoFix": true },
      { "language": "javascript", "autoFix": true }
    ],
    "prettier.eslintIntegration": true, // #让prettier使用eslint的代码格式进行校验
    "prettier.semi": false, //#去掉代码结尾的分号
    "prettier.singleQuote": true, //#使用带引号替代双引号
    "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
    "editor.formatOnType": true, //#让函数(名)和后面的括号之间加个空格
    "vetur.format.defaultFormatter.html": "js-beautify-html",
    "vetur.format.defaultFormatter.js": "vscode-typescript"
  ```

- **关闭 Eslint :**

  - 参考 : config/index.js ==> 26 行 : `dev.useEslint ` 设置为 false
  - 重启项目: `npm run dev`

### 5.3 问题 3 : vscode 安装 格式化插件 Prettier

- **安装** vscode 插件 `Prettier -Code formatter`

- **功能 1** : shift + alt + F => 格式化代码
- **功能 2** : 配合 eslint : 见上一个问题的配置

### 5.4 问题 4 : 检测警告

```js
eslint-disable-next-line # 忽略检测下一行  可以使用单行注释/多行注释,其他都是多行注释
eslint-disable # 忽略当前整个文件  多行注释   /*    */

eslint-disable no-new # 忽略前面是new开头
```

## 六 : ES6 的模块语法 (基于 webpack 基类演示)

##### 6.1 : export default 默认导出一个模块 ( 简单类型 + 复杂类型 )

- **导出 : export default**

- > 默认 只能导出一个

  ```js
  let str = "abc";
  let num = 20;
  let obj = { name: "zs" };

  export default num;
  // export default obj
  ```

- **导入 : import**

- > 导入的名字可以任意

- ```js
  import res from "./a.js";
  console.log(res);
  ```

#### 6.2 export 导出多个模块, 都放在一个对象里

- **导出 : export **

- ```js
  // 逻辑模块
  // 登录一个函数
  export let login = () => {
    console.log("登录");
  };
  // 注册一个函数
  export let register = () => {
    console.log("注册");
  };
  ```

- **导入 : import**

- ```js
  // 方式1
  import * as res from "./a";
  console.log(res);
  res.login();
  res.register();
  // 方式2
  import { login, register as reg } from "./a";
  login();
  register();
  ```

#### 6.3 import 模块

```js
import axios from "axios";
```
