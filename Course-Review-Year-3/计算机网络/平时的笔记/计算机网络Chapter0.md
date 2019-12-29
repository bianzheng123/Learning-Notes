# 计算机网络Chapter0

### 什么是计算机网络

数据传输（data communication）包括了电话网络，计算机网络

计算机网络：allow computers to exchange data

有很多的网络，计网只是其中一种

这节课主要讲计网的基本原理

### 各个层（自顶向下）

上层依赖下层，下层给上层提供数据

application: user（许多app），需要能接收发送数据

transport: end-end(TCP/UDP协议)，保证将包能按照顺序的传送进来

network: route(IP协议)，保证应该怎么走，做的是选择路的事情

link: 保证在两个节点之间，如何进行传输

and physical: bit transmit (许多种协议)，使用哪种具体的波形

### Telephone Network vs Computer Network

telephone network：终端简单，中继站复杂（只能单向传输，两个用户进行通信时链路阻塞）

computer network：终端复杂，中继站简单（只负责传输数据，不负责处理异常）

