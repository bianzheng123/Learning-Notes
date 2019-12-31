# Lecture 4 Subroutines

用来调用函数

link register

- 用来存储函数执行完后主函数返回的地址
- r14, lr

### 流程

执行其他函数时，调用BL（branch and link）指令

link register存放的是当前指令的地址加4，也就是从pc中得到值

### Nested subroutines

如果函数中调用函数，原来lr的值就会被覆盖

使用stack暂时存储原lr的返回值

### stack pointer

存放栈顶的地址

full stack--sp指向的是最后一个数据被存放的地址

empty stack--sp指向最后一个数据被存放的地址的下一个地址

Ascending and descending stack

r13 stack pointer, sp

STMFD sp!, {lr}

将lr存到stack中

LDMFD sp!,{lr}

将lr从stack中取出

STMFD sp!, {r6-r9, lr}

LDMFD sp!, {r6-r9, pc}

push, pop多个，但是需要一一对应

## Barrel Shifter

MOV r1, r2, LSL #5

r1 = r2 << 5

logical shift left 

logical shift right

arithmetic shift right

rotate right