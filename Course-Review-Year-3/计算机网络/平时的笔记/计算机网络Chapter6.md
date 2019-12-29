# 计算机网络Chapter6

# Link Layer

都是half-duplex，很少有full-duplex

就是时分复用/频分复用等

### error detection

添加r个冗余bit，做按位异或，保留最后几项

### CSMA/CD

通过信号强度进行检测，如果出现了collision，就停止传播



无线collision detection就不能检测信号强度检测collision

# MAC

### Channel Partitioning

TDMA

CDMA

(FDMA)

### Random Access

ALOHA

CSMA/CD

### Taking turns

cable access network

- 将多个技术混合
- downlink，uplink
- polling，token ring

# LAN

ARP

用来的值子网中主机的mac地址

Ethernet

包前面加01010101....

接收端和发送端的clock要同步

硬件中只能通过MAC地址比较，ip地址是软件的部分