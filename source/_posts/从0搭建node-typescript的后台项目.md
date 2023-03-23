---
title: 从0搭建node+typescript的后台项目
date: 2023-03-22 22:03:26
tags:
  - typescript
  - express
categories:
  - node
description:
  - 第一次用ts写后台项目，看了很多博客，记录一下搭建的全过程(〃'▽'〃)!
---

# 初始化项目

直接 npm init -y 初始化项目

```bash
npm init -y 
```



## 配置typescript

安装typescript

```bash
npm i typescript -D
```

安装`@types/node`

 @types/node 是一个TypeScript的声明文件库，提供了node的常用的语法提示。TypeScript并不知道Node.js的内置模块和全局变量的类型，因此需要使用@types/node库提供的声明文件来帮助TypeScript理解这些模块和变量的类型。这样，可以获得更好的代码提示和类型检查。

```bash
npm i @types/node -D
```

创建一个typescript默认配置文件tsconfig.json，[tsconfig.json的详细配置](https://www.tslang.cn/docs/handbook/compiler-options.html)

```bash
npx tsc --init
```

安装`ts-node`

ts-node是一个Node.js的命令行工具，它允许你在运行TypeScript代码时不需要预编译

```bash
npm i ts-node -D
```



## 安装exress

安装`express`,并且安装`@types/express`

`@types/express` 是 TypeScript 对 Express 框架的类型定义文件。它提供了一组类型声明，用于在 TypeScript 中编写 Express 应用程序时进行类型检查和自动补全。

```bash
npm i express -S
npm i @types/express -D
```

## 创建入口文件

创建`src`目录并创建`server.ts`

```ts
import express, { Request, Response } from "express";

const app = express();

app.get("/test", (req: Request, res: Response) => {
	res.json({ msg: "hello world" });
});
console.log("Server is running on port 3000");
app.listen(3000);
```

然后终端运行代码，访问 http://localhost:3000/test ：

```bash
npx ts-node ./src/server.ts
```

## 配置热更新

直接执行并且监听 ts 文件的变化，开发时更加方便

```bash
npm i ts-node-dev -D
```

`ts-node-dev ` 提供了一些常用的应用参数，帮助轻松运行和调试TypeScript应用程序。以下是ts-node-dev常用参数以及它们的作用：

1. `--respawn`：监视文件更改，当文件更改时重启应用程序。

2. `--transpile-only`：只编译TypeScript文件而不检查类型错误。

3. `--ignore-watch`：指定一个逗号分隔的文件或文件夹列表来忽略它们的更改，以避免重启应用程序。

4. `--no-notify`：禁用通知。

5. `--debug`：在运行过程中启用Node.js的调试功能，并在指定的端口或路径处运行调试器。

6. `--inspect-brk`：在应用程序启动时启用调试器，并在代码的第一行暂停应用程序，以便调试器附加到代码。

```bash
# 启动ts-node-dev
npx ts-node-dev --respawn src/server.ts
```

   现在就实现热跟新了。

## 配置eslint

配置`eslint`用于代码规范

```bash
# 安装
npm i -D eslint
# eslint 对 ts 的检验，需要安装ts的eslint插件
npm i @typescript-eslint/eslint-plugin@latest @typescript-eslint/parser@latest -D
```

生成.eslint.js配置文件

```bash
# 初始化eslint  根据自己的需求配置eslint
npx eslint --init
```

下面是我的`eslint`配置

```js
module.exports = {
	"ignorePatterns": [ "node_modules/*", "dist/*", ".eslintrc.js" ],
	"env": {
		"browser": true,
		"es2021": true
	},
	"extends": [
		"eslint:recommended",
		"plugin:@typescript-eslint/recommended"
	],
	"overrides": [
	],
	"parser": "@typescript-eslint/parser",
	"parserOptions": {
		"ecmaVersion": "latest",
		"sourceType": "module"
	},
	"plugins": [
		"@typescript-eslint"
	],
	"rules": {
		"indent": [
			"error",
			"tab"
		],
		"linebreak-style": [
			"error",
			"unix"
		],
		"quotes": [
			"error",
			"double"
		],
		"semi": [
			"error",
			"always"
		]
	}
};
```

## 配置`package.json`的`scripts`

```json
"scripts": {
    "dev": "ts-node-dev --respawn src/server.ts",
    "prod": "npm run build && npm run serve",
    "build": "npm run lint && tsc",
    "serve": "node dist/server.js",
    "lint": "eslint --ext .ts src/"
  }
```
这里要到`tsconfig.json` 添加 `"outDir": "dist"`。
```json
"compilerOptions": {
  "outDir": "dist",
}
```
现在就可以`npm run dev`进行开发了，部署就`npm run prod`。

## 配置环境变量

cross-env和dotenv是两个用于设置环境变量的工具，在Node.js服务中经常用到。它们的作用如下：

1. cross-env：可以跨平台地设置环境变量。因为在不同的操作系统上设置环境变量的方式不同，如果直接使用`NODE_ENV=production`之类的方式设置，可能会出现兼容性问题。而cross-env允许我们使用一致的方式来设置环境变量，无论在哪个操作系统上运行应用程序。

2. dotenv：允许我们从`.env`文件中加载环境变量。我们可以将敏感信息（例如数据库凭据）放在`.env`文件中，并使其不受版本控制。这可以有效地保护我们的应用程序和敏感数据。

安装`cross-env`和`dotenv`

```bash
npm i cross-env dotenv -D
```

修改`package.json`的`scripts`

```json
"scripts": {
    "dev": "cross-env NODE_ENV=development ts-node-dev --respawn src/server.ts",
    "prod": "npm run build && npm run serve",
    "build": "npm run lint && tsc",
    "serve": "cross-env NODE_ENV=production node dist/server.js",
    "lint": "eslint --ext .ts src/"
  }
```

在根目录下新建`.env.prod`和`.env.dev`

```
// .env.prod
ENV_TEST='我是生产的' 
// .env.dev
ENV_TEST='我是开发环境的' 
```

然后在`src`目录下创建`config.ts`

```ts
import dotenv from "dotenv";
dotenv.config({ path: process.env.NODE_ENV === "production" ? ".env.prod" : ".env.dev" });

export default {
	test: process.env.ENV_TEST
};
```

这样我们就可以在`server.ts`里面引入`config.ts`，可以在`config.ts`里面配置比如数据库地址等等数据

比如：

```ts
// 下面是config.ts
import dotenv from "dotenv";
dotenv.config({ path: process.env.NODE_ENV === "production" ? ".env.prod" : ".env.dev" });

export const db = {
  name: process.env.DB_NAME || '',
  host: process.env.DB_HOST || '',
  port: process.env.DB_PORT || '',
  user: process.env.DB_USER || '',
  password: process.env.DB_USER_PWD || '',
  minPoolSize: parseInt(process.env.DB_MIN_POOL_SIZE || '5'),
  maxPoolSize: parseInt(process.env.DB_MAX_POOL_SIZE || '10'),
};
// 下面是.env.dev
DB_NAME=xxx
DB_HOST=xxx
DB_PORT=xxx
...
```

