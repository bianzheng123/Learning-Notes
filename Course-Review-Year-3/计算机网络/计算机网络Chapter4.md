# 计算机网络Chapter4

# Network Layer - The Data Plane

在端系统和网络核心中都有

**forwarding，routing**

routing：决定去哪一个路由器

forwarding：从接入链路发往传出的链路

data plane

用于forwarding

control plane

用于routing

对每一个路由器，自己计算

centralized control plane

- 每一个路由器将自己的信息发送给Remote controller
- Remote controller将优化的参数发给路由器

Per-router control plane

- 每一个路由器存放路由算法
- 每一个路由器创建了这个路由转换表
- 每一个路由转换表按照最长前缀的原则进行转发，确定去往哪一个地方

网络层只是将数据包从发送端发给接收端

### router

input port

output port

#### forwarding方法

使用最长前缀进行forwarding

使用光纤连接input和output

- memory：read from input，write the output

- bus：一个时间间隙只能传输一个包
- crossbar

scheduling：确定哪个包先传，哪个包后传

- FIFO
- **drop**
  - priority
    - 对于优先级高的先传输，及其他来得晚
  - round robin
    - 拉链式传输包
  - generalized round robin
    - 同时实现priority和round robin
      - 对于高优先级的，每一次传输的包数量少于低优先级的

如果所有的input port都传输到output port，就可能会有很长的队

为什么是RTT * C

每一个接口都有自己的ip

每一个接口都是一个网卡

每一个接口都是双向的

能提供的功能：**best effort**

# Internet network layer

## IP protocol

只有头部的检验和

### fragmentation

不同的链路有不同的传输速率

将网络边缘的包切成多个部分，在网络核心中传输

网络边缘错误率高，传出速率低

网络核心则相反

#### 实现方式

将这些包分成多个部分，加上头部即可

fragflag：是否为完整的包

offset：用于确定包的片段顺序

length由链路中MTU决定，最大是1500

offset：用1代表8bytes

### IP addressing

每一个网络的接口都有一个ip地址

对于每一个子网，都附上不同的值

不同子网之间可以实现相互通信

子网掩码：用于区分内网和外网

**看有多少个子网：去掉路由器，看看是否相连**

- 路由器也算是子网，不单单是网络就算是子网

- Classless InterDomain Routing
- Class IP allocation: a.b.c.d/x
  - 子网掩码只有8个bit的分割形式

DHCP

- plug and play
- 连接路由器就自动的分配
- 有一个DHCP服务器，自动分配ip地址
- **DHCP client-server scenario**
- DHCP是应用层的协议
- default gateway
- ICANN：分配ISP的ip地址

### ip地址分配

有golbal ip address，也有内网的ip地址

路由器根据内网进行转换

### NAT

用于解决公网ip地址不足的问题

将内网的各个接口的ip地址统一

使用NAT转换表，当一个主机发送请求时，将源主机和源端口号稍作修改，发送给服务器

服务器返回结果后再根据NAT转换表改成原来的ip地址和端口号

### ipv6

使用**tunneling**将ipv4转换成ipv6

6能转换成4，4不能转换成6

将ipv6添加一个ipv4的头部地址，并添加src为自己，dst为下一个v6路由器

ICMP protocol





IHL：报文头部的长度

Length：ip报文总共的长度

标志位：第一个保留位

第二个是是否做分片

第三个代表该包是否为最后一个包

第四个代表从第几个序号开始发送

进行分片的各个包identification相同