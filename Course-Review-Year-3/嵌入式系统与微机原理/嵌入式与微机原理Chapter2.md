# 嵌入式与微机原理Chapter2

每一个机器码都有对应的汇编语句（Mnemonic code）

assembler将汇编语句变成机器码

ARM7可以进行加减乘，但是不能除

对于溢出的数字，自动抛弃最前面的一位 

用逻辑与（and），逻辑或（or）控制一个bit的开关，而在操作过程中，无需关心其他开关的顺序

bit clear

- `BIC rz,rx,ry`等价于`rz = rx and not(ry)`

#### 寻址方式

Register addressing

- 机器码中，使用数字代表寄存器

Immediate Addressing

- 指的是立即赋值
- eg：`ADD r2,r1,#10`指的是将r1内的值加10，赋值到r2中
- 常数一定要是位于最后一个
- 不能将32bit长的值赋给寄存器（指令长度不够）
- 立即数只有12bit长
  - 在这12bit长中，8bit用来指定其值
  - 另外4bit用来进行左移/右移操作（确定其位置）
    - 4bit只能确定16个位置
    - 这16个位置指的是偶数位上的16个bit 
    - 对于立即数，值只能是$\mathrm{N_{1}}\mathrm{N_{2}} \times 2^{2\mathrm{M}}$，其中0<=N_1,N_2<=255,0<=M<=15，这里的N_1,N_2分别指的是8个bit，不是相乘

Indirect Addressing

- `LDR r6,[r11]`指的是将r11中的数据作为地址，先在内存中找，然后放到r6中
- `STR r6,[r11]`指的是将r11中的值作为地址，将r6的值存在该地址中
- 寄存器存在内存中的顺序
  - little endian
    - 逆序存储
    - ![1568705620387](C:\Users\BianZheng\AppData\Roaming\Typora\typora-user-images\1568705620387.png)
  - big endian
    - 顺序存储
    - ![1568705673616](C:\Users\BianZheng\AppData\Roaming\Typora\typora-user-images\1568705673616.png)
  - cortexM用的是little endian
- Base plue offset addressing
  - `LDR r6,[r11,#12]`指的是将r11加12作为基址，将结果放到r6中
  - `LDR r6,[r11,#12]!`指在执行操作后，r6的值不仅会变化，r11的值也会加上12

### Restriction

ARM中，没有向左移操作，可以使用右移代替左移