---
layout: post
title:  "HUAWEI数通作业10-ACL实验"
date:  2025-11-12 17:04:47 +0800
categories: HUAWEI-ENSP
excerpt_image: /assets/dong_man/碧蓝档案优香.jpg
author: 双重十月
---

### 题目要求
!["图片"](/assets/HUAWEI/huawei作业10ACL实验.png)
完成图片中的要求


### PC机与网关
这里需要配置一个server1即可，其余的老师均配置好了
下面是server1配置FTP服务的步骤
!["图片"](/assets/HUAWEI/华为作业10ACL配图1.png)
根据图中步骤随便选一个文件夹即可

### PC1-内部员工工作区
- 基础配置
```bash
system-view 
undo info-center enable
```

- IP配置
```bash
interface GigabitEthernet0/0/1
ip address 192.168.1.2 255.255.255.0
quit
```

- OSPF配置
```bash
ospf
area 0.0.0.0
network 192.168.1.0 0.0.0.255
```