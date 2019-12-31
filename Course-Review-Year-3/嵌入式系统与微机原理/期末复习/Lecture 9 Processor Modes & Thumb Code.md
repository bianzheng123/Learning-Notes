# Lecture 9 Processor Modes & Thumb Code

CPSR

总共有32个bit，只用了12bit

四个bit表示flag

五个bit表示当前状态

两个bit，表示是否可用中断

一个thumb bit

SPSR

用来保存模式的当前状态，用于返回正常模式时使用

supervisor mode

- 用于执行操作系统级别的指令

abort mode

- 当访问异常的内存时启动

undef mode

- 机器码没有被定义

system mode

- 用于操作系统

exception vector

- 当中断发生时pc的值就是不同mode对应的地址

## Thumb instruction set

就是将指令变成16bit

但是，能使用的指令集也少了许多

切换到thunb code时，32bit被分成了两个16bit的指令

16bit的指令映射到等价的32bit，再执行

优点

- 减少内存空间（指令需要的内容少了）

当内存空间和能耗占主导时用thumb code

否则，用ARM code