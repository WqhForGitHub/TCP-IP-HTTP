### 4.1 IP 即网际协议

#### 1. IP 相当于 OSI 参考模型的第 3 层

网络层的主要作用是实现终端节点之间的通信。这种终端节点之间的通信也叫点对点通信。

从前面的章节可知，网络层的下一层，**`数据链路层的主要作用在互联同一种数据链路的节点之间进行包传递`** 。而一旦跨越多种数据链路，就需要借助网络层。网络层可以 **`跨越不同的数据链路`** ，即使在不同的数据链路中也能实现两端节点之间的数据包传输。

* **`主机与节点`**

  在互联网世界中，将那些配有 **`IP 地址的设备叫做主机`** 。这里的主机，可以是超大型计算机，也可以是小型计算机。这是因为互联网在当初刚发明的时候，只能连接这类大型的设备，因此习惯上就将配有 IP 地址的设备称为主机。

  然而，准确的说，**`主机的定义应该是指配置有 IP 地址，但是不进行路由控制的设备`** 。**`既配有 IP 地址又具有路由控制能力的设备叫做路由器`** ，跟主机有所区别。而 **`节点则是主机和路由器的统称`** 。



### 4.2 IP 基础知识

#### 1. IP 地址属于网络层地址

IP 地址用于在 **`连接到网络中的所有主机中识别出进行通信的目标地址`** 。因此，在 TCP/IP 通信中所有 **`主机或路由器`** 必须设定自己的 IP 地址。

不论一台主机与哪种数据链路连接，其 IP 地址的形式都保持不变。以太网、无线局域网、PPP 等，都不会改变 IP 地址的形式。

另外，在 **`网桥或交换集线器`** 等物理层或数据链路层数据包转发设备中，不需要设置 IP 地址。因为这些设备只负责将 IP 包转化为 0、1 比特流转发或对数据链路帧的数据部分进行转发，而不需要应对 IP 协议。



#### 2. 路由控制

* **`发送数据至最终目标地址`** 

​	跳，它是指 **`网络中的一个区间`** 。IP包正是在网络中一个个跳间被转发。因此 IP 路由也叫做 **`多跳路由`** 。在每一个区间内决定着包在 **`下一跳被转发的路径`** 。

* **`一跳的范围`**

  一跳是指利用  **`数据链路层以下分层的功能传输数据帧的一个区间`** 。以太网等数据链路中使用 MAC 地址传输数据帧。此时的一跳是指从源 MAC 地址到目标 MAC 地址之间传输帧的区间。也就是说它是主机或路由器网卡不经其他路由器而能直接到达的相邻主机或路由器网卡之间的一个区间。在一跳的这个区间内，电缆可以通过网桥或交换集线器相连，不会通过路由器或网关相连。

* **`多跳路由`**

  多跳路由是指  **`路由器或主机在转发 IP 数据包时只指定下一个路由器或主机`** ，而不是将到最终目标地址为止的所有通路全都指定出来。因为每一个区间（跳）在转发 IP 数据包时会分别指定  **`下一跳的操作`** ，直至包达到最终的目标地址。              

* **`路由控制表`**

  为了将数据包发给目标主机，**`所有主机都维护着一张路由控制表`** 。该表记录 **`IP 数据在下一步应该发给哪个路由器`** 。IP 包将根据这个路由表在各个数据链路上传输。



#### 3. 数据链路的抽象化

不同数据链路有个最大的区别，就是它们各自的 **`最大传输单位（MTU）`** 不同。就好像人们在邮寄包裹或行李时有各自的大小限制一样。

MTU 的值在 **`以太网中是 1500 字节，在 FDDI 中是 4352 字节，而 ATM 则为 9180 字节`** 。IP 的上一层可能会要求传送比这些 MTU 更多字节的数据，因此必须在线路上传送比包长还要小的 MTU。为了解决这个问题， **`IP 进行分片处理`** 。顾名思义，所谓分片处理是指， **`将较大的 IP 包分成多个较小的 IP 包`** 。分片的包   **`到了对端目标地址以后再被组合起来传给上一层`** 。即从 IP 的上层看，它完全可以忽略数据包在途中的各个数据链路上的 MTU，而只需要按照源地址发送的长度接收数据包。IP 就是以这种方式抽象化了数据链路层，使得从上层更不容易看到底层网络构造的细节。



#### 4. IP 属于面向无连接型

1. **`简化`**
2. **`提速`**

* 为了提高可靠性，上一层的 TCP  采用面向有连接型



### 4.3 IP 地址的基础知识

#### 1. IP 地址的定义

IP 地址（IPv4 地址）由 **`32 位正整数`** 来表示。TCP/IP 通信要求将这样的 IP 地址分配给每一个参与通信的主机。IP 地址在计算机内部以二进制方式被处理。然而，由于人类社会并不习惯于采用二进制方式，需要采用一种特殊的标记方式。那就是将 32 位的 IP 地址以 **`每 8 位为一组，分成 4 组，每组以 "." 隔开`** ，再将 **`每组数转换为十进制数`** 。下面举例说明这一方法。                                                                                          

10101100             00010100           00000001        00000001       （2 进制） 

10101100             00010100           00000001        00000001       （2 进制）

172                        20                         1                       1                      （10 进制） 



将表示成 IP 地址的数字整体计算，会得出如下数值。

2^32 = 4 294 967 296

从这个计算结果可知，最多可以允许 **`43 亿台计算机`** 连接到网络。

实际上，IP 地址并非是根据 **`主机台数`** 来配置的，而是 **`每一台主机上的每一块网卡（NIC）都得设置 IP 地址`** 。 通常一块网卡只设置一个 IP 地址，其实每一块网卡也可以设置多个 IP 地址 。 此外，一台路由器通常都会配置两个以上的网卡，因此可以设置两个以上的 IP 地址 。因此，让 43 亿台计算机全部连网其实是不可能的。后面将要详细介绍 IP 地址的两个组成部分 **`（网络标识和主机标识）`** ，了解了这两个组成部分后你会发现实际能够连接到网络的计算机个数更是少了很多。



#### 2. IP 地址由网络和主机两部分标识组成

IP 地址由网络地址和主机地址两部分组成。

网络标识在数据链路的每个段配置不同的值。网络标识必须保证相互连接的 **`每个段的地址不相重复`** 。而相同段内相连的主机必须有相同的网络地址。IP 地址的主机标识则 **`不允许在同一个网段内重复出现`** 。由此，可以通过设置网络地址和主机地址，在相互连接的整个网络中保证每台主机的 IP 地址都不会相互重叠。即 IP 地址具有了唯一性。

IP 包被转发到途中某个路由器时，正是利用目标 IP 地址的网络标识进行路由。因为即使不看主机标识，只要一见到网络标识就能判断出是否为该网段内的主机。那么，究竟是从第几位开始到第几位算是网路标识，又从第几位开始到第几位算是主机标识？关于这点，有约定俗成的两种类型。最初二者以分类进行区别。而现在基本以 **`子网掩码（网络前缀）区分`** 。不过，请读者注意，在有些情况下依据部分功能、系统和协议的需求，前一种的方法依然存在。

**`192.168.128.10/24`** 中的 "/24" 表示从第 1 位开始到多少位属于网络标识。在这个例子中，192.168.128 之前的都是该 IP 的网络地址。



#### 3. IP 地址的分类

* **`A 类地址`**

  A 类 IP 地址是首位以 "0" 开头的地址。从第 1 位到第 8 位是它的网络标识。用十进制表示的话，0.0.0.0 ~ 127.0.0.0 是 A 类的网络地址。A 类的地址的后 24 位相当于主机标识。因此，一个网段内可容纳的主机地址上限为 16777214 个。

* **`B 类地址`**

  B 类 IP 地址是前两位为 "10" 的地址。从第 1 位到第 16 位是它的网络标识。用十进制表示的话，128.0.0.1 ~ 191.255.0.0 是 B 类的网络地址。B 类地址的后 16 位相当于主机标识。因此，一个网段内可容纳的主机地址上限为 65534 个。

* **`C 类地址`**

  C 类 IP 地址是前三位为 "110" 的地址。从第 1 位到第 24 位是它的网络标识。用十进制表示的话，192.0.0.0 ~ 223.255.255.0 是 C 类的网络地址。C 类地址的后 8 位相当于主机标识。因此，一个网段内可容纳的主机地址上限为 254 个。

* **`D 类地址`**

​	D 类 IP 地址是前四位为 "1110" 的地址。从第 1 位到第 32 位是它的网络标识。用十进制表示的话，224.0.0.0 ~ 239.255.255.255 的是 D 类的网络地址。D 类地址没有主机标识，常被用于多播。

* **`关于分配 IP 主机地址的注意事项`**

  在分配 IP 地址时关于主机标识有一点需要注意。即要用比特位表示主机地址时，不可以全部为 0 或全部为 1。因为全部为只有 0 在表示对应的网络地址或 IP 地址 **`不可获知的情况下才使用`** 。而全部为 1 的主机地址通常作为 **`广播地址`** 。



#### 4. 广播地址

广播地址用于在 **`同一个链接中相互连接的主机之间发送数据包`** 。将 IP 地址中的 **`主机地址部分全部设置为 1`** ，就改成了广播地址。例如把 172.20.0.0/16 用二进制表示如下：

10101100.00010100.00000000.00000000      （二进制）

将这个地址的主机部分全部改为 1，则形成广播地址：

10101100.00010100.11111111.11111111      （二进制）

再将这个地址用十进制表示，则为 172.20.255.255。



* 两种广播

​	广播分为 **`本地广播`** 和 **`直接广播`** 两种。

​	**`在本网络内的广播`** 叫做本地广播。例如网络地址为 192.168.0.0/24 的情况下，广播地址是 192.168.0.255。因为这个广播地址的 IP 包会被路由器屏蔽掉，所以不会到达 192.168.0.0/24 以外的其他链路上。

​	**`在不同网络之间的广播`** 叫做直接广播。例如网络地址为 192.168.0.0/24 的主机向 192.168.1.255/24 的目标地址发送 IP 包。收到这个包的路由器，将数据转发给 192.168.1.0/24，从而使得所有 192.168.1.1 ~ 192.168.1.254 的主机都能收到这个包。



#### 5. IP 多播

* **`同时发送提交效率`**

多播用于将包发送给特定组内的所有主机。由于其直接使用 IP 协议，因此也不存在可靠传输。

* **`IP 多播与地址`**

​	多播使用 **`D 类地址`** 。因此，如果从首位开始到第 4 位是 **`"1110"`** ，就可以认为是多播地址。而剩下的 **`28`**  位可以成为多播的组编号。

从 224.0.0.0 到 239.255.255.255 都是多播地址的可用范围。其中从 224.0.0.0 到 224.0.0.255 的范围不需要路由控制，在同一个链路内也能实现多播。而在这个范围内设置多播地址会给全网所有组内成员发送多播的包。此外，对于多播，所有的主机（路由器以外的主机和终端主机）必须属于 224.0.0.1 的组，所有的路由器必须属于 224.0.0.2 的组。类似地，多播地址中有众多已知的地址，它们中具有代表性的部分已在表中列出。利用 IP 多播实现通信，除了地址外还需要 IGMP 等协议的支持。

​                  

| 地址       | 内容                                   |
| ---------- | -------------------------------------- |
| 224.0.0.0  | 预定                                   |
| 224.0.0.1  | 子网内所有的系统                       |
| 224.0.0.2  | 子网内所有的路由器                     |
| 224.0.0.5  | OSPF 路由器                            |
| 224.0.0.6  | OSPF 指定路由器                        |
| 224.0.0.9  | RIP2 路由器                            |
| 224.0.0.10 | IGRP 路由器                            |
| 224.0.0.11 | Mobile-Agents                          |
| 224.0.0.12 | DHCP 服务器/ 中继器代理                |
| 224.0.0.14 | RSVP-ENCAPSULATION                     |
| 224.0.1.1  | NTP Network Time Protocol              |
| 224.0.1.8  | SUN NIS+ Information Service           |
| 224.0.1.22 | Service Location（SVRLOC）             |
| 224.0.1.33 | RSVP-encap-1                           |
| 224.0.1.34 | RSVP-encap-2                           |
| 224.0.1.35 | Directory Agent Discovery（SVRLOC-DA） |
| 224.0.2.2  | SUN RPC PMAPPROC CALLIT                |



#### 6. 子网掩码

* **`子网与子网掩码`**

  自从引入了子网以后，一个 IP 地址就有了两种识别码。一是 **`IP 地址本身`** ，另一个是表示 **`网络部的子网掩码`** 。子网掩码用二进制方式表示的话，也是一个 **`32`** 位的数字。它对应 IP 地址 **`网络标识部分的位全部为 "1"`** ，对应 IP 地址 **`主机标识的部分则全部为 "0"`** 。由此，一个 IP 地址可以不再受限于自己的类别，而是可以用这样的子网掩码自由地定位自己的网络标识长度。当然，子网掩码必须是 IP 地址的首位开始连续的 "1"。

  对于子网掩码，目前有两种表示方式。以 172.20.100.52 的前 26 位是网络地址的情况为例，以下是其中一种表示方法，它将 IP 地址与子网掩码的地址分别用两行表示。

  

  IP 地址           172.        20.       100.      52

  子网掩码        255.       255.      255.     192

  

   网络地址       172.        20.        100.      0

  子网掩码        255.        255.      255.     192

  

  广播地址        172.        20.        100.      63

  子网掩码        255.        255.      255.     192

​	

​	另一种表示方式如下所示。它在每个 IP 地址后面追加网络地址的位数用 "/" 隔开。

​        IP 地址          172.        20.          100.       52             /26

​       网络地址        172.         20.         100.       0               /26

​       广播地址        172.         20.         100.       63             /26

​	不难看出，在第二种方式下记述网络地址时可以省略后面的 "0"。例如， **`172.20.0.0/16`**  跟 **`172.20/16`** 其实是一个意思。



#### 7. CIDR 与 VLSM

采用任意长度分割 IP 地址的网络标识和主机标识。这种方式叫做 CIDR。意为 **`无类型域间选路`**。        

可以随机修改组织内各个部门的子网掩码长度的机制，VLSM（可变长子网掩码）。它可以通过域间路由协议转换为 RIP2以及 OSPF 实现。根据 VLSM 可以将网络地址划分为主机数为 500 个时子网掩码长度为 /23，主机数为 50 个时子网掩码长度为 /26。从而在理论上可以将 IP 地址的利用率提高至 50%。                                                                

有了 CIDR 和 VLSM 技术，确实相对缓解了全局 IP 地址不够用的问题。但是 IP 地址的绝对数本身有限的事实无法改变。



#### 8. 全局地址与私有地址

私有网络的 IP 地址。它的地址范围如下所示：

**`10.  0.  0.  0 ~ 10.  255.  255.  255  （10/8）       A 类`**

**`172.  16.  0.  0 ~ 172.  31.  255.  255 （172.16/12）    B 类`**

**`192.  168.  0.  0 ~ 192.  168.  255.  255（192.168/16）  C 类`**

包含在这个范围内的 IP 地址都属于 **`私有 IP`**，而在此之外的 IP 地址称为 **`全局 IP`** 。





### 4.4 路由控制

实现 IP 通信的主机和路由器都必须持有一张这样的表。它们也正是在这个表格的基础上才得以进行数据包发送的。

该路由控制表的形成方法有两种：一种是管理员手动设置，另一种是路由器与其他路由器相互交换信息时自动刷新。前者叫静态路由控制，而后者叫做动态路由控制。为了让动态路由及时刷新路由表，在网络上互连的路由器之间必须设置好路由协议，保证正常读取路由控制信息。



#### 1. IP 地址与路由控制



#### 2. 路由控制表的聚合





### 4.5 IP 分割处理与再构成处理





### 4.6 IPv6

#### 1. IPv6 的必要性

IPv6 的地址长度则是原来的 4 倍，即 **`128 比特`** ，一般写成 **`8 个 16 位字节`** 。



#### 2. IPv6 特点



#### 3. IPv6 中 IP 地址的标记方法

IPv6 的 IP 地址长度为 **`128 位`** 。一般人们将 128 比特 IP 地址以 **`每 16 比特为一组，每组用冒号 ":" 隔开进行标记`** 。而且如果出现连续的 0 时还可以将这些 0 省略，并用两个冒号 "::" 隔开。但是，一个 IP 地址中只允许出现一次两个连续的冒号。在 IPv6 当中，人们正在努力使用最简单的方法标记 IP 地址，以便易于记忆。

* **`IPv6 的 IP 地址标记举例`**

  * 用二进制数表示

    1111111011011100: 1011101010011000: 0111011001010100: 0011001000010000: 1111111011011100: 1011101010011000: 0111011001010100:   0011001000010000

  * 用十六进制表示

    FEDC:BA98:7654:3210:FEDC:BA98:7654:3210

* **`IPv6 的 IP 地址省略举例`**

  * 用二进制数表示

    0001000010000000:0000000000000000:00000000000000000000000000:0000000000000000:0000100000000000:00100000000001100:0100000101111010

  * 用十六进制表示

    1080:0:0:0:8:800:200C:417A

    1080::8:800:200C:417A
    
    

####                                               4. IPv6 地址的结构





### 4.7 IPv4 首部

 ![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3TCP/IP/static/Chapter4/IPv4.png?raw=true)



* **`版本（Version）`**

  由 **`4`** 比特构成，表示标识 **`IP 首部的版本号`** 。IPv4 的版本号即为 4，因此在这个字段上的值也是 "4"。此外，关于 IP 的所有版本在以下表中列出。

  | 简称  | 版本 | 协议                        |
  | ----- | ---- | --------------------------- |
  | IP    | 4    | Internet Protocol           |
  | ST    | 5    | ST Datagram Mode            |
  | IPv6  | 6    | Internet Protocol version 6 |
  | TP/IX | 7    | TP/IX：The Next Internet    |
  | PIP   | 8    | The P Internet Protocol     |
  | TUBA  | 9    | TUBA                        |



* **`首部长度`**

​	由 **`4 比特`** 构成，表明 **`IP 首部的大小`** ，单位为 **`4 字节（32 比特）`** 。对于没有可选项的 IP 包，首部长度则设置为 "5"。也就是说，当没有可选项时，IP 首部的长度为 **`20 字节`** 。



* **`区分服务`**

   由 **`8 比特`** 构成，用来表明 **`服务质量`** 。每一位的具体含义如表所示。

  | 比特      | 含义       |
  | --------- | ---------- |
  | 0 1 2     | 优先度     |
  | 3         | 最低延迟   |
  | 4         | 最大吞吐   |
  | 5         | 最大可靠性 |
  | 6         | 最小代价   |
  | （3 ~ 6） | 最大安全   |
  | 7         | 未定义     |



​	

* **`总长度`**

​	表示 **`IP 首部与数据部分合起来的总字节数`** 。该字段长 **`16 比特`** 。因此 IP 包的最大长度为 **`65535 字节`** 。



* **`标识`**

  由 **`16 比特`** 构成，用于 **`分片重组`** 。同一个分片的标识值不同，不同分片的标识值不同。通常，每发送一个 IP 包，它的值也逐渐递增。此外， **`即使 ID 相同，如果目标地址、源地址或协议不同的话，也会被认为是不同的分片`** 。

* **`标记`**

​	由 **`3 比特`** 构成，表示包被分片的相关信息。每一位的具体含义请参考下表。

| 比特 | 含义                                                         |
| :--- | ------------------------------------------------------------ |
| 0    | 未使用。现在必须是 0。                                       |
| 1    | 指示是否进行分片 0- 可以分片   1-不能分片                    |
| 2    | 包被分片的情况下，表示是否为最后一个包。0- 最后一个分片的包   1- 分片中段的包 |

* **`片偏移`**

  由 **`13 比特`** 构成，用来标识被分片的每一个分段相对于原始数据的位置。每一个分片对应的值为 0。由于 FO 域占 13 位，因此最多可以表示 8192 个相对位置。单位为 8 字节，因此最大可表示原始数据 **`8 x 8192 = 65536 字节`** 的位置。

* **`生存时间`**

​	由 **`8 比特`** 构成，它最初的意思是以秒为单位记录当前包在网络上应该生存的期限。然而，在实际中它是指可以中转多少个路由器的意思。每经过一个路由器， **`TTL 会减少 1，直到变成 0 则丢弃该包`** 。

* **`协议`**

  由 **`8 比特`** 构成，表示的是 IP 包传输层的上层协议编号。目前常使用的协议如表所示已经分配相应的协议编号。

  | 分配编号 | 简称                    | 协议                                 |
  | -------- | ----------------------- | ------------------------------------ |
  | 0        | HOPOPT                  | IPv6 Hop-by-Hop Option               |
  | 1        | ICMP                    | Internet Control Message             |
  | 2        | IGMP                    | Internet Group Management            |
  | 4        | IP                      | IP in IP                             |
  | 6        | TCP                     | Transmission Control                 |
  | 8        | EGP                     | Exterior Gateway Protocol            |
  | 9        | IGP                     | any private interior gateway         |
  | 17       | UDP                     | User Datagram                        |
  | 33       | DCCP                    | Datagram Congestion Control Protocol |
  | 41       | IPv6                    | IPv6                                 |
  | 43       | IPv6-Route              | Routing Header for IPv6              |
  | 44       | IPv6-Frag               | Fragment Header for IPv6             |
  | 46       | RSVP                    | Reservation Protocol                 |
  | 50       | ESP                     | Encap Security Payload               |
  | 51       | AH                      | Authentication Header                |
  | 58       | IPv6-ICMP               | ICMP for IPv6                        |
  | 59       | IPv6-NoNxt              | No Next Header for IPv6              |
  | 60       | IPv6-Opts               | Destination Options for IPv6         |
  | 88       | EIGRP                   | EIGRP                                |
  | 89       | OSPFIGP                 | OSPF                                 |
  | 97       | ETHERIP                 | Ethernet-within-IP Encapsulation     |
  | 103      | PIM                     | Protocol Independent Multicast       |
  | 108      | IPComp                  | IP Payload Compression Protocol      |
  | 112      | VRRP                    | Virtual Router Redundancy Protocol   |
  | 115      | L2TP                    | Layer Two Tunneling Protocol         |
  | 124      | ISIS over IPv4          | ISIS over IPv4                       |
  | 132      | SCTP                    | Stream Control Transmission Protocol |
  | 133      | FC                      | Fibre Channel                        |
  | 134      | RSVP-E2E-IGNORE         | RSVP-E2E-IGNORE                      |
  | 135      | Mobility Header（IPv6） | Mobility Header（IPv6）              |
  | 136      | UDPLite                 | UDP-Lite                             |
  | 137      | MPLS-in-IP              | MPLS-in-IP                           |



* **`首部检验和`**

  由 **`16 比特（2 个字节）构成`** ，也叫 **`IP 首部校验和`** 。该字段只校验数据报的首部，不校验数据部分。它主要用来 **`确保 IP 数据报不被破坏`** 。



* **`源地址`**

  由 **`32 比特（4 个字节）构成`** ，表示 **`发送端 IP 地址`** 。  



* **`目标地址`**

  由 **`32 比特（4 个字节）构成`** ，表示 **`接收端 IP 地址`** 。



* **`可选项`**

  长度可变，通常只在进行实验或诊断时使用。该字段包含如下几点信息：

  * **`安全级别`**
  * **`源路径`**
  * **`路径记录`**
  * **`时间戳`**



* **`填充`**

  也称作 **`填补物`** 。在有可选项的情况下，首部长度可能不是 32 比特的整数倍。为此，通过 **`向字段填充 0， 调整为 32 比特的整数倍`** 。



* **`数据`**

  存入数据。将 IP 上层协议的首部也作为数据进行处理。





### 4.8 IPv6 首部格式

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3TCP/IP/static/Chapter4/IPv6.png?raw=true)



* **`版本`**

  与 IPv4 一样，由 **`4 比特`** 构成。IPv6 其版本号为 6，因此在这个字段上的值为 "6"。

* **`通信量类`**

  相当于 IPv4 的 TOS 字段，也由 **`8 比特`** 构成。由于 TOS 在 IPv4 中几乎没有什么建树，未能成为卓有成效的技术，本来计划在 IPv6 中删掉这个字段。不过，处于今后研究的考虑还是保留了该字段。

* **`流标号`**

  由 **`20 比特构成`** ，准备用于 **`服务质量控制`** 。

* **`有效载荷长度`**

  有效载荷是指包的数据部分。

* **`下一个首部`**

  相当于 IPv4 中的协议字段。由 **`8 比特`** 构成。不过在 IPv6 扩展首部的情况下，该字段表示后面第一个扩展首部的协议类型。

* **`跳数限制`**

  由 **`8 比特`** 构成。与 IPv4 中的 TTL 意思相同。为了强调可通过路由器个数这个概念，才将名字改成了 "Hop Limit"。数据每经过一次路由器就减 1，减到 0 则丢弃数据。

* **`源地址`**

  由 **`128 比特（8 个 16 位字节）`**构成。表示 **`发送端 IP 地址`** 。

* **`目标地址`**

  由 **`128 比特（8 个 16 位字节）`** 构成。表示 **`接收端 IP 地址`** 。               

* **`IPv6 扩展首部`**

  | 扩展首部      | 协议号 |
  | ------------- | ------ |
  | IPv6 逐跳选项 | 0      |
  | IPv6 路由标头 | 43     |
  | IPv6 片首部   | 44     |
  | 载荷加密      | 50     |
  | 认证首部      | 51     |
  | 首部终止      | 59     |
  | 目标地址选项  | 60     |
  | 移动首部      | 135    |

  