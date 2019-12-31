# Chapter 6

node, link

通过物理相连的进行连接

有多种link

framing

将datagram变成小的frame

## link access protocol

随机产生一个数字

过了一段时间后，就访问

## link layer

firmware

- 可以烧写

hardware

software

- 没办法写code

## error detection，correction

奇偶校验，也可以是二维的奇偶校验

**CRC**

d长度的码里面加上r bit，就能检测到r bit的错误

设定生成矩阵G

取异或，求余数

## multiple access protocol

一个时间内只能有一个人说话

避免collision

## MAC protocol

### channel partitioning

有很多数据要传输时效果很好

#### TDMA

将通信分成不同的时间

手机打电话

#### FDMA

将通信分成不同的频率

电视电缆

### random access 

要求数据不要太多

#### ALOHA

随机的决定是否要传输

如果撞了，就重新传

#### unslotted ALOHA

想要传输，就传输，也不对其

#### CSMA

先听，如果有人在传输，就不传，直到没人传输了就传输

如果有两个人同时想传，就撞了

CSMA/CD（在ethernet中，通过channel强度detect到）

如果检测到了别人传输，就停止传输

现有的方法

CSMA/CA（适用于无线的方式）

collision avoidance

相当于先声明内容，保留信道

### "taking turns"

#### polling

轮询

找一个master，挨个问

delay比较大

#### token passing

搞一个令牌

delay比较大

# LAN

## MAC地址

有几个网卡，就有几个bit

每个电脑都不能变

链路层要加一层MAC地址，作为链路层的头部，才能传输

每当传输到一个节点，就需要改变mac地址的内容

需要MAC地址

- 网卡无法拿到network layer信息
- 只要包的mac地址是自己，就pass上去

### ARP

使用ARP table

用来知道其他人的mac地址

就广播，有人回复就添加mac地址

用于寻找其他人的mac地址

## Ethernet

preamble

用来校准时钟

### switch

只是建一个switch table，通过别人发送过来的包进行自学习，然后转发

self-learning，plug-and-play

如果不知道别人的ip地址，就广播，等待别人发送消息，就能自学习

# 共同点

都可以store和转发

# 不同点

查看ip地址

router上面有计算

switch就是被动的记忆