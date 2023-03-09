---
title: mysql约束
toc: true
mathjax: false
summary: 黑马课程的mysql约束笔记
categories: mysql
keywords: mysql 基础 约束
tags:
  - mysql
abbrlink: 2f5f27c8
date: 2020-09-23 13:33:02
---

# 约束

     概念： 对表中的数据进行限定，保证数据的正确性、有效性和完整性。
     分类：
    	1. 主键约束：primary key
    	2. 非空约束：not null
    	3. 唯一约束：unique
    	4. 外键约束：foreign key

<!--more-->

## 非空约束：not null，某一列的值不能为 null

    	1. 创建表时添加约束
    		CREATE TABLE stu(
    			id INT,
    			NAME VARCHAR(20) NOT NULL -- name为非空
    		);
    	2. 创建表完后，添加非空约束
    		ALTER TABLE stu MODIFY NAME VARCHAR(20) NOT NULL;

    	3. 删除name的非空约束
    		ALTER TABLE stu MODIFY NAME VARCHAR(20);

## 唯一约束：unique，某一列的值不能重复

    	1. 注意：
    		* 唯一约束可以有NULL值，但是只能有一条记录为null
    	2. 在创建表时，添加唯一约束
    		CREATE TABLE stu(
    			id INT,
    			phone_number VARCHAR(20) UNIQUE -- 手机号
    		);
    	3. 删除唯一约束
    		ALTER TABLE stu DROP INDEX phone_number;
    	4. 在表创建完后，添加唯一约束
    		ALTER TABLE stu MODIFY phone_number VARCHAR(20) UNIQUE;

## 主键约束：primary key。

    	1. 注意：
    		1. 含义：非空且唯一
    		2. 一张表只能有一个字段为主键
    		3. 主键就是表中记录的唯一标识

    	2. 在创建表时，添加主键约束
    		create table stu(
    			id int primary key,-- 给id添加主键约束
    			name varchar(20)
    		);

    	3. 删除主键
    		alter table stu modify id int -- 错误  ;
    		ALTER TABLE stu DROP PRIMARY KEY;

    	4. 创建完表后，添加主键
    		ALTER TABLE stu MODIFY id INT PRIMARY KEY;

        5. 自动增长：
    		1.  概念：如果某一列是数值类型的，使用 auto_increment 可以来完成值得自动增长

    		2. 在创建表时，添加主键约束，并且完成主键自增长
    		create table stu(
    			id int primary key auto_increment,-- 给id添加主键约束
    			name varchar(20)
    		);

    		3. 删除自动增长
    		ALTER TABLE stu MODIFY id INT;
    		4. 添加自动增长
    		ALTER TABLE stu MODIFY id INT AUTO_INCREMENT;

## 外键约束：foreign key,让表于表产生关系，从而保证数据的正确性。

### 1. 在创建表时，可以添加外键

    		 语法：
    			create table 表名(
    				....
    				外键列
    				constraint 外键名称 foreign key (外键列名称) references 主表名称(主表列名称)
    			);

例如：在数据库中创建一个部门表 dept，表结构如下表所示。

| 字段名称 | 数据类型    | 备注     |
| -------- | ----------- | -------- |
| id       | INT(11)     | 部门编号 |
| name     | VARCHAR(22) | 部门名称 |
| location | VARCHAR(22) | 部门位置 |

创建 dept 的 SQL 语句:

    CREATE TABLE dept (
    id INT(11) PRIMARY KEY,
    name VARCHAR(22) NOT NULL,
    location VARCHAR(50)
    );

创建数据表 emp，并在表 emp 上创建外键约束，让它的键 deptId 作为外键关联到表 dept 的主键 id，SQL 语句如下：

    CREATE TABLE emp(
    id INT(11) PRIMARY KEY,
    name VARCHAR(25),
    deptId INT(11),
    salary FLOAT,
    CONSTRAINT fk_emp_dept FOREIGN KEY(deptId) REFERENCES dept(id)
    );

在表 emp 上添加了名称为 fk_emp_dept 的外键约束，外键名称为 deptId，其依赖于表 dept 的主键 id。

注意：从表的外键关联的必须是主表的主键，且主键和外键的数据类型必须一致。例如，两者都是 INT 类型，或者都是 CHAR 类型。如果不满足这样的要求，在创建从表时，就会出现“ERROR 1005(HY000): Can't create table”错误。

### 2. 删除外键

    		ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;

### 3. 创建表之后，添加外键

    		ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);



### 4. 级联操作

添加级联操作，语法：

    ALTER TABLE 表名 ADD CONSTRAINT 外键名称
    FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称)
    ON UPDATE CASCADE ON DELETE CASCADE;

分类：

1. 级联更新：ON UPDATE CASCADE
2. 级联删除：ON DELETE CASCADE

以上是来自黑马课程的笔记
