# 嵌入式与微机原理Chapter5

## Interrupts

用来处理突发的事件

normal interrupt

fast interrupt

interrupt发生时，用户会切换模式

normal interrupt-IRQ mode

fast interrupt - FIQ mode

FIO和IRO都有其独立的寄存器，前几个寄存器共享

FIO的独立寄存器是r8-r14

IRO的独立寄存器是r13-r14

如果模式切换了，就需要将r0到r7的值存到stack中，切换成正常模式时再换回来

不同的模式在Current Program Status Register中表示

将值放到SPSR中

IRQ的第一条指令地址是0x00000018，FIQ是0x0000001C

- 当interrupt发生时，program counter就存在0x00000018或者0x0000001C
- 这些地址都是跳转的指令，用来跳转到相应的地址执行interrupt的内容

ARM7中，栈的保留地址存放了不同的异常

当interrupt发生时，program counter就自动存放对应的interrupt地址

如果interrupt发生了，program counter就存放特定的地址，用来表示interrupt

## Pipeline

Fetch，Decode，Execute

Decode

- Thumb decompress
  - 将16位的指令解压成32位的
- Decode
- Reg select

Execute

- Reg read
- Shift
- ALU
- Reg write

Execute花了更长的时间

CPU同时的使用计算机资源

对于Branch指令，如果执行错了，就可能丢掉两个周期

当normal interrupt发生时，会发生两次branch

- 第一次是发生了interrupt，指令地址跳转到0x00000018
- PC再跳转到存放interrupt代码的地方

如果是Fast interrupt，就发生一次branch

- 先跳转到0x0000001C
- 0x0000001C中不存放跳转指令，直接顺序执行下面的命令

当load和store进行时，就不能使用Fetch指令，就需要等2个额外的cycle

使用两个数组总线，一个用于存储数据，一个执行指令就可以避免冲突

当指令a在execute段中运行，program counter的大小为指令a的地址加8

对于branch指令，如果成功的跳转，会丢失两个时钟周期

对于跳转到subroutine指令，Execute占用了三个周期

- 同理，branch指令如果跳转成功，也会占用三个周期
- 如果没有跳转，就只占用一个周期

对于从内存中读取数据，需要先将数据从内存中取出来

load要两个额外的周期

store要一个额外的周期

auto index：将索引地址从两句变成一句