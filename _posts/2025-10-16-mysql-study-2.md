---
layout: post
title:  "mysql的基础操作 - 连接、创建、查看、删除"
date:  2025-10-15 17:04:47 +0800
categories: mysql
excerpt_image: /assets/dong_man/bai_si.png
author: 双重十月
---
<!-- 此章节学习的是MySQL数据库的创建与删除，讲的不深，都是基础 -->

### 本章节用于入门MySQL，不会讲的深，只是最基础，所有实验均在Windows系统下进行，不区分大小写<br>

### 一、数据库的连接
在第一章文章中，我们设置的MySQL的系统变量，设置了系统变量可以让我们任意开一个命令终端都能直接调用MySQL，在这里我们先学习如何登陆连接MySQL。
连接数据库的基础语法
```SQL
MySQL -u 用户名 -p
```
- <span style="color:red">-u</span>：这个参数可以看作是user(用户)的首字母，对应着输入的用户名<span style="color:red">用户名</span>
- <span style="color:red">-p</span>：这个参数是password(密码)的首字母，对应着后面的参数输入的密码

其实密码在命令行中有两种输入方式
1. 输入完 <span style="color:red">-p</span> 时直接回车输入密码，此时输入的密码是密文的形式
2. 另外一种在输入完<span style="color:red">-p</span> 时不要有空格和回车，在<span style="color:red">-p</span>后面紧挨着写密码，此时输入的密码是以明文的形式输入的

例如我的密码是123456  用户名是root  (root是MySQL自带的一个管理员账户，在装MySQL时输入的密码就是root用户的密码)
```SQL
MySQL -u root -p123456
```

<hr style="border-color: blue;"><br>




### 二、创建数据库语句 <span style="color:red">CREATE DATABASE</span>
用法是：<span style="color:red">CREATE　DATABASE</span>  &nbsp; <span style="color:#165DFF">要创建的数据库名称\;</span>
例如：我现在需要创建一个名为<span style="color:red">MYDB</span>的数据库
```SQL
CREATE DATABASE MYDB;
```
提示：注意<span style="color:red">“ \; ”</span>分号是用来告诉程序这段话到这里结束的，每次输入命令的最后都要加上“分号”表示结束


### 三、查看创建的数据库 <span style="color:red">SHOW DATABASES;</span>
用法：直接输入即可，无需其他参数。(提示：databases和database后面多个s)
```SQL
show databases;
```
可用于查看创建的所有数据库
![图片](/assets/mysql/database-all.png)
以上是作者的所有数据库


### 四、删除所创建的数据库 <span style="color:red">DROP DATABASE/span> <span style="color:blue">MYDB字</span>;
用法：drop是删除的意思，后面跟着的是要删除的数据库名称
```
drop database mydb;
```

删除之后可以再次使用查看命令 <span style="color:red">SHOW DATABASES;</span> 来查看数据库是否被删除
![图片](/assets/mysql/数据库删除后的结果.png)
图片中与上面的图片对比，你们能看出我删除了哪个数据库吗
