# Chapter 4_2

## Subnets

将子网分成若干个小的子网

CIDR

之前的子网只能以8个bit为单位作为子网掩码

## DHCP

自动分配ip地址

分配流程

1. 主机先brocast（255.255.255.255），判断是否有DHCP的服务器
2. DHCP收到，返回一个ip地址
3. 主机返回ACK
4. DHCP发送ACK，表示确定使用该ip地址

该流程全程都是使用的broadcast

除了返回ip地址以外，还有first-hop router，DNS的ip地址和名字，子网掩码

application protocol

## Hierarchical addressing

在ISP中获得ip地址

通过子网掩码进行结构化的内容

- 知道那些有没有用，方便查找
- 减少路由器routing table的长度（longest prefix matching）

如果用户切换了ISP，还是使用了同样的ip地址

根据longest prefix matching，forwarding table不需要变化

## NAT

多个主机共享一个ip地址，使用不同的port

外部的网络不知道ip地址是多少

### 流程

内部的主机发送给router

router改变报文的ip地址，并在translation table中添加一条记录

收到恢复后，根据记录改变ip地址和端口号对主机进行分配

### 缺点

- violate end-to-end argument
  - ip地址在传输的过程中被修改了
  - 对于p2p，外面的人不知道怎么访问内部的主机
    - relay，使用一个中间知道的地址的主机
    - 必须要内部的主机先发送请求，NAT才能产生记录，产生内部主机的port

- NAT在路由器中工作，但是做的是传输层的事情，就违反了协议
- 主机连接的每一个port，router都要建立连接，就可能会被占满，不过这个一般不可能

## ICMP

internet control message protocol

发的是正常的datapacket，返回的是错误的状态（ICMP）

网络层上的报文

用于表示路由器的状态的，当发生错误时，返回一个ICMP报文

中间的router也是可以发送ICMP报文

eg：traceroute

## IPV6

不支持fragmentation，但是会添加ICMPv6，发送包太长的错误

没有checksum，为了在转发过程中更快

v4的option变成了next header

可以知道哪个主机在multicast group中，减少发送的流量

- 支持多媒体业务

### Translation 

对于只能识别ipv4的router，就要在外面套一层ipv4的header

