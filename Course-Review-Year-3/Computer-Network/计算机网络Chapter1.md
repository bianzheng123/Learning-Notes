# 计算机网络Chapter1

### 什么是互联网

##### 组成

主机（hosts），也叫端系统（end system）

- 运行程序的
- 例如手机，电器等

端系统通过通信链路（communication links）和分组交换机（packet switch）连在一起

- 通信链路（communication links）
  - 使用物理介质进行传递
  - 光纤，铜线，无线电频谱等
  - 传输速率：bandwidth，单位：bps
  - 通过分组进行传递
- 分组交换机
  - 接收包，传送包
  - 路由器（router），链路层交换机（link-layer switch）

端系统通过ISP接入因特网

- 因特网服务提供商（Internet service providers）
  - 将各个端系统连在一起

协议（protocols）

- 控制信息的接收和发送
- TCP，IP

因特网标准（Internet standards）

- 标准的协议
- RFC，IETF

##### 定义

网络的网络（network of networks）

给应用程序提供服务

给应用程序提供编程接口：socket

### 什么是协议

定义了消息传送的方式和顺序，以及报文发送/接收所采取的动作

关键词：**messages, actions**

### 网络结构

网络边缘（network edge）

- 主机（host）=端系统（end system）
- client/server model
  - 要求服务器永远在工作
- peer-peer model
  - require high bandwith

- 主机：客户（client），服务器（servers）
- 接入网（access networks）
  - 将端系统连接到边缘路由器（edge router）的物理链路
  - 家庭接入：DSL，电缆，光纤到户（FTTH），拨号和卫星
  - 企业接入：以太网和WiFi
  - 广域无线接入：3G，LTE
- 物理媒体：引导型媒体（guided media），非引导型媒体（unguided media）

网络核心（network core）

- 分组交换

  - 将大的报文分成较小的数据块，进行传输

  - 每个分组通过通信链路和分组交换机进行传输

  - 存储转发传输

    - 分组交换机只进行报文的传递和转发

    - 假设包大小为L，传输速率为R，则延迟为
      $$
      \frac{L(\text { bits })}{R(\text { bits } / \text { sec})}
      $$

