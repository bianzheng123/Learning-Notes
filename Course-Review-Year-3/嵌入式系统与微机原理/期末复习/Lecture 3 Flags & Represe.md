# Lecture 3 Flags & Represe

## Flags

zero flag, negative flag, carry flag, overflow flag

### zero flag

如果结果为0，则zero flag为1

SUBS r2, r1, r1，由于r2的计算结果为0，则zero flag结果为1

对于SUB指令，不管结果是否为0，zero flag的值都不会变

##### 用途

用于执行确定次数的循环

### carry flag

结果大于0xFFFFFFFF，则carrry flag为1

##### 用途

- ADC r0, r1,#3

如果carry flag为1，则r0 = r1 + 3 + 1

否则r0 = r1 + 3

- 做大于32位的加法

### overflow flag

出现异常情况时（两个正数相加结果为负，或者两个负数相加结果为正），为set

否则为clear

### negative flag

结果为负，就set                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            

## conditional execution

MOVCS r12, #114

如果carry flag为1，则执行MOV r12,#114

clear指的是carry flag的值为0

set指的是carry flag的值为1

## 表示负数

- 直接更换MSB的符号

- 取反加一

## 表示浮点数

第一部分占用1位，是符号位

第二部分占用8位，指数位，采用减去127的偏移量来表示

保留位代表正负无穷

| exp  | decimal | binary              |
| ---- | ------- | ------------------- |
| 128  | 255     | special cases(全一) |
| 0    | 127     | 0111 1111           |
| -127 | 0       | special cases(全零) |

第三部分是尾数域，前面默认的1去掉了，只是显示小数点后面的部分