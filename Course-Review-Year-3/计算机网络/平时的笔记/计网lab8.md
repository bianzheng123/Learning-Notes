# 计网lab8

当接受侧发送了窗口为0（TCP ZeroWindow，Win = 0）的报文

发送侧会发送保持连接的报文（Keep-Alive），直到接受侧发送Win！=0的报文（说明接受侧缓存清空）

Option中，SACK permitted代表是否存在缓存（会话建立阶段）

如果接收方是permit，就选择重传（SR）

tcp_optionKind == 5 

对于不正常的报文

SACK：业务阶段

- SLE：代表收到的报文的范围的最小值
- SRE：代表收到的报文的范围的最大值