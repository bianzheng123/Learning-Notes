# Chapter 5_2

## Intra-AS routing

IGP

- RIP
  - 计算需要多少个hop才能到达目的地
    - 应该以延时进行计算
  - 只支持15个hop
  - 使用distance vector
- OSPF
  - link state
  - 可以同时维护负载均衡的两条路
  - 每一个OSPF的消息都需要认证，安全
  - 对于不同优先级的内容支持不同的传输速率
  - 支持unicast和multicast（多波）
  - Hierarchical OSPF
    - backbone的路由器不需要关心边缘的路由器的情况
- ISIS
  - 同OSPF

关键是性能

## Inter-AS routing

BGP

边界的路由器需要运行BGP

- eBGP

  从其他区域的路由器得知可以到达那些路由器

- iBGP

  告诉本区域的路由器可以到达哪个路由器

BGP session

- BGP之间的会话，来传输某个消息
- 包了TCP的头部
- 通过搜集信息，得到longest prefix matching的表

传递的信息

AS-path：prefix + 每一个AS的序号

NEXT-HOP：prefix + 每一个router的ip地址

BGP routing policy

对于不想过的，可以不告诉他不想过

关键是policy