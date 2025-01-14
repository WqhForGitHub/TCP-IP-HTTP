### 6.1 传输层的作用



#### 3. 两种传输层协议 TCP 和 UDP

* #### **`TCP`**

  TCP 是面向连接的、可靠的流协议。流就是指不间断的数据结构，你可以把她它想象成排水管道中的水流。当应用程序采用 TCP 发送消息时，虽然可以保证发送的顺序，但还是犹如没有任何间隔的数据流发送给接收端。TCP 为提供可靠性传输，实行顺序控制或重发控制机制。此外还具有流控制、拥塞控制、提高网络利用率等众多功能。

* **`UDP`**

  UDP 是不具有可靠性的数据报协议。细微的处理它会交给上层的应用去完成。在 UDP 的情况下，虽然可以确保发送消息的大小，却不能保证消息一定会到达。因此，应用有时会根据自己的需要进行重发处理。



#### 4. TCP 与 UDP 区分

​                                                            



### 6.2 端口号

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               

#### 1. 端口号定义

在传输层中也有这种类似于地址的概念，那就是端口号。端口号用来识别 **`同一台计算机中进行通信的不同应用程序`** 。因此，它也被称为 **`程序地址`** 。



#### 2. 根据端口号识别应用





#### 3. 通过 IP 地址、端口号、协议号进行通信识别

因此，TCP/IP 或 UDP/IP 通信中通常采用 5 个信息来识别一个通信。它们是源 IP 地址、目标 IP 地址、协议号、源端口号、目标端口号。只要其中某一项不同，则被认为是其他通信。





#### 4. 端口号如何确定



* **`标准既定的端口号`**

  这种方法也叫静态方法。它是指每个应用程序都有其指定的端口号。但并不是说可以随意使用任何一个端口号。每个端口号都有其对应的使用目的。例如，HTTP、TELNET、FTP 等广为使用的应用协议中所使用的端口号就是固定的。这些端口号也被称之为知名端口号。知名端口号一般由 **`0`** 到 **`1023`** 的数字分配而成。应用程序应该避免使用知名端口号进行既定目的之外的通信，以免产生冲突。除知名端口号之外，还有一些端口号也被正式注册。它们分布在 **`1024`** 到  **`49151`** 的数字之间。不过，这些端口号可用于任何通信用途。

* **`动态分配法`**

  此时，服务端有必要确定监听端口号，但是接受服务的客户端没必要确定端口号。在这种方法下，客户端应用程序可以完全不用自己设置端口号，而全权交给 **`操作系统`** 进行分配。操作系统可以为每个应用程序分配互不冲突的端口号。例如，每需要一个新的端口号时，就在之前分配号码的基础上加 1。这样，操作系统就可以动态地管理端口号了。动态分配地端口号取值范围在 **`49152`** 到 **`65535`** 之间。



#### 5. 端口号与协议

* **`TCP 具有代表性的知名端口号`**

| 端口号 | 服务名                | 内容                                    |
| ------ | --------------------- | --------------------------------------- |
| 1      | tcpmux                | TCP Port Service Multiplexer            |
| 7      | echo                  | Echo                                    |
| 9      | discard               | Discard                                 |
| 11     | systat                | Active Users                            |
| 13     | daytime               | Daytime                                 |
| 17     | qotd                  | Quote of the Day                        |
| 19     | chargen               | Character Generator                     |
| 20     | ftp-data              | File Transfer [  Default Data ]         |
| 21     | ftp                   | File Transfer [ Control ]               |
| 22     | ssh                   | SSH Remote Login Protocol               |
| 23     | telnet                | Telnet                                  |
| 25     | smtp                  | Simple Mail Transfer Protocol           |
| 43     | nicname               | Who Is                                  |
| 53     | domain                | Domain Name Server                      |
| 70     | gopher                | Gopher                                  |
| 79     | finger                | Finger                                  |
| 80     | http（www, www-http） | World Wide Web HTTP                     |
| 95     | supdup                | SUP DUP                                 |
| 101    | hostname              | NIC Host Name Server                    |
| 102    | iso-tsap              | ISO-TSAP                                |
| 109    | pop2                  | Post Office Protocol - Version 2        |
| 110    | pop3                  | Post Office Protocol - Version 3        |
| 111    | sunrpc                | SUN Remote Procedure Call               |
| 113    | auth（ident）         | Authentication Service                  |
| 117    | uucp-path             | UUCP Path Service                       |
| 119    | nntp                  | Network News Transfer Prorocol          |
| 123    | ntp                   | Network Time Protocol                   |
| 139    | netbios-ssn           | NETBIOS Session Service（SAMBA）        |
| 143    | imap                  | Internel Message Access Protocol v2, v4 |
| 163    | cmip-man              | CMIP/TCP Manager                        |
| 164    | cmip-agent            | CMIP/TCP Agent                          |
| 179    | bgp                   | Border Gateway Protocol                 |
| 194    | irc                   | Internet Relay Chat Protocol            |
| 220    | Imap3                 | Interactive Mail Access Protocol v3     |
| 389    | ldap                  | Lightweight Directory Access Protocol   |
| 434    | mobileip-agent        | Moblie IP Agent                         |
| 443    | https                 | http protocol over TLS/SSL              |
| 515    | printer               | Printer spooler（lpr）                  |
| 587    | submission            | Message Submission                      |
| 636    | ldaps                 | ldaps protocol over TLS/SSL             |
| 989    | ftps-data             | ftp protocol, data, over TLS/SSL        |
| 990    | ftps                  | ftp protocol, control, over TLS/SSL     |
| 993    | imaps                 | imap4 protocol over TLS/SSL             |
| 995    | pop3s                 | pop3 protocol over TLS/SSL              |

​         

* **`UDP 具有代表性的知名端口号`**

| 端口号 | 服务名         | 内容                               |
| ------ | -------------- | ---------------------------------- |
| 7      | echo           | Echo                               |
| 9      | discard        | Discard                            |
| 11     | systat         | Active Users                       |
| 13     | daytime        | Daytime                            |
| 17     | qotd           | Quote of the Day                   |
| 19     | chargen        | Character Generator                |
| 49     | tacacs         | Login Host Protocol（TACCACS）     |
| 53     | domain         | Domain Name Server                 |
| 67     | bootps         | Bootstrap Protocol Server（DHCP）  |
| 68     | bootpc         | Bootstrap Protocol Client（DHCP）  |
| 69     | tftp           | Trivial File Transfer Protocol     |
| 111    | sunrpc         | SUN Remote Procedure Call          |
| 123    | ntp            | Network Time Protocol              |
| 137    | netbios-ns     | NETBIOS Name Service（SAMBA）      |
| 138    | netbios-dgm    | NETBIOS Datagram Service（SAMBA）  |
| 161    | snmp           | SNMP                               |
| 162    | snmptrap       | SNMP TRAP                          |
| 177    | xdmcp          | X Display Manager Control Protocol |
| 201    | at-rtmp        | AppleTalk Routing Maintenance      |
| 202    | at-nbp         | AppleTalk Name Binding             |
| 204    | at-echo        | AppleTalk Echo                     |
| 206    | at-zis         | AppleTalk Zone Information         |
| 213    | ipx            | IPX                                |
| 434    | mobileip-agent | Mobile IP Agent                    |
| 520    | router         | RIP                                |
| 546    | dhcov6-client  | DHCPv6 Client                      |
| 547    | dhcpv6-server  | DHCPv6-Server                      |



### 6.3 UDP

**`UDP 的特点及其目的`**

由于 UDP 面向无连接，它可以随时发送数据。再加上 UDP 本身的处理既简单又高效，因此经常用于以下几个方面：

* **`包总量较少的通信（DNS、SNMP 等）`**
* **`视频、音频等多媒体通信（即时通信）`**
* **`限定于 LAN 等特定网络中的应用通信`**
* **`广播通信（广播、多播）`**