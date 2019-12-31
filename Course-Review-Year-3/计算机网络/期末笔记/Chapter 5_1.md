# Chapter 5_1

## routing algorithm

forwarding table是转发表的结果

路由算法

全局

### link state

dijkstra

时间复杂度

$O(n^2)$或者$O(nlogn)$

网络中，up link和down link不一样

通过上一次的traffic作为cost，则每一次传输都会进行震荡

每一次传输都会将一部分链路进行闲置

speed of convergence：N

robustness可以

局部

### distance vector

借用相邻的节点的数据，来预估该节点到目标节点的最终距离

需要直到本节点到邻居的cost，以及邻居到目标节点的cost

每一个路由器都要维护一个向量，记录到其他节点的cost（通过prop来记录）

关键：

- 自己只计算自己的
- 如果自己的有变化，就告诉邻居节点

posioned reverse

如果a到另外一个节点b是经过节点c，而原来的路径值已经变化，就会需要很多次迭代

因为其他的节点没有变化，是通过其他节点得到值

使用posioned reverse减少迭代次数

就是b告诉c变化为无穷

speed of convergence：|V|

robustness不太好

## 路由算法

在一个autonomous systems内需要使用同一种算法

Intra-AS routing

- 区域内进行路由

- 如何到达gateway

Inter-AS routing

- 各个区域之间进行路由
- 查看需要经过哪几个AS才能到达目的地
- 本区域对应的gateway是什么

hot potato：不管外面多难走，让自己的路走的最快