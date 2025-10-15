---
layout: post
title:  "mysql的基础操作 - 系统变量"
date:  2025-10-15 17:04:47 +0800
categories: mysql
excerpt_image: /assets/dong_man/bai_si.png
author: 双重十月
---

### 一、数据库的含义
```text
MySQL 是一款开源的关系型数据库管理系统（RDBMS），核心功能是高效存储、组织和管理结
构化数据。它通过 SQL（结构化查询语言）实现数据的增删改查，支持多用户并发访问和事务
处理，能保证数据的一致性与安全性；同时具备跨平台特性，可在 Windows、Linux 等系统运
行，广泛用于网站后台、企业级应用等场景，为数据存储和业务逻辑提供稳定支持。
```
[点击跳转MySQL官网](https://www.mysql.com/)
这里不展示安装过程，如有不会自行使用ai工具或者搜索视频教学安装

### 二、设置系统变量
安装成功后直接在<span style="color : red;">命令行</span>中输入MySQL会显示报错
![MySQL报错](/assets/mysql/mysql报错.png)
这是因为没有设置系统变量的原因，导致找不到MySQL这个命令
<br>
***


我们需要找到MySQL的安装位置默认是：<span style="color:red">C:\Program Files\MySQL\MySQL Server 8.0\bin</span> (根据安装情况找)
![MySQL安装位置](/assets/mysql/MySQL位置.png)
找到目录并打开<span style="color:red">bin</span>文件夹，复制<span style="color:red">bin</span>目录位置的绝对路径
<br>
***

接下来要找到系统环境变量把路径添加进去，接下来以Windows10来演示 <span style="color:red">不同的版本可能位置不太一样</span>
打开设置 → 系统 → 系统信息 → 高级系统设置 → 环境变量
![位置](/assets/mysql/系统环境变量设置图片.png)
注意这里有两个变量，一个是<span style="color:red">用户</span>变量，一个是<span style="color:red">系统</span>变量
- <span style="color:red">用户</span>：<span style="color:blue">用户变量是一种存储特定用户配置信息的环境变量，仅对当前登录用户生效，其他用户无法访问。</span>
- <span style="color:red">系统</span>：<span style="color:blue">系统变量和用户不同，系统变量能被所有用户使用</span>

这里我们使用<span style="color:red">系统变量</span>找到系统变量中的<span style="color:red">Path(路径)</span>可以直接双击点进去
![添加变量](/assets/mysql/添加变量.png)
把MySQL的<span style="color:red">bin</span>目录路径添加进去
添加完成后保存关闭所有窗口，重新打开一个命令终端验证是否成功
```
mysql -u root -p
输入密码
```
![验证变量](/assets/mysql/MySQL变量验证.png)
当出现 <span style="color:red">MySQL> </span>时代表着添加成功