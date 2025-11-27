---
layout: post
title:  "HUAWEI数通作业12-ISIS协议"
date:  2025-11-57 20:04:47 +0800
categories: HUAWEI-ENSP
excerpt_image: /assets/dong_man/bai_si.png
author: 双重十月
---

### 题目要求
!["题目要求"](/assets/HUAWEI/题目要求.png)
<span style="color:red">下面所有命令对应的接口与图中是一致的，如果你的接口不是图片中的编号，自行调整，避免做出来的结果不通</span>

### XY-AR1的配置命令
- ISIS配置
```bash
system-view 
un in en
isis 
cost-style wide
is-level level-1
network-entity 49.0010.0000.0001.00
quit
```

- 接口配置
```bash
interface GigabitEthernet 0/0/0
ip address 192.168.10.254 24
isis enable 1
interface GigabitEthernet 0/0/1
ip address 10.10.1.1 24
isis enable 1
```

### XY-AR2的配置命令
- ISIS配置
```bash
system-view 
un in en
isis 
cost-style wide
is-level level-1-2
network-entity 49.0010.0000.0002.00
quit
```
- 接口配置
```bash
interface GigabitEthernet 0/0/1	
ip address 10.10.1.2 24
isi enable 1
interface GigabitEthernet 0/0/0	
ip address 10.10.5.2 24
isi enable 1
```

### Core-AR3的配置命令
- ISIS配置
```bash
system-view 
un in en
isis 
cost-style wide
is-level level-1-2
network-entity 49.0000.0000.0003.00
quit
```

- 接口配置
```bash
interface GigabitEthernet 0/0/1	
ip address 10.10.10.1 24
isi enable 1
interface GigabitEthernet 0/0/0	
ip address 10.10.5.1 24
isi enable 1
```

### Com-AR4的配置命令
- ISIS配置
```bash
system-view 
un in en
isis 
cost-style wide
is-level level-1-2
network-entity 49.0020.0000.0004.00
quit
```

- 接口配置
```bash
interface GigabitEthernet 0/0/1	
ip address 10.10.10.2 24
isi enable 1
interface GigabitEthernet 0/0/2	
ip address 10.10.20.1 24
isi enable 1
```


### Com-SW1的配置命令
- ISIS配置
```bash
system-view 
un in en
isis 
cost-style wide
is-level level-1
network-entity 49.0020.0000.0005.00
quit
```

- vlan配置
```bash
vlan batch 100 20 30
interface Vlanif 100
ip address 10.10.20.2 24
isis enable 1
interface Vlanif 20
ip address 192.168.20.254 24
isis enable 1
interface Vlanif 30
ip address 192.168.30.254 24
isis enable 1
quit
```

- 接口配置
```bash
interface GigabitEthernet 0/0/2
port link-type access 
port default vlan 100
interface GigabitEthernet 0/0/4
port link-type access 
port default vlan 20
interface GigabitEthernet 0/0/1
port link-type access 
port default vlan 30
```