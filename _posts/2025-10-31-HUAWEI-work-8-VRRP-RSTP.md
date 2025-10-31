---
layout: post
title:  "HUAWEI数通作业8-VRRPP + RSTP"
date:  2025-10-25 17:04:47 +0800
categories: HUAWEI-ENSP
excerpt_image: /assets/dong_man/bai_si.png
author: 双重十月
---

### 题目要求
!["图片"](/assets/HUAWEI/作业8：VRRP+RSTP实验.png)
完成图片中的要求


### PC机与网关
```bash
PC1  IP: 192.168.10.10  网关: 192.168.10.254
PC2  IP: 192.168.20.20  网关: 192.168.20.254
PC3  IP: 17.16.50.10    网关: 17.16.50.1
```

### R1的配置命令
- 基础配置
```bash
system-view 
undo info-center enable
sysname AR-XXX   把xxx改为自己的名字
```

- IP配置
```bash
interface LoopBack 0
ip address 10.1.1.1 32
interface GigabitEthernet 0/0/0
ip address 10.1.20.1 24
interface GigabitEthernet 0/0/1
ip address 10.1.26.1 24
interface GigabitEthernet 0/0/2
ip address 17.16.50.1 24
quit 
```

- OSPF动态路由配置
```bash
ospf
area 0
network 17.16.50.0 0.0.0.255
network 10.1.20.0 0.0.0.255
network 10.1.26.0 0.0.0.255
network 10.1.1.1 0.0.0.0
```

<br>

### agg01的配置命令
- 基础配置
```bash
system-view 
undo info-center enable
sysname agg01 
```

- VLAN和IP地址配置
```bash
vlan batch 10 20 100
interface Vlanif 100
ip address 10.1.20.2 24
interface Vlanif 10
ip address 192.168.10.252 24
interface Vlanif 20
ip address 192.168.20.252 24
interface LoopBack 0
ip address 10.2.2.2 32
quit 
```

- VRRP虚拟IP－优先级－端口监测配置
```bash
interface Vlanif 10
vrrp vrid 1 virtual-ip 192.168.10.254
vrrp vrid 1 priority 120
vrrp vrid 1 track interface GigabitEthernet 0/0/8 reduced 30
interface Vlanif 20
vrrp vrid 2 virtual-ip 192.168.20.254
quit
```

- RSP配置
```bash
stp enable 
stp mode rstp 
stp root primary
```

- 端口VLAN配置
```bash
interface GigabitEthernet 0/0/8
port link-type access 
port default vlan 100
interface GigabitEthernet 0/0/1
port link-type trunk
port trunk allow-pass vlan 10 20
interface GigabitEthernet 0/0/6
port link-type trunk
port trunk allow-pass vlan 10 20
interface GigabitEthernet 0/0/7
port link-type trunk
port trunk allow-pass vlan 10 20
quit
```

- OSPF动态路由配置
```bash
ospf
area 0
network 192.168.10.0 0.0.0.255
network 192.168.20.0 0.0.0.255
network 10.1.20.0 0.0.0.255
network 10.2.2.2 0.0.0.0
quit
quit
```

<br>

### agg02的配置命令
- 基础配置
```bash
system-view 
undo info-center enable
sysname agg02
```


- VLAN和IP地址配置
```bash
vlan batch 10 20 100
interface Vlanif 100
ip address 10.1.26.2 24
interface Vlanif 10
ip address 192.168.10.253 24
interface Vlanif 20
ip address 192.168.20.253 24
interface LoopBack 0
ip address 10.3.3.3 32
quit 
```

- VRRP虚拟IP－优先级－端口监测配置
```bash
interface Vlanif 10
vrrp vrid 1 virtual-ip 192.168.10.254
interface Vlanif 20
vrrp vrid 2 virtual-ip 192.168.20.254
vrrp vrid 2 priority 120
vrrp vrid 2 track interface GigabitEthernet 0/0/8 reduced 30
quit
```

- RSP配置
```bash
stp enable 
stp mode rstp 
stp root secondary 
```

- 端口VLAN配置
```bash
interface GigabitEthernet 0/0/8
port link-type access 
port default vlan 100
interface GigabitEthernet 0/0/1
port link-type trunk
port trunk allow-pass vlan 10 20
interface GigabitEthernet 0/0/6
port link-type trunk
port trunk allow-pass vlan 10 20
interface GigabitEthernet 0/0/7
port link-type trunk
port trunk allow-pass vlan 10 20
quit
```

- OSPF动态路由配置
```bash
ospf
area 0
network 192.168.10.0 0.0.0.255
network 192.168.20.0 0.0.0.255
network 10.1.26.0 0.0.0.255
network 10.3.3.3 0.0.0.0
quit
quit
```

<br>

### acc01的配置命令
- 基础配置
```bash
system-view 
undo info-center enable
sysname acc01
```

- VLAN配置
```bash
vlan batch 20 10
```

- RSP配置
```bash
stp enable 
stp mode rstp 
```

- 端口VLAN配置
```bash
interface GigabitEthernet 0/0/1
port link-type access 
stp edged-port enable 
port default vlan 10
interface GigabitEthernet 0/0/6
port link-type trunk
port trunk allow-pass vlan 10 20
interface GigabitEthernet 0/0/7
port link-type trunk
port trunk allow-pass vlan 10 20
quit
```

### acc02的配置命令
- 基础配置
```bash
system-view 
undo info-center enable
sysname acc02
```

- VLAN配置
```bash
vlan batch 20 10
```

- RSP配置
```bash
stp enable 
stp mode rstp 
```

- 端口VLAN配置
```bash
interface GigabitEthernet 0/0/1
port link-type access 
stp edged-port enable 
port default vlan 20
interface GigabitEthernet 0/0/6
port link-type trunk
port trunk allow-pass vlan 10 20
interface GigabitEthernet 0/0/7
port link-type trunk
port trunk allow-pass vlan 10 20
quit
```