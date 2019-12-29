# 计网lab7

SYN：TCP用于三次握手的数据段

传输层不对UDP做标记，网络层会对其做标记

通过receive window控制流量

TCP的报文头长度不固定

UDP报文长度固定

window scale：表示window的大小，有些会有移位操作

Seqn = Seq(n-1) + Pkt(n-1)---len(byte)

- 在握手，拆链的时候会有差异
- 握手，拆链时，报文的负载为0，不执行业务操作，Seq按理说就不会变

Ackn = Ack(n-1)（上一次确认过的报文） + Pkt(n-1)---len(tcp在这段时间内（Ackn-1到Ackn的时间）接收到的报文payload长度)