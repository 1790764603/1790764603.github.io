---
layout: post
title:  "HUAWEI数通作业6-MSTP + 链路聚合"
date:  2025-10-25 17:04:47 +0800
categories: HUAWEI-ENSP
excerpt_image: /assets/dong_man/bai_si.png
author: 双重十月
---

### 题目要求
完成图片中的要求，并验证结果，上传三张图片
图片1：agg01：<span style="color:red">disp stp brief</span>
图片1：agg01：<span style="color:red">disp eth-trunk1</span>
图片1：agg02：<span style="color:red">disp stp brief</span>
!["题目要求"](/assets/HUAWEI/题目要求.png)
<span style="color:red">下面所有命令对应的接口与图中是一致的，如果你的接口不是图片中的编号，自行调整，避免做出来的结果不通</span>

### PC机与网关
```bash
PC1  IP: 192.168.10.10  网关: 192.168.10.1
PC2  IP: 192.168.20.20  网关: 192.168.20.1
PC3  IP: 192.168.30.30  网关: 192.168.30.1
PC4  IP: 192.168.40.40  网关: 192.168.40.1
```


### agg01的配置命令
- vlan创建以及接口的vlan配置
```bash
system-view     进入配置界面
vlan batch 10 20 30 40      创建四个vlan
interface GigabitEthernet 0/0/1     进入接口G 0/0/1
port link-type trunk        接口模式改为trunk模式
port trunk allow-pass vlan all      允许所有vlan通过
interface GigabitEthernet 0/0/2     进入接口G 0/0/2
port link-type trunk        口模式改为trunk模式
port trunk allow-pass vlan all      允许所有vlan通过
quit    退出视图
```

- 链路聚合配置
```bash
interface Eth-Trunk 1       创建并进入聚合组1
mode lacp-static        链路聚合使用LACP
max active-linknumber 1     设置最大活动链路为1
port link-type trunk        聚合模式设置trunk模式
port trunk allow-pass vlan all      允许所有vlan通过
trunkport GigabitEthernet 0/0/4     将G0/0/4口加入到聚合组中
trunkport GigabitEthernet 0/0/5     将G0/0/5口加入到聚合组中
quit    退出视图
```

- MSTP配置
```bash
stp enable      启用stp
stp mode mstp       设置模式为mstp
stp region-configuration        进入stp配置视图
region-name 243     域名称为243
revision-level 2        修订级别为2
instance 1 vlan 10 20       将vlan 10 20 映射到实例1中
instance 2 vlan 30 40       将vlan 30 40 映射到实例1中
active region-configuration     让以上配置生效
quit    退出视图
```

- 设置mstp实例优先级
```bash
stp instance 1 root primary     设置实例1为主
stp instance 2 root secondary   设置实例2为备
```

<br>

### agg02的配置命令
- vlan创建以及接口的vlan配置
```bash
system-view     进入配置界面
vlan batch 10 20 30 40      创建四个vlan
interface GigabitEthernet 0/0/1     进入接口G 0/0/1
port link-type trunk        接口模式改为trunk模式
port trunk allow-pass vlan all      允许所有vlan通过
interface GigabitEthernet 0/0/2     进入接口G 0/0/2
port link-type trunk        口模式改为trunk模式
port trunk allow-pass vlan all      允许所有vlan通过
quit    退出视图
```

- 链路聚合配置
```bash
interface Eth-Trunk 1       创建并进入聚合组1
mode lacp-static        链路聚合使用LACP
max active-linknumber 1     设置最大活动链路为1
port link-type trunk        聚合模式设置trunk模式
port trunk allow-pass vlan all      允许所有vlan通过
trunkport GigabitEthernet 0/0/4     将G0/0/4口加入到聚合组中
trunkport GigabitEthernet 0/0/5     将G0/0/5口加入到聚合组中
quit    退出视图
```

- MSTP配置
```bash
stp enable      启用stp
stp mode mstp       设置模式为mstp
stp region-configuration        进入stp配置视图
region-name 243     域名称为243
revision-level 2        修订级别为2
instance 1 vlan 10 20       将vlan 10 20 映射到实例1中
instance 2 vlan 30 40       将vlan 30 40 映射到实例1中
active region-configuration     让以上配置生效
quit    退出视图
```

- 设置mstp实例优先级
```bash
stp instance 2 root primary     设置实例2为主
stp instance 1 root secondary   设置实例1为备
```

- 配置vlan的IP地址
```bash
interface Vlanif 10     进入vlan 10
ip address 192.168.10.1 24      设置IP地址
interface Vlanif 20     进入vlan 20
ip address 192.168.20.1 24      设置IP地址
interface Vlanif 30     进入vlan 30
ip address 192.168.30.1 24      设置IP地址
interface Vlanif 40     进入vlan 40
ip address 192.168.40.1 24      设置IP地址
```

<br>

### acc01的配置命令
- vlan创建以及接口的vlan配置
```bash
system-view     进入配置界面
vlan batch 10 20 30 40      创建四个vlan
interface GigabitEthernet 0/0/1     进入接口G 0/0/1
port link-type trunk        接口模式改为trunk模式
port trunk allow-pass vlan all      允许所有vlan通过
interface GigabitEthernet 0/0/2     进入接口G 0/0/2
port link-type trunk        口模式改为trunk模式
port trunk allow-pass vlan all      允许所有vlan通过
quit    退出视图
```

- MSTP配置
```bash
stp enable      启用stp
stp mode mstp       设置模式为mstp
stp region-configuration        进入stp配置视图
region-name 243     域名称为243
revision-level 2        修订级别为2
instance 1 vlan 10 20       将vlan 10 20 映射到实例1中
instance 2 vlan 30 40       将vlan 30 40 映射到实例1中
active region-configuration     让以上配置生效
quit    退出视图
```

- MSTP边缘化接口及单个vlan配置
```bash
interface Ethernet 0/0/1    进入接口E0/0/1
port link-type access       接口模式为access
port default vlan 10        加入vlan10
stp edged-port enable       启用边缘化
interface Ethernet 0/0/2    进入接口E0/0/2
port link-type access       接口模式为access
port default vlan 20        加入vlan20
stp edged-port enable       启用边缘化
quit
```

<br>

### acc02的配置命令
- vlan创建以及接口的vlan配置
```bash
system-view     进入配置界面
vlan batch 10 20 30 40      创建四个vlan
interface GigabitEthernet 0/0/1     进入接口G 0/0/1
port link-type trunk        接口模式改为trunk模式
port trunk allow-pass vlan all      允许所有vlan通过
interface GigabitEthernet 0/0/2     进入接口G 0/0/2
port link-type trunk        口模式改为trunk模式
port trunk allow-pass vlan all      允许所有vlan通过
quit    退出视图
```

- MSTP配置
```bash
stp enable      启用stp
stp mode mstp       设置模式为mstp
stp region-configuration        进入stp配置视图
region-name 243     域名称为243
revision-level 2        修订级别为2
instance 1 vlan 10 20       将vlan 10 20 映射到实例1中
instance 2 vlan 30 40       将vlan 30 40 映射到实例1中
active region-configuration     让以上配置生效
quit    退出视图
```

- MSTP边缘化接口及单个vlan配置
```bash
interface Ethernet 0/0/1    进入接口E0/0/1
port link-type access       接口模式为access
port default vlan 30        加入vlan30
stp edged-port enable       启用边缘化
interface Ethernet 0/0/2    进入接口E0/0/2
port link-type access       接口模式为access
port default vlan 40        加入vlan40
stp edged-port enable       启用边缘化
quit
```

### 验证截图
- agg01
```bash
display stp brief   截屏stp运行情况
display eth-trunk 1     截屏链路汇聚运行情况
```

- agg02
```bash
display stp brief   截屏stp运行情况
```

一共三张截图