# Chapter 4_1

### flow control

控制接收方溢出

改变窗口大小

### congestion control

控制router溢出

通过timeout，duplicate ACK

慢慢的增加window size，快速的减少window size

congestion avoidance：一个一个的增长：MSS

slow start：先指数地增长，到了某个门限，就慢慢的增加

#### TCP congestion control

对于timeout，window设为1

对于duplicate ACK，变成原来的一半

平均的TCP吞吐量，都不会超过最大限度的3/4

对于wireless里面，就不适用congestion control（wireless也会出现空中丢包）

#### TCP fairness

两个TCP连接，如果两个带宽不同，到最后，一定会实现TCP fairness

如果想提高TCP传输速率，就建立很多个连接

# Network Layer

host-to-host

一整个网络只用一个网络层协议，就是ip协议

data-plane			forwarding 

在路由器中选择哪一个口发送

control plane		routing

决定是从哪一个出发

## forwarding table

设定了一个范围，符合范围的，就去xxx端口

具体方法：longest prefix matching

## router

### input和output

line termination

物理层和链路层的事情

link layer protocol

有线/无线网卡（将物理层解析成一个一个的包）

queue

就是缓冲

- priority scheduling

### switching fabrics

switch快慢直接影响到router的性能

- memory

  主要受限于writing speed

- bus

  通过公共的总线进行传输

  受制于总线的速率

  一次只能传输一个

- cross bar

  一次可以传输多个

## IP协议

头部大小：20byte

MTU：IP包的最大报文长度（包括ip协议头部）

### fragmentation

不同的链路有不同的最大包大小，就需要分片

分片的id都相同

fragflag

- 最后一个包的fragflag设置为0
- 其余为1

offset来表示分片，表示的单位为8byte

### IP地址

路由器也有ip地址，而且是多个

### subnet

将所有router拿掉，则所有连在一起的部分就是一个子网

通过子网掩码得知该子网分配了多少个ip

通过这样子可以节省forwarding table的数量