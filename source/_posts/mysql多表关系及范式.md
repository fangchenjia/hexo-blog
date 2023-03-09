---
title: mysql多表关系及范式
toc: true
mathjax: false
summary: 记录黑马课程的mysql设计笔记
categories: mysql
keywords: mysql 基础 多表关系 范式
tags:
  - mysql
abbrlink: 92291af4
date: 2020-09-23 17:13:37
---

# 数据库的设计

## 1.多表之间的关系

<!--more-->

### 1.分类：

1.  一对一(了解)：
    - 如：人和身份证
    - 分析：一个人只有一个身份证，一个身份证只能对应一个人
2.  一对多(多对一)：
    - 如：部门和员工
    - 分析：一个部门有多个员工，一个员工只能对应一个部门
3.  多对多：
    - 如：学生和课程
    - 分析：一个学生可以选择很多门课程，一个课程也可以被很多学生选择

### 2.实现关系：

1.  一对多(多对一)：
    - 如：部门和员工
    - 实现方式：在多的一方建立外键，指向一的一方的主键。
2.  多对多：
    - 如：学生和课程
    - 实现方式：多对多关系实现需要借助第三张中间表。中间表至少包含两个字段，这两个字段作为第三张表的外键，分别指向两张表的主键
3.  一对一(了解)：
    - 如：人和身份证
    - 实现方式：一对一关系实现，可以在任意一方添加唯一外键指向另一方的主键。

### 3.案例

#### 1. 创建旅游线路分类表 tab_category

```
CREATE TABLE tab_category (
cid INT PRIMARY KEY AUTO_INCREMENT,   ——旅游线路分类主键，自动增长
cname VARCHAR(100) NOT NULL UNIQUE	 ——旅游线路分类名称非空，唯一，字符串 100
    );
```

#### 2.创建旅游线路表 tab_route

```
CREATE TABLE tab_route(
rid INT PRIMARY KEY AUTO_INCREMENT, ——旅游线路主键，自动增长
rname VARCHAR(100) NOT NULL UNIQUE, ——旅游线路名称非空,唯一,字符串 100
price DOUBLE, ——价格
rdate DATE,——上架时间，日期类型
cid INT, ——外键，所属分类
FOREIGN KEY (cid) REFERENCES tab_category(cid)
			);
```

#### 3.创建用户表 tab_user

```
CREATE TABLE tab_user (
uid INT PRIMARY KEY AUTO_INCREMENT, ——用户主键，自增长
username VARCHAR(100) UNIQUE NOT NULL, ——用户名长度 100，唯一，非空
PASSWORD VARCHAR(30) NOT NULL, ——密码长度 30，非空
NAME VARCHAR(100), ——真实姓名长度 100
birthday DATE, ——生日
sex CHAR(1) DEFAULT '男', ——性别，定长字符串 1
telephone VARCHAR(11), ——手机号，字符串 11
email VARCHAR(100) ——邮箱，字符串长度 100
);
```

#### 4.创建收藏表 tab_favorite

```
CREATE TABLE tab_favorite (
rid INT, -- 旅游线路 id，外键
DATE DATETIME, --收藏时间
uid INT, -- 用户id 外键
-- 创建复合主键
PRIMARY KEY(rid,uid), -- 联合主键
FOREIGN KEY (rid) REFERENCES tab_route(rid),
FOREIGN KEY(uid) REFERENCES tab_user(uid)
			);
rid 和 uid 不能重复，设置复合主键，同一个用户不能收藏同一个线路两次
```

## 2.数据库设计的范式

&emsp;&emsp;概念：设计数据库时，需要遵循的一些规范。要遵循后边的范式要求，必须先遵循前边的所有范式要求

&emsp;&emsp;设计关系数据库时，遵从不同的规范要求，设计出合理的关系型数据库，这些不同的规范要求被称为不同的范式，各种范式呈递次规范，越高的范式数据库冗余越小。目前关系数据库有六种范式：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）和第五范式（5NF，又称完美范式）。

分类：

1. 第一范式（1NF）：每一列都是不可分割的原子数据项
2. 第二范式（2NF）：在 1NF 的基础上，非码属性必须完全依赖于码（在 1NF 基础上消除非主属性对主码的部分函数依赖），其中相关几个概念：
   1. 函数依赖：A-->B,如果通过 A 属性(属性组)的值，可以确定唯一 B 属性的值。则称 B 依赖于 A
   - 例如：学号-->姓名。 （学号，课程名称） --> 分数
   2. 完全函数依赖：A-->B， 如果 A 是一个属性组，则 B 属性值得确定需要依赖于 A 属性组中所有的属性值。
   - 例如：（学号，课程名称） --> 分数
   3. 部分函数依赖：A-->B， 如果 A 是一个属性组，则 B 属性值得确定只需要依赖于 A 属性组中某一些值即可。
   - 例如：（学号，课程名称） -- > 姓名
   4. 传递函数依赖：A-->B, B -- >C . 如果通过 A 属性(属性组)的值，可以确定唯一 B 属性的值，在通过 B 属性（属性组）的值可以确定唯一 C 属性的值，则称 C 传递函数依赖于 A
   - 例如：学号-->系名，系名-->系主任
   5. 码：如果在一张表中，一个属性或属性组，被其他所有属性所完全依赖，则称这个属性(属性组)为该表的码
   - 例如：该表中码为：（学号，课程名称）
   6. 主属性：码属性组中的所有属性
   7. 非主属性：除过码属性组的属性
3. 第三范式（3NF）：在 2NF 基础上，任何非主属性不依赖于其它非主属性（在 2NF 基础上消除传递依赖）

---

记录来自黑马课程的笔记
