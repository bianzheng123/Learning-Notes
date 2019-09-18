# 嵌入式与微机原理Chapter1

## The Bus Architecture

#### 数据总线（data bus）

- 使用多根导线并联的方式
- 在同一时间内各个设备之间同时传输多个bit

#### 控制总线（control bus）

- ARM规定同一时间内只有一个设备能发送数据
- CPU进行控制其他设备能否发送数据

- CPU也控制不同设备中数据的同步
- 控制方式
  - 总的来说就是共享资源（时间，频率等），这里以时间为例
  - 将时间分成许多片段，每一个片段只允许一个设备发送数据，也叫TDMA
  - 对于一些片段，不能发送数据的设备，则这些设备会将数据放到缓存中，便于一起发送
  - 电脑看似是多个程序一起工作，其实是每一个时间段只能执行一个工作，只是看起来在多次执行而已

#### 地址总线（address bus）

- 便于CPU在内存中抓取命令

### Computer Memory

由数百万个逻辑门组成

每一个数据存放8bit，都有其独一无二的地址

ARM处理器：32bit，地址：32bit

32bit = 1 word = 4 byte

1 kilobyte = 1KB = 2^10 byte

### CPU

#### 组成

- Instruction Register
  - 将内存的指令放到下面

- Instruction Decoder
  - 将指令进行分析，分解

- ALU
  - 进行运算

- Register Bank
  - 暂时存储运算的数据  
  - 一些寄存器有特殊的用途
  - R0-R15
    - R15永远存放Program Counter，即下一条指令的地址
    - 通常R15的数据一直加4
    - 当遇到了branch指令（比如说函数调用）时，R15的值就会变化

- Address Register
  - 查看在哪里得到内存中的数据，用于内存的读，写操作
- 这五个东西通过Internal connections进行连接

#### CPU三个周期

- fetch：读取指令

- decode：将指令进行解码，分析

- execute：执行ALU，对内存进行读写等操作

Data Bus与Register Bank，Instruction Register相连

Address Register与Address Bus相连

需要4个Memory Location存放一个指令

### 指令例子

将114移动到寄存器R12

- 其指令为0xE3A0**C**0**72**
- 72是16进制的114
- C指的是寄存器R12