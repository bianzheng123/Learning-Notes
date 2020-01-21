# 人工智能05Planning

有一个agent，经过怎样的动作，能达到最后的目的

就变成了SAT问题

1万个动作中有100要做，就要使用全排列算出最优的顺序

PDDL

- 在什么状态下，做什么动作，会有什么结果
- 做完一个Action，会到达某一个状态
- 从initial state出发，看成一个图，每一个顶点都是state，每一个边都是action
- 现实中图特别的大

### 搜索方法

对图进行松弛，变成一个能应用heuristics的function

方法

#### 加边

- 只是让可行的plan多走一点
- 会剪掉precondition
- 会将很多effect剪掉

理论上：任意两个state之间都有边了

事实：实际情况是每个顶点的state都可以表示为一个命题逻辑的sentence（goal state）

任意一个顶点做action都是可达的，则那些顶点的“并集”能满足goal state

顶点a：condition 1，condition 2

顶点b：condition 1，condition 3

goal：condition 1，condition 2，condition 4

每一张图可以看成一个集合a

所处的任何一个状态中，可以认为是挑选了集合a，并作conjunction

假设一个集合有2n个元素

里面有一个子集，是goal state

还有一堆其他的状态

问题：

为了满足goal state，需要挑选多少个状态

为了满足goal state，能否挑选k个解，从而满足条件

这是一个npc问题

#### 删除结点

- 有些状态不需要，比如说删除不在goal state的满足条件的状态
- 实质是抽取某一些无关的状态
- GraphPlan算法
  - 动态规划

对状态的定义没办法会具体到那么具体

- 向前迈了一步，距离门就近了一步，但是可能发生摔倒的情况
- 现实中的状态可能发生各种各样的情况
- 这时候就需要一个heuristics function

