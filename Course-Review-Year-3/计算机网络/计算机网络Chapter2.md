# 计算机网络Chapter2

## Overview

application architecture

client-server

peer-to-peer

- self-scalability
- 任意的端系统都能直接相互联系
- 只需建立一些连接即可，不需全部建立

除了应用层，其余的都有操作系统控制

不同主机之间使用message进行交互

相同的主机使用inter-process communication进行交互

IP：区分不同主机

port number：区分不同进程

提供给应用层的服务

- 数据完整性
  - 保证不会出现数据错误，丢包等操作
- 是否准时
- 吞吐量
- 安全

传输层协议

- 都不能保证吞吐量，延迟

- TCP
  - 接收端的接受速率是一定的，所以发送端的发送速率也是一定的
- UDP
  - 直接发送数据，吞吐量很快

## Web和HTTP

HTML：用来写网页的语言，不是协议

HTTP：是一个网页的协议

URL：主机名（host name），路径名（path name）

HTTP只有两种报文：request，response

HTTP

- stateless
  - 不需要关心其之前的请求
  - 对于需要登陆的网站
    - 使用cookies
- non-persistent HTTP
  - 在一个连接中，只得到一个对象
  - 同时可以建立多个连接，他们是并行的
  - 快
- persistent HTTP
  - 一次连接，传输多个对象
  - 节省资源
- request
  - POST method
    - 发送某个文件
  - URL method
    - 使用GET method
    - 得到某个网页或者文件
- response
  - 