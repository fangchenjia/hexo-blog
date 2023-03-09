---
title: git基础入门
toc: true
comments: true
tags:
  - git
categories:
  - tool
description:
  - git的基本操作
keywords:
  - git
  - 基本操作
  - 命令
abbrlink: e08524f1
date: 2021-01-19 21:59:24
updated: 2021-01-19 21:59:24
---

# git 基础入门

<!-- more -->

> Git 是一款免费、开源的**分布式** **版本控制系统** ，用于敏捷高效地处理任何或小或大的项目。
>
> Git 是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的版本控制软件。

## git 的安装

[下载地址](https://git-scm.com/download/win)

注意：

1. 不要安装在中文目录
2. 不要使用桌面管理软件

安装很简单，一直下一步即可。在任意的目录下右键，能看到菜单, 就表示安装成功了。

注册码云（远程 git 仓库）账号：

​ 地址： https://gitee.com/signup

## git config 配置

如果是第一次提交，需要配置提交者信息，推荐和 gitee 的账号邮箱一致

```Bash
# git config  user.name 你的目标用户名
# git config  user.email 你的目标邮箱名

# 使用--global参数，配置全局的用户名和邮箱，只需要配置一次即可。推荐配置gitee的用户名和密码
git config  --global user.name Jepson
git config  --global user.email jepsonpp@qq.com

# 查看配置信息
git config --list

# 重置
git config --unset --global user.name
git config --unset --global user.email

```

## git 三个区

要对某个项目使用 git 进行管理，需要使用`git init`命令初始化 git 仓库
`git init`会在当前目录生成一个隐藏文件夹 .git 不要去修改这个文件夹下的任意东西。

git 仓库会分成三个区

工作区：我们书写代码的地方，工作的目录就叫工作区。

暂存区：暂时存储的区域，在 git 中，代码无法直接从工作区提交到仓库区，而是需要先从工作区添加到暂存区，然后才能从暂存区提交到仓库区。暂存区的目的是避免误操作。

本地仓库区：将保存在暂存区域的内容永久转储到 Git 仓库中，生成版本号。生成版本号之后，就可以任何的回退到某一个具体的版本。

## git 基本命令

### git init

- 作用：初始化 git 仓库，想要使用 git 对某个项目进行管理，需要`git init`进行初始化

```bash
# 初始化仓库， 在当前目录下生成一个隐藏文件夹.git
git init
```

### git add

- 作用：将文件由 `工作区` 添加到 `暂存区`，在 git 中，文件无法直接从工作区直接添加到仓库区，必须先从工作区添加到暂存区，再从暂存区添加到仓库区。
- 命令：`git add 文件名/目录名`

```bash
# 将index.html添加到暂存区
git add index.html

# 将css目录下所有的文件添加到暂存区
git add css

# 将当前目录下所有的js文件添加到暂存区
git add *.js

# 添加当前目录下所有的文件
git add .
git add -A
git add --all
```

### git commit

作用：将文件由 暂存区 添加到 仓库区，生成版本号

```bash
# 将文件从暂存区提交到仓库
git commit -m "提交说明"

# 如果不写提交说明，会进入vi编辑器，没有写提交说明，是提交不成功的。
git commit   # 需要使用vi输入内容
# 退出vi编辑器  1-按esc键  2-输入 :q! 按回车即可退出

# 如果是一个已经暂存过的文件，可以快速提交，如果是未暂存的文件，那么命令将不生效。
git commit -a -m '提交说明'

# 修改最近的一次提交说明， 如果提交说明不小心输错了，可以使用这个命令
git commit --amend -m "提交说明"
```

### git status

- 作用：查看文件的状态

- 命令：`git status`
  - 红色表示工作区中的文件需要提交
  - 绿色表示暂存区中的文件需要提交
- 命令：`git stauts -s` 简化日志输出格式

### git log

- 作用：查看提交日志
- `git log` 查看提交的日志
- `git log --oneline` 简洁的日志信息

![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/git%E6%93%8D%E4%BD%9C/git01.png)

## git 对比

### git diff

`git diff`可以查看每次提交的内容的不同

```bash
# 查看工作区与暂存区的不同
git diff

# 查看暂存区与仓库区的不同
git diff --cached

# 查看工作区与仓库区的不同，HEAD表示最新的那次提交
git diff HEAD

# 查看两个版本之间的不同
git diff c265262 de4845b
```

![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/git%E6%93%8D%E4%BD%9C/git02.png)

## git 重置

### git reset

- 作用：版本回退，将代码恢复到已经提交的某一个版本中。
- `git reset --hard 版本号` 将代码回退到某个指定的版本(版本号只要有前几位即可)
- `git reset --hard head~1`将版本回退到上一次提交
  - ~1:上一次提交
  - ~2:上上次提交
  - ~0:当前提交

```bash
关于参数 --hard的解释
git reset 的参数可以是以下三个值：
git reset --soft 版本号  ： 只重置仓库区 （了解）
git reset --mixed 版本号 ： 重置仓库区和暂存区【默认】（了解）
git reset --hard  版本号 ： 重置仓库区和暂存区和工作区。
git reset 版本号         : 效果与--mixed一致
```

- 当使用了`git reset`命令后，版本会回退，使用`git log`只能看到当前版本之前的信息。使用`git reflog`可以查看所有的版本信息

## git 忽视文件

> 在仓库中，有些文件是不想被 git 管理的，比如数据的配置密码、写代码的一些思路等。git 可以通过配置从而达到忽视掉一些文件，这样这些文件就可以不用提交了。

- 在仓库的根目录创建一个`.gitignore`的文件，文件名是固定的。
- 将不需要被 git 管理的文件路径添加到`.gitignore`中

```bash
# 忽视idea.txt文件
idea.txt

# 忽视.gitignore文件
.gitignore

# 忽视css下的index.js文件
css/index.js

# 忽视css下的所有的js文件
css/*.js

# 忽视css下的所有文件
css/*.*
# 忽视css文件夹
css
```

# git 分支操作

分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习 Git 的时候，另一个你正在另一个平行宇宙里努力学习 SVN。

如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，结果，你既学会了 Git 又学会了 SVN！

![](https://myblog-1303177382.cos.ap-chongqing.myqcloud.com/blogpostimg/git%E6%93%8D%E4%BD%9C/fenzhi.png)

## 为什么要有分支？

- 如果你要开发一个新的功能，需要 2 周时间，第一周你只能写 50%代码，如果此时立即提交，代码没写完，不完整的代码会影响到别人无法工作。如果等代码写完再提交，代码很容易丢失，风险很大。
- 有了分支，你就可以创建一个属于自己的分支，别人看不到，也不影响别人，你在自己的分支上工作，提交到自己的分支上，等到功能开发完毕，一次性的合并到原来的分支。这样既安全，又不影响他人工作。

- 分支可以提高 功能开发的独立性

## git 分支命令

### 创建分支

- `git branch 分支名称`创建分支，分支中的代码，在创建时与当前分支的内容完全相同。
- git 在第一次提交时，就有了一个叫`master`的主分支。
- `git branch dev`，创建了一个叫做 dev 的分支

### 查看分支

- `git branch`可以查看所有的分支，
- 在当前分支的前面会有一个`*`
- 在 git 中，有一个特殊指针`HEAD`,永远会指向当前分支

### 切换分支

- `git checkout 分支名称`切换分支 HEAD 指针指向了另一个分支
- 在当前分支的任何操作，都不会影响到其他的分支，除非进行了分支合并
- 提交代码时，会生产版本号，当前分支会指向最新的版本号

### 创建并切换分支

- `git checkout -b 分支名称` 创建并切换分支
- 切换分支会做两件事情
  - 创建一个新分支
  - 把 head 指针指向当前的分支

### 删除分支

- `git branch -d 分支名称` 可以删除分支
- 注意：不能在当前分支删除当前分支，需要切换到其他分支才能删除。
- 注意：`master`分支是可以删除的，但是不推荐那么做。

### 合并分支

- `git merge 分支名称` 将其他分支的内容合并到当前分支。
- 在`master`分支中执行`git merge dev` 将`dev`分支中的代码合并到`master`分支
- [分支合并](https://git-scm.com/book/zh/v1/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6)

## git 合并冲突

- 对于同一个文件，如果有多个分支需要合并时，容易出现冲突。
- 合并分支时，如果出现冲突，只能手动处理，再次提交，一般的作法，把自己的代码放到冲突代码的后面即可。

# git 远程仓库

## gitee（码云）与 git

git 与 gitee 没有直接的关系。

- git 是一个版本控制工具。
- 码云 是一个代码托管平台，开源社区，是 git 的一个远程代码仓库。

```javascript
//1. gitee是一个面向开源及私有软件项目的托管平台，因为只支持git 作为唯一的版本库格式进行托管，故名gitHub。
//2. gitee免费，代码所有人都能看到，但是只有你自己能修改。
```

[gitee 官网](https://gitee.com/)

[开源中国-git](https://git.oschina.net/)

## git clone

- 作用：克隆远程仓库的代码到本地

- git clone [远程仓库地址]

- `git clone git://gitee.com/jepsongithub/test.git`会在本地新建一个`test`文件夹，在 test 中包含了一个`.git`目录，用于保存所有的版本记录，同时 test 文件中还有最新的代码，你可以直接进行后续的开发和使用。

- git 克隆默认会使用远程仓库的项目名字，也可以自己指定。需要是使用以下命令：

  `git clone [远程仓库地址] [本地项目名]`

## git push

- 作用：将本地仓库中代码提交到远程仓库

- `git push 仓库地址 master` 在代码提交到远程仓库

- 例子：`git push git@gitee.com:jepsongithub/test.git master` 如果第一次使用，需要填写 gitee 的用户名和密码

- 完整语法：

  `git push <远程主机名> <本地分支名>:<远程分支名>`

- > 若远程是空仓库，推送是本地仓库不能为空

## git pull

- 作用：将远程的代码下载到本地

- 通常在 push 前，需要先 pull 一次。

- 获取远程仓库的更新，并且与本地的分支进行合并

```bash
git pull
```

将远程主机的某个分支的更新取回，并与本地指定的分支合并，完整格式可表示为：

```
$ git pull <远程主机名> <远程分支名>:<本地分支名>
```

## git remote

每次 push 操作都需要带上远程仓库的地址，非常的麻烦，我们可以给仓库地址设置一个别名

```bash
# 给远程仓库设置一个别名
git remote add 仓库别名 仓库地址
git remote add jepson git@github.com:jepsongithub/test.git

# 删除jepson这个别名
git remote remove jepson

# git clone的仓库默认有一个origin的别名
```

## SSH 免密码登陆

git 支持多种数据传输协议：

- https 协议：`https://github.com/jepsongithub/test.git` 需要输入用户名和密码
- ssh 协议：`git@github.com:jepsongithub/test.git` 可以配置免密码登录

每次 push 或者 pull 代码，如果使用 https 协议，那么都需要输入用户名和密码进行身份的确认，非常麻烦。

- gitee 为了账户的安全，需要对每一次 push 请求都要验证用户的身份，只有合法的用户才可以 push

- 使用 ssh 协议，配置 ssh 免密码，可以做到免密码往 github 推送代码

## SSH 免密码登录配置（了解）

注意：这些命令需要在 bash 中敲

- 1 创建 SSH Key：`ssh-keygen -t rsa`

- 2 在文件路径  `C:\用户\当前用户名\`  找到  `.ssh`  文件夹

- 3 文件夹中有两个文件：

  - 私钥：`id_rsa`
  - 公钥：`id_rsa.pub`

- 4 在  `gitee -> 设置-> SSH 公钥`页面中，新创建 SSH key

- 5 粘贴 公钥  `id_rsa.pub`  内容到对应文本框中

- 5 在 github 中新建仓库或者使用现在仓库，拿到`git@github.com:用户名/仓库名.git`

- 6 此后，再次 SSH 方式与 github“通信”，不用输入密码确认身份了

  ssh-keygen -t rsa 运行后 每台电脑都会生成自己的公钥和私钥

**非对称加密**：

> 非对称加密算法需要两个密钥：公开密钥（publickey）和私有密钥（privatekey）。公开密钥与私有密钥是一对，如果用公开密钥对数据进行加密，只有用对应的私有密钥才能解密；如果用私有密钥对数据进行加密，那么只有用对应的公开密钥才能解密。因为加密和解密使用的是两个不同的密钥，所以这种算法叫作非对称加密算法。 非对称加密算法实现机密信息交换的基本过程是：甲方生成一对密钥并将其中的一把作为公用密钥向其它方公开；得到该公用密钥的乙方使用该密钥对机密信息进行加密后再发送给甲方；甲方再用自己保存的另一把专用密钥对加密后的信息进行解密。

###设置：

git 中文转义处理：

1. 尝试修改 右键 -- `Options` -- `Text` --`Character set` 选中`UTF-8`
   无效
2. 使用`git` 命令 `$ git config --global core.quotepath false`
   有效果
