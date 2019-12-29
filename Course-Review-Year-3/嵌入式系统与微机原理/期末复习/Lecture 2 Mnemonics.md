# Lecture 2 Mnemonics

ADD rz,ry,rx		rz = ry + rx

SUB rz, ry, rx		rz = ry - rx

RSB rz, ry, rx		rz = rx - ry

MUL rz, ry, rx		rz = rx * ry	只接受32bit的长度

MLA rz, ry, rx, rw		rz = ry * rx + rw

逻辑与，逻辑或，异或（输入相同为假，不同则为真）

BIC rz, ry, rx		rz = ry & !(rx) 只有ry为1，rx为0的位置输出为1，其余情况全部为0

### 寻址方式

- #### register addressing

- #### immediate addressing

使用立即数寻址

对于立即寻址，限制条件为

MOV rZ, $\# \mathrm{N} \times 2^{2(16-\mathrm{M})}$

其指令为0xE3A0ZMNN，其中NN是一个整体，范围是0-255，M是0-15

- #### indirect addressing

LDR r6, [r11]

读取r11中的值作为地址，在内存中寻找，并将结果返回r6

STR r6, [r11]

存取指令，同上

##### 数据在内存中的存储格式

little endian

数据存储的格式从根据地址从低到高

big endian

与little endian相反

- ### Base plus offset addressing

LDR r6, [r11,#12]

将r11的值加上12作为地址，在内存中取数作为地址，并存放到r6中

LDR r6, [r11,#12]!

相当于

```
ADD r11, r11, #12
LDR r6, [r11]
```

LDR r6, [r11], #12

相当于

```
LDR r6, [r11]
ADD r11, r11, #12
```

