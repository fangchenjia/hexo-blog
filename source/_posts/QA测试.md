---
title: QA测试
toc: true
comments: true
tags:
  - 测试
categories:
  - 全栈
description:
  - 用js做一些测试
abbrlink: 32bb5ac8
date: 2021-05-12 10:12:30
updated: 2021-05-12 10:12:30
---

# unit 单元测试

<!-- more -->

> 使用 karma 进行测试

- http://karma-runner.github.io/

## 安装及使用

1. 创建一个测试文件夹 unit,并`npm init`
2. 安装 karma

```bash
npm install karma --save-dev
npm install -g karma-cli
```

3. 在 unit 文件夹创建要测试的 index.js

```js
//+1 函数
window.add = function (num) {
  return num == 1 ? 1 : num + 1;
};
```

4. 创建测试脚本 index.spec.js

```js
describe("基本api测试", function () {
  it("+1函数测试", function () {
    //测试+1函数是否符合预期
    expect(window.add(1)).toBe(1);
    expect(window.add(2)).toBe(3);
  });
});
```

5. 在`package.json`中添加脚本

```js
"scripts": {
    "unit": "karma start"
  }
```

6. 生成`karma.conf.js`

```bash
$ karma init

Which testing framework do you want to use?
Press tab to list possible options. Enter to move to the next question.
> jasmine

Do you want to use Require.js?
This will add Require.js plugin.
Press tab to list possible options. Enter to move to the next question.
> no

Do you want to capture a browser automatically?
Press tab to list possible options. Enter empty string to move to the next question.
> PhantomJS
>

What is the location of your source and test files?
You can use glob patterns, eg. "js/*.js" or "test/**/*Spec.js".
Press Enter to move to the next question.
>

Should any of the files included by the previous patterns be excluded?
You can use glob patterns, eg. "**/*.swp".
Press Enter to move to the next question.
>

Do you want Karma to watch all the files and run the tests on change?
Press tab to list possible options.
> no

```

7. 对生成的`karma.conf.js`进行一些修改

```js
files: [
      "./unit/*.js",
      "./unit/*.spec.js"
    ],
browsers: ['PhantomJS'],
singleRun: true
```

8. 运行`npm run unit`
   如图表示测试成功
   ![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/QA%E6%B5%8B%E8%AF%95/unit%E6%B5%8B%E8%AF%951.png)
   然后我们把`index.spec.js`进行一些修改

```js
describe("基本api测试", function () {
  it("+1函数测试", function () {
    //测试+1函数是否符合预期
    expect(window.add(1)).toBe(1);
    expect(window.add(2)).toBe(4); //预期值应该为3而我们设置为4 则会报错
  });
});
```

![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/QA%E6%B5%8B%E8%AF%95/unit%E6%B5%8B%E8%AF%952.png)

## karma-coverage 的使用

> 尝试测试覆盖率以检测测试质量

1. 安装

```
npm install karma karma-coverage --save-dev
```

2. 对`karma.conf.js`进行一些基本的配置

```js
// karma.conf.js
module.exports = function (config) {
  config.set({
    // coverage reporter generates the coverage
    reporters: ["progress", "coverage"],

    preprocessors: {
      // source files, that you wanna generate coverage for
      // do not include tests or libraries
      // (these files will be instrumented by Istanbul)
      "./unit/**/*.js": ["coverage"],
    },

    // optionally, configure the reporter
    coverageReporter: {
      type: "html",
      dir: "./coverage/",
    },
  });
};
```

3. `npm run unit`
   > 此时会生成`coverage`目录
   > ![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/QA%E6%B5%8B%E8%AF%95/coverage.png) > ![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/QA%E6%B5%8B%E8%AF%95/coverage2.png)
   > 打开 index.html 我们可以查看覆盖率
   > ![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/QA%E6%B5%8B%E8%AF%95/coverage3.png)
4. 然后我们把`index.spec.js`进行一些修改

```js
describe("基本api测试", function () {
  it("+1函数测试", function () {
    //测试+1函数是否符合预期
    expect(window.add(1)).toBe(1); //只进行了部分测试 没有考虑到num不为1的情况
  });
});
```

再次`npm run unit`
![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/QA%E6%B5%8B%E8%AF%95/coverage4.png)
点击`index.js`可以查看详情
![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/QA%E6%B5%8B%E8%AF%95/coverage5.png)

# 自动化 e2e 测试

> https://www.npmjs.com/package/selenium-webdriver
> 官网挺详细的，直接参考

# ui 测试

## BackstopJS

> BackstopJS 是一个测试工具，用于测试 ui 图和实际项目是否偏差。

### 1. 首先全局安装 BackstopJS

```
npm install -g backstopjs
```

### 2. 创建一个文件夹，进入该文件夹。

使用 npm init 生成一个 Package.json （可以忽略这步) ，接着使用 backstop init 命令生成一个 backstop 的初始项目

```
backstop init
```

### 3. 这时候根目录会生成一个文件夹叫做 backstop_data 以及一个 backstop.json 的配置文件

### 4. 打开 backstop.json 文件

得到大概如下面图所示的数据

```json
{
  "id": "backstop_default",
  "viewports": [
    {
      "label": "phone",
      "width": 320,
      "height": 480
    },
    {
      "label": "tablet",
      "width": 1024,
      "height": 768
    }
  ],
  "onBeforeScript": "puppet/onBefore.js",
  "onReadyScript": "puppet/onReady.js",
  "scenarios": [
    {
      "label": "BackstopJS Homepage",
      "cookiePath": "backstop_data/engine_scripts/cookies.json",
      "url": "https://garris.github.io/BackstopJS/",
      "referenceUrl": "",
      "readyEvent": "",
      "readySelector": "",
      "delay": 0,
      "hideSelectors": [],
      "removeSelectors": [],
      "hoverSelector": "",
      "clickSelector": "",
      "postInteractionWait": 0,
      "selectors": [],
      "selectorExpansion": true,
      "expect": 0,
      "misMatchThreshold": 0.1,
      "requireSameDimensions": true
    }
  ],
  "paths": {
    "bitmaps_reference": "backstop_data/bitmaps_reference",
    "bitmaps_test": "backstop_data/bitmaps_test",
    "engine_scripts": "backstop_data/engine_scripts",
    "html_report": "backstop_data/html_report",
    "ci_report": "backstop_data/ci_report"
  },
  "report": ["browser"],
  "engine": "puppeteer",
  "engineOptions": {
    "args": ["--no-sandbox"]
  },
  "asyncCaptureLimit": 5,
  "asyncCompareLimit": 50,
  "debug": false,
  "debugWindow": false
}
```

里面的 id 是测试截图的别名，随便取什么名字都行，重要的是配置"viewports"下面环境的尺寸

scenarios[n].label 也是配置别名,这是必须的

scenarios[n].url 您想要测试的端点/文档。它可以是一个绝对 URL，也可以是当前工作目录的本地 URL。

### 5. 添加对比 ui 图

现在还不能测试，因为现在只有测试的真实项目，并没有 ui 对比图，所以现在需要在 backstop_data 里面创建一个文件夹 backstop_reference,在这个里面放入 ui 图片，要和生成的截图命名一样（等等，我不知道最后截图生成的名字是什么，好吧）。

还是在根目录输入命令： `backstop test`

此时 backstop 会开始编译运行，打开一个网页，并会生成截图，对比页面与 ui 图的差异。 这时候因为还没有对比图，因为页面无法比较。但是你此刻会发现 backstop_data 文件夹里面会生成一个测试文件夹 叫做 bitmaps_test。打开里面的文件夹，找到一个你在`backstop.json 配置的id + scenarios.label 命名开头图片`，这就是你需要对比的文件名。 复制这个名字出来。 现在你可以在 bitmaps_reference 文件夹里面 把 ui 设计的图命名为刚才复制的名字了，并且把 bitmaps_test 文件夹全部删除。

### 6.重新使用 backstop test 命令

现在自动打开的网页就会生成对比图片
转载自https://www.cnblogs.com/zzd0916/p/10076552.html
