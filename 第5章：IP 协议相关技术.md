### 5.1 仅凭 IP 无法完成通信



### 5.2 DNS



#### 1. IP 地址不便记忆

IP 地址不方便记忆，TCP/IP 世界中从一开始就已经有了一个叫做主机识别码的东西。这种识别方式是指为每台计算机赋以唯一的主机名，在进行网络通信时可以直接使用主机名称而无需输入一大长串的 IP 地址。并且此时，系统必须自动将主机名转换为具体的 IP 地址。为了实现这样的功能，主机往往会利用一个叫做       **`hosts 的数据库文件`**。



#### 2. DNS 的产生



#### 3. 域名的构成

 **`域名`**  是指为了识别主机名称和组织机构名称的一种具有 **`分层的名称`** 。例如，仓敖艺术科技大学的域名如下：

kusa.ac.jp

域名由几个英文字母用点号连接构成。在上述域名中最左边的 "kusa" 表示仓敖艺术科技大学固有的域名。而 "ac" 表示大学或高等专科以及技术专门学校等高等教育相关机构。最后边的 "jp" 则代表日本。

在使用域名时，可以在每个主机名后面 **`追加组织结构的域名`** 。例如，有 pepper、piyo、kinoko 等主机时，它们完整的带域名的主机名将呈如下形式：

pepper.kusa.ac.jp

piyo.kusa.ac.jp

kinoko.kusa.ac.jp



* **`域名的分层`**



![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3TCP/IP/static/Chapter5/DNS.png?raw=true)



* **`域名服务器`**





* **`解析器`**

  进行 DNS 查询的主机和软件叫做 **`DNS 解析器`** 。用户所使用的工作站或个人电脑都属于解析器。 **`一个解析器至少要注册一个以上域名服务器的 IP 地址`** 。通常，它至少包含组织内部的域名服务器的 IP 地址。



#### 4. DNS 查询

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3TCP/IP/static/Chapter5/dns%20search.png?raw=true)



1. 向 DNS 服务器查询 IP 地址。
2. 由于 kusa 的 DNS 服务器并不知道 **`www.ietf.org`**  的 IP 地址是什么，它向根域名服务器请求进行查询。
3. 由于根域名服务器知道 **`www.ietf.org`**  的 IP 地址，因此将地址返回。
4. 向 ietf.org 的域名服务器查询 **`www.ietf.org`**  的 IP 地址。
5. 将查到的 IP 地址返回给客户端。
6. pepper 开始与 **`www.ietf.org`**  进行通信。



#### 5. DNS 如同互联网中的分布式数据库

* **`DNS 的主要记录`**

| 类型  | 编号 | 内容                     |
| ----- | ---- | ------------------------ |
| A     | 1    | 主机名的 IP 地址（IPv4） |
| NS    | 2    | 域名服务器               |
| CNAME | 5    | 主机别名对应的规范名称   |
| SOA   | 6    | 区域内权威记录起始标志   |
| WKS   | 11   | 已知的服务               |
| PTR   | 12   | IP 地址反向解析          |
| HINFO | 13   | 主机相关的追加信息       |
| MINFO | 14   | 邮箱与邮件组信息         |
| MX    | 15   | 邮件交换                 |
| TXT   | 16   | 文本                     |
| SIG   | 24   | 安全证书                 |
| KEY   | 25   | 密钥                     |
| GPOS  | 27   | 地理位置                 |
| AAAA  | 28   | 主机的 IPv6 地址         |
| NXT   | 30   | 下一代域名               |
| SRV   | 33   | 服务器选择               |
| *     | 255  | 所有缓存记录             |

​                                                                                                                                                          



### 5.3 ARP



#### 1. ARP 概要

ARP 是一种 **`解决地址问题的协议`** 。以目标 IP 地址为线索，用来定位下一个应该接收数据分包的网络设备对应的 **`MAC 地址`** 。如果目标主机不在同一个链路上时，可以通过 ARP 查找下一跳路由器的 MAC 地址。不过 ARP 只适用于 **`IPv4`** ， **`不能用于 IPv6`** 。 **`IPv6 中可以用 ICMPv6 替代 ARP 发送邻居探索消息`** 。



#### 2. ARP 的工作机制

那么 ARP 又是如何知道 MAC 地址的呢？简单地说，ARP 是 **`借助 ARP 请求与 ARP 响应两种类型的包确定 MAC 地址的`** 。

ARP 请求包还有一个作用，那就是将自己的 MAC 地址告诉给对方。根据 ARP 可以动态地进行解析，因此，在 TCP/IP 的网络构造和网络通信中无需事先知道 MAC 地址究竟是什么，只要有 IP 地址即可。

如果每发送一个 IP 数据报都要进行一次 ARP 请求以此确定 MAC 地址，那将会造成不必要的网络流量，因此，通常的做法是把获取到的 MAC 地址缓存一段时间。即把第一次通过 ARP 获取到的 MAC 地址作为 IP 对 MAC 的映射关系记忆到一个 **`ARP 缓存表`** 中，下一次再向这个 IP 地址发送数据报时不需再重新发送 ARP 请求，而是直接使用这个缓存表当中的 MAC 地址进行数据报的发送。 **`每执行一次 ARP，其对应的缓存内容都会被清除`** 。不过在清除之前都可以不需要执行 ARP 就可以获取想要的 MAC 地址。这样，在一定程度上也防止了 ARP 包在网络上被大量广播的可能性。

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3TCP/IP/static/Chapter5/ARP%20work%20mechanism.png?raw=true)

不过， **`MAC 地址的缓存是有一定期限的`** 。超过这个期限，缓存的内容将被清除。这使得 MAC 地址与 IP 地址对应关系即使发生了变化，也依然能够将数据包正确地发送给目标地址。



* **`ARP 包格式`**

  ![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3TCP/IP/static/Chapter5/ARPDataFormat.png?raw=true)

  

#### 3. IP 地址和 MAC 地址缺一不可



#### 4. RARP

RARP 是将 ARP 反过来，从 **`MAC 地址定位 IP 地址的一种协议`** 。例如将打印机服务器等小型嵌入式设备接入到网络时就经常会用得到。平常我们可以通过个人电脑设置 IP 地址，也可以通过 DHCP 自动分配获取 IP 地址。然而，对于使用嵌入式设备时，会遇到没有任何输入接口或无法通过 DHCP 动态获取 IP 地址的情况。在类似情况下，就可以使用 RARP。为此，需要架设一台 **`RARP 服务器`** ，从而在这个服务器上 **`注册设备的 MAC 地址及其 IP 地址`** 。然后再将这个设备接入到网络，插电启动设备时，该设备会发送一条 "我的 MAC 地址是 "，请告诉我，我的 IP 地址应该是什么的请求信息。RARP 服务器接到这个消息后返回类似于 "MAC 地址为设备，IP 地址为" 的信息给这个设备。而设备就根据从 RARP 服务器所收到的应答信息设置自己的 IP 地址。

1. 我的 IP 地址是什么？
2. RARP 请求包 MAC 地址 = 08:00:2B:94:4C:F8，IP 地址 = ?
3. RARP 响应包，你的 IP 地址是 172.16.1.3。



#### 5. 代理 ARP

通常 ARP 包会被路由器隔离，但是采用代理 ARP 的路由器可以将 ARP 请求转发给邻近的网段。由此，两个以上网段的节点之间可以像在同一个网段中一样进行通信。

 

### 5.4 ICMP

#### 1. 辅助 IP 的 ICMP

ICMP 的这种通知消息会使用 IP 进行发送。ICMP 的消息大致可以分为两类：一类是通知出错原因的错误消息，另一类是用于诊断的查询消息。

* **`ICMP 消息类型`**

  | 类型（十进制数） | 内容                                  |
  | ---------------- | ------------------------------------- |
  | 0                | 回送应答（Echo Reply）                |
  | 3                | 目标不可达（Destination Unreachable） |
  | 4                | 原点抑制（Source Quench）             |
  | 5                | 重定向或改变路由（Redirect）          |
  | 8                | 回送请求（Echo Request）              |
  | 9                | 路由器公告（Router Advertisement）    |
  | 10               | 路由器请求（Router Solicitation）     |
  | 11               | 超时（Time Exceeded）                 |
  | 17               | 地址子网请求（Address Mask Request）  |
  | 18               | 地址子网应答（Address Mask Reply）    |

  



#### 2. 主要的 ICMP 消息

* **`ICMP 目标不可达消息（类型 3）`** 

  具体原因如下：

  | 错误号 | ICMP 不可达消息                                              |
  | ------ | ------------------------------------------------------------ |
  | 0      | Network Unreachable                                          |
  | 1      | Host Unreachable                                             |
  | 2      | Protocol Unreachable                                         |
  | 3      | Port Unreachable                                             |
  | 4      | Fragmentation Needed and Don't Fragment was Set              |
  | 5      | Source Route Failed                                          |
  | 6      | Destination Network Unknown                                  |
  | 7      | Destination Host Unknown                                     |
  | 8      | Source Host Isolated                                         |
  | 9      | Communication with Destination Network is Administratively Prohibited |
  | 10     | Communication with Destination Host is Administratively Prohibited |
  | 11     | Destination Network Unreachable for Type of Service          |
  | 12     | Destination Host Unreachable for Type of Service             |



* **`ICMP 超时消息（类型 11）`**



* **`ICMP 回送消息（类型0、8）`**



#### 3. 其他 ICMP 消息

* **`ICMP 原点抑制消息（类型 4）`**



* **`ICMP 路由器探索消息（类型9、10）`**



* **`ICMP 地址掩码消息（类型 17、18）`**



#### 4. ICMPv6

* **`ICMPv6 的作用`**

  尤其在 IPv6 中，从 IP 地址定位 MAC 地址的协议从 ARP 转为 ICMP 的邻居探索消息。这种邻居探索消息融合了 IPv4 的 ARP、ICMP 重定向以及 ICMP 路由器选择消息等功能为一体，甚至还提供自动设置 IP 地址的功能。

  ICMPv6 中将 ICMP 大致分为两类：一类是错误消息，另一类是信息消息。类型 0 ~ 127 属于错误消息，128 ~ 255 属于信息消息。

  

  **`ICMPv6 错误消息`**

  | 类型（十进制数） | 内容                                  |
  | ---------------- | ------------------------------------- |
  | 1                | 目标不可达（Destination Unreachable） |
  | 2                | 包过大 （Packet Too Big）             |
  | 3                | 超时（Time Exceeded）                 |
  | 4                | 参数问题（Parameter Problem）         |



​	**`ICMPv6 信息消息`**

​	

| 类型（十进制） | 内容                                                         |
| -------------- | ------------------------------------------------------------ |
| 128            | 回送请求消息（Echo Request）                                 |
| 129            | 回送应答消息（Echo Reply）                                   |
| 130            | 多播监听查询（Multicast Listener Query）                     |
| 131            | 多播监听报告（Multicast Listener Report）                    |
| 132            | 多播监听结束（Multicast Listener Done）                      |
| 133            | 路由器请求消息（Router Solicitation）                        |
| 134            | 路由器公告消息（Router Advertisement）                       |
| 135            | 邻居请求消息（Neighbor Solicitation）                        |
| 136            | 邻居宣告消息（Neighbor Advertisement）                       |
| 137            | 重定向消息（Redirect Message）                               |
| 138            | 路由器重编号（Router Renumbering）                           |
| 139            | 信息查询（ICMP Node Information Query）                      |
| 140            | 信息应答（ICMP Node Information Response）                   |
| 141            | 反邻居探索请求消息（Inverse Neighbor Discovery Solicitation） |
| 142            | 反邻居探索宣告消息（Inverse Neighbor Discovery Advertisement） |

