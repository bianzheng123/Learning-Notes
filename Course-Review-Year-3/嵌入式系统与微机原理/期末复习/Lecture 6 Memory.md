# Lecture 6 Memory

ROM-----non-volatile

RAM---------volatile

cache--------temporal and spatial locality

## Cache operation

hit rate-------------h

miss rate--------------m

Simple approach (ignoring cache controller overheads) analysis suggests for many accesses with a cache access time of $t_{c}$, and a main memory access time of $\boldsymbol{t}_{m}$ the mean access time will be

$t_{a v e}=h \times t_{c}+m \times t_{m}=h \times t_{c}+(1-h) \times t_{m}=(1-m) \times t_{c}+m \times t_{m}$

### 缓存策略

associative

direct mapped

#### 丢弃block策略

丢掉很久没有被访问过的

随机丢

丢掉的次数很多的

#### 写访问问题

write through

直接在主存中写

write copy

当要丢失cache时再写

## 三态门

将一整块大的memory分成一个个小的memory

取前几个最高位固定，其余看成一个个单独的block即可

## Memory mapped I/O

内存自动给输入和输出分配一个地址

写在地址里面的就可以看作是input/output