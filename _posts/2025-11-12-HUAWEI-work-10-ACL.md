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
ip address 192.168.1.2 24
quit
```

- OSPF配置
```bash
ospf
area 0
network 192.168.1.0 0.0.0.255
```

### PC2-访客用户区
- 基础配置
```bash
system-view 
undo info-center enable
```

- IP配置
```bash
interface GigabitEthernet0/0/2
ip address 192.168.2.1 24
quit
```

- OSPF配置
```bash
ospf
area 0
network 192.168.2.0 0.0.0.255
```

### Router-1
- 基础配置
```bash
system-view 
undo info-center enable
```

- IP配置
```bash
interface GigabitEthernet0/0/1
ip address 192.168.1.254 24
interface GigabitEthernet0/0/2
ip address 192.168.2.254 24
interface GigabitEthernet1/0/0
ip address 192.168.100.254 24
interface GigabitEthernet0/0/0
ip address 172.16.100.1 24
quit
```

- OSPF配置
```bash
ospf
area 0
network 192.168.1.0 0.0.0.255
network 192.168.2.0 0.0.0.255
network 192.168.100.0 0.0.0.255
network 172.16.100.0 0.0.0.255
quit
quit
```

- ACL配置
```
acl number 2001
rule 5 permit source 192.168.1.0 0.0.0.255
rule 10 deny source 192.168.2.0 0.0.0.255
interface GigabitEthernet 1/0/0
traffic-filter outbound acl 2001
quit
```

### Router-2
- 基础配置
```bash
system-view 
undo info-center enable
```

- IP配置
```bash
interface GigabitEthernet0/0/0
ip address 172.16.100.5 24
interface GigabitEthernet0/0/1
ip address 172.16.50.254 24
quit
```

- OSPF配置
```bash
ospf
area 0
network 172.16.100.0 0.0.0.255
network 172.16.50.0 0.0.0.255
quit
quit
```

- Telnet配置
```bash
user-interface vty 0 4
authentication-mode password  // 回车会弹出输入，输入的内容是密码，要记住
user privilege level 15
quit
```

- ACL配置
```bash
acl number 3001
rule 5 permit tcp source 192.168.1.0 0.0.0.255 destination 172.16.100.0 0.0.0.255 destination-port eq telnet
rule 10 permit tcp source 192.168.100.0 0.0.0.255 destination 172.16.100.0 0.0.0.255 destination-port eq telnet
rule 15 deny tcp source any destination 172.16.100.0 0.0.0.255 destination-port eq telnet 
user-interface vty 0 4
acl 3001 inbound 
acl number 3002
rule 5 permit tcp source 192.168.2.0 0.0.0.255 destination 172.16.50.0 0.0.0.255 destination-port eq ftp
rule 10 deny tcp source any destination 172.16.50.0 0.0.0.255 destination-port eq ftp
interface GigabitEthernet 0/0/1
traffic-filter outbound acl 3002
```

### 作业上交要求
录屏
截图
[Router-1]disp acl 2000
[Router-2]disp acl all
PC1远程登录成功Router-1的截图
PC2访问Server1 FTP的截图，密码为空
PC1无法访问Server1 FTP的截图