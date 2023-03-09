---
title: php操作数据库
toc: true
comments: true
tags:
  - php
  - mysql
categories:
  - php
description:
  - PHP操作数据库常用API
abbrlink: 42bd3837
date: 2020-12-14 11:20:52
updated: 2020-12-14 11:20:52
---

# PHP 操作数据库

<!-- more -->

## **连接数据库基本步骤**

1-连接数据库
2-准备 sql 语句
3-执行 sql 语句
4-获取执行的结果并分析
5-释放并关闭数据库

## **操作数据库常用 API**

- mysqli_connect(IP,用户名，密码，数据库名) 连接数据库
- mysqli_query($link,$sql) 执 SQL 语句
- mysqi_error($link); 返回最近调用函数的错误描述
- mysql_close($link) 关闭连接
- mysqli_fetch_assoc($res) 以关联数组的形式范湖数据
- mysqli_num_rows(resource $res); 返回结果集的行数

## sql 操作注意事项：

- 使用 PHP 发送 SQL 语句前，可以先打印 SQL 语句，检查语句的正确性。

- 使用变量拼接 SQL 语句时，字段为字符串类型，需要在变量的两侧使用单、双引号包裹。可以将所有的字段外面都使用双引号包含。

```php
    //常用方法
      //mysqli_connect('ip地址','用户名','密码','数据库名称');
      //如果成功返回 数据库连接
      //如果失败返回 false

      //die('文本');  终止程序的执行

      //mysqli_query(数据库连接,要执行的sql语句);
      //成功 返回 true
      //失败 返回 false

      //mysqli_close(数据库连接); 关闭数据库的连接
      //mysqli_error(数据库的连接)； 输出数据库最近一次执行错误信息

     //@ 抑制错误
     //1-连接数据库
     @$link= mysqli_connect('127.0.0.1','root','','test1');
    // 如果出错 给用户提示
     if(!$link){
         //如果数据库连接失败，后面代码直接结束
         die('数据库连接失败！');
     }

    //2-操作数据
     //2-1 准备好sql语句（删除）
     $id=14;
     //双引号可以解析变量
     $sql="delete from stu1 where icd=$id";

     //2-2 让数据库执行sql语句
     if(mysqli_query($link,$sql)){
         echo '删除成功！';
     }else{
        echo '<br/>';
         //输出数据库最近一次执行错误
         echo mysqli_error($link);
     }

     //关闭数据库连接
     mysqli_close($link);
```

## 非查询(增删改)和查询语句（select）的区别

通过 mysqli_query()函数，来执行 sql 语句，操作数据库

- 执行的是非查询 sql 语句时，mysqli_query()执行成功返回 true,失败返回 false 作为标识

- 而执行查询的 sql 语句是，mysqli_query()执行成功，返回查询数据的结果集（二维数组），失败返回 false，我们拿到数据库中返回的数据进行渲染处理;
  **查询数据逻辑如下**

  ```php
      //操作数据的基本步骤：
      //1-连接数据库
      //2-准备sql语句
      //3-操作数据（对数据库进行增删改查）
      //4-获取执行结果
      //5-关闭数据连接

       //1-连接数据库
       @$link=mysqli_connect('127.0.0.1','root','','test1');
       if(!$link){
           die('数据库连接失败!');
       }

       //进行查询炒作
       $sql="select * from stu1";

       //执行sql
       // 如果 mysqi_query 执行的是查询语句
       // 查询成功 返回的 查询到的数据的结果集
       // 查询失败 返回 false
       $res=mysqli_query($link,$sql);

      //如果获取到数据 把数据保存到php中，然后传给前端
      //当查询结果不为false并且数据行数大于0行 进行保存
      //mysqli_num_rows($res);//获取结果集的行数
       if(!$res || mysqli_num_rows($res)==0 ){
           die('未获取到数据！');
       }

       //对数据进行保存
       //获取结果集中的数据
       // mysqli_fetch_assoc($res); 返回的是一个关联数组 一次取一条数据
      while($row=mysqli_fetch_assoc($res)){
          $arr[]=$row; //把每次获取的一行的关联数组的数据 放到$arr数组
      }

      mysqli_close($link);
  ```

## 数据库工具函数的封装

> 为了提高代码的复用性，把数据增删改的操作封装成一个方法

> 封装公共代码部分，变换的部分提取成参

```php
      //定义常量 存储数据库基本信息
      define('HOST','127.0.0.1');
      define('UNAME','root');
      define('PWD','');
      define('DB','test1');
      //非查询功能
      function my_exec($sql){
          //1-连接数据库
          @$link=mysqli_connect(HOST,UNAME,PWD,DB);
          //判断
          if(!$link){
              die('数据库连接失败！');
          }
          //2-执行sql语句，判断执行结果
          if(!mysqli_query($link,$sql)){
              //如果失败输出错误信息
              echo  '操作失败！'.mysqli_error($link);
          }
          //3-关闭连接
          mysqli_close($link);
      }

      //查询功能
      function my_query($sql){
          //1-连接数据库
          @$link=mysqli_connect(HOST,UNAME,PWD,DB);
          //判断连接
          if(!$link){
              echo '数据库连接失败！';
              return false;
          }

          //执行查询
          $res=mysqli_query($link,$sql);
          //判断是否有数据
          if(!$res || mysqli_num_rows($res)==0 ){
              echo '未获取到数据！';
              //关闭连接
              mysqli_close($link);
              return false;
          }
          //保存数据 二维数组的形式
          //获取结果集中所有的数据
          while($row=mysqli_fetch_assoc($res)){
              $arr[]=$row;
          }
          //关闭连接
          mysqli_close($link);
          //返回数据库的数据
          return $arr;

      }
```
