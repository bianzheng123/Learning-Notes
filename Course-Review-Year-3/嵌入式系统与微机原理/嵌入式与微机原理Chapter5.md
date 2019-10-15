# 嵌入式与微机原理Chapter5

## Interrupts

用来处理事件

normal interrupt

fast interrupt

interrupt发生时，用户会切换模式

normal interrupt-IRO mode

fast interrupt - FIO mode

FIO和IRO都有其独立的寄存器

FIO是r8-r14

IRO是r13-r14

不同的模式在Current Program Status Register中表示

如果interrupt发生了，program counter就存放特定的地址，用来表示interrupt

