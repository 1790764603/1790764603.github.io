---
layout: post
title:  "mysql作业"
date:  2025-06-18 22:42:47 +0800
categories: mysql
excerpt_image: /assets/dong_man/bai_si.png
author: 双重十月
---

### 1、题目要求
##### 创建数据库mydb，并设置为当前数据库
##### 在该数据库中创建名为BJ的班级表，该表中有四个字段分别为:
1. BJH 编号 int
2. BJMC 班级名称 varcahr(20)
3. ZYDM 专业代码 varchar(10)
4. FDY 辅导员 varchar(6)

#### 在该表中插入三行数据：
- 1  网络241   WL123   张三
- 2  网络242   WL123   李四
- 3  软件241   RJ123    王五




### 2、答案与解析
#### （注意事项：windows不区分大小写，Linux必须大写）注意符号和空格，符号全是英文符号，不要使用中文符号

{% highlight SQL %}
create database mydb default charset utf8mb4;  创建数据库并设置字符集utf8mb4   
   
use mydb;      切换到刚刚创建的数据库

create table BJ(          创建一个名为BJ的表，表中有四个字段，
    -> BJH int,
    -> BJMC varchar(20),
    -> ZYDM varchar(10),
    -> FDY varchar(6));


insert into BJ values       插入三条数据
    -> (1, "网络241", "WL123", "张三"),
    -> (2, "网络242", "WL123", "李四"),
    -> (3, "软件241", "RJ123", "王五");


select * from BJ;    查询BJ表中的所有数据
{% endhighlight %}

#### 3.验证图片
![验证结果](/assets/mysql/mysql实操作业1.png)