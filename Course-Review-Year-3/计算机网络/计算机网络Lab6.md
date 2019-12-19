# 计算机网络Lab6

KeyCDN Edge Server

- 靠近的是用户，使得用户体验有了很大的提升

- 选择距离近，负载轻的提供服务

内容分发

orgin到CDN的分发

CDN到client的分发

cache-control

- 代表是否缓存到各级节点，如果缓存，缓存过期的时间是什么
- 作用范围，private，public，none
  - 如果是私有，则只缓存到私有的cache中，cache server不进行缓存
  - 如果是共有，则cache server中就进行缓存
  - none代表不缓存

via：判断是否使用到CDN的信息

x-cache：这个指的是CDN中的cache

网页中不是所有东西要做缓存的

对于时时刻刻都要发生变化的资源就不存到cache中

将静态资源放到CDN中

对于网页的基本结构，网站的图标等等，就不会发生变化，就直接放到CDN中转即可

## Web proxies

相当于网络中的cache

Forward Proxy

面向客户端，将client给保护起来，不提供client的具体信息

Reverse Proxy

代理orginal server，给客户端回送消息

CDN

相当于反向代理（Reverse Proxy）

对于浏览的网页，可能在内存中进行缓存，也可能在硬盘中进行缓存，空间换时间

对于缓存，设定一个过期时间，超过时间再访问，就重新请求

- 有时候不会进行重新请求，发送消息判断资源是否变化

- etag：基于内容做的hash编码，如果编码变化了，就代表请求的资源发生了变化
- cache-control：no-cache，max-age，must-revalidate

# DASH

根据不同的网络条件，启动不同速率的编码文件

mpd：xml文件，描述文件，不同的period

文件唯一，总体的描述

描述名字，速率，编码方式，分辨率，不同的带宽及其请求方式

