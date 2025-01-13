### 6.1 HTTP 报文首部







### 6.2 HTTP 首部字段



#### 3. 4 种 HTTP 首部字段类型

HTTP 首部字段根据实际用途被分为以下 4 种类型。

**通用首部字段**

**请求首部字段**

**响应首部字段**

**实体首部字段**



#### 4. HTTP/1.1 首部字段一览

HTTP/1.1 规范定义了如下 47 种首部字段。

* **`通用首部字段`**

| 首部字段名        | 说明                       |
| ----------------- | -------------------------- |
| Cache-Control     | 控制缓存的行为             |
| Connection        | 逐跳首部、连接的管理       |
| Date              | 创建报文的日期时间         |
| Pragma            | 报文指令                   |
| Trailer           | 报文末端的首部一览         |
| Transfer-Encoding | 指定报文主体的传输编码方式 |
| Upgrade           | 升级为其他协议             |
| Via               | 代理服务器的相关信息       |
| Warning           | 错误通知                   |



* **`请求首部字段`**

| 首部字段名          | 说明                                            |
| ------------------- | ----------------------------------------------- |
| Accept              | 用户代理可处理的媒体类型                        |
| Accept-Charset      | 优先的字符集                                    |
| Accept-Encoding     | 优先的内容编码                                  |
| Accept-Language     | 优先的语言（自然语言）                          |
| Authorization       | Web 认证信息                                    |
| Expect              | 期待服务器的特定行为                            |
| From                | 用户的电子邮箱地址                              |
| Host                | 请求资源所在的服务器                            |
| If-Match            | 比较实体标记（ETag）                            |
| If-Modified-Since   | 比较资源的更新时间                              |
| If-None-Match       | 比较实体标记（与 If-Match 相反）                |
| If-Range            | 资源未更新时发送实体 Byte 的范围请求            |
| If-Unmodified-Since | 比较资源的更新时间（与 If-Modified-Since 相反） |
| Max-Forwards        | 最大传输逐跳数                                  |
| Proxy-Authorization | 代理服务器要求客户端的认证信息                  |
| Range               | 实体的字节范围请求                              |
| Referer             | 对请求种 URI 的原始获取方                       |
| TE                  | 传输编码的优先级                                |
| User-Agent          | HTTP 客户端程序的信息                           |



* **`响应首部字段`**

| 首部字段名         | 说明                         |
| ------------------ | ---------------------------- |
| Accept-Ranges      | 是否接收字节范围请求         |
| Age                | 推算资源创建经过时间         |
| ETag               | 资源的匹配信息               |
| Location           | 令客户端重定向至指定 URI     |
| Proxy-Authenticate | 代理服务器对客户端的认证信息 |
| Retry-After        | 对再次发起请求的是时机要求   |
| Server             | HTTP 服务器的安装信息        |
| Vary               | 代理服务器缓存的管理信息     |
| WWW-Authenticate   | 服务器对客户端的认证信息     |



* **`实体首部字段`**

| 首部字段名       | 说明                         |
| ---------------- | ---------------------------- |
| Allow            | 资源可支持的 HTTP 方法       |
| Content-Encoding | 实体主体适用的编码方式       |
| Content-Language | 实体主体的自然语言           |
| Content-Length   | 实体主体的大小（单位：字节） |
| Content-Location | 替代对应资源的 URI           |
| Content-MD5      | 实体主体的报文摘要           |
| Content-Range    | 实体主体的位置范围           |
| Content-Type     | 实体主体的媒体类型           |
| Expires          | 实体主体过期的日期时间       |
| Last-Modified    | 资源的最后修改日期时间       |



### 6.3 HTTP/1.1 通用首部字段

通用首部字段是指，请求报文和响应报文双方都会使用的首部。



#### 1. Cache-Control

通过指定首部字段 Cache-Control 的指令，就能操作缓存的工作机制。

指令的参数是可选的，多个指令之间通过 "." 分隔。首部字段 Cache-Control 的指令可用于请求及响应时。

```http
Cache-Control: private, max-age=0, no-cache
```



* **`Cache-Control 指令一览`**

可用的指令按请求和响应分类如下所示。

1.  **`缓存请求指令`**

| 指令            | 参数   | 说明                         |
| --------------- | ------ | ---------------------------- |
| no-cache        | 无     | 强制向源服务器再次验证       |
| no-store        | 无     | 不缓存请求或响应的任何内容   |
| max-age = [秒]  | 必需   | 相应的最大 Age 值            |
| max-stale= [秒] | 可省略 | 接收已过期的响应             |
| min-fresh= [秒] | 必需   | 期望在指定时间内的响应仍有效 |
| no-transform    | 无     | 代理不可更改媒体类型         |
| only-if-cached  | 无     | 从缓存获取资源               |
| cache-extension | -      | 新指令标记（token）          |



2.  **`缓存响应指令`**

| 指令              | 参数   | 说明                                           |
| ----------------- | ------ | ---------------------------------------------- |
| public            | 无     | 可向任意方提供响应的缓存                       |
| private           | 可省略 | 仅向特定用户返回响应                           |
| no-cache          | 可省略 | 缓存前必须先确认其有效性                       |
| no-store          | 无     | 不缓存请求或响应的任何内容                     |
| no-transform      | 无     | 代理不可更改媒体类型                           |
| must-revalidate   | 无     | 可缓存但必须再向源服务器进行确认               |
| proxy-revalidate  | 无     | 要求中间缓存服务器对缓存的响应有效性再进行确认 |
| max-age = [ 秒 ]  | 必需   | 响应的最大 Age 值                              |
| s-maxage = [ 秒 ] | 必需   | 公共缓存服务器响应的最大 Age 值                |
| cache-extension   | -      | 新指令标记（token）                            |



**`表示是否能缓存的指令`**

**`public 指令`**

```http
Cache-Control: public
```

当指定使用 public 指令时，则 **`明确表明其他用户也可利用缓存`** 。

**`private 指令`**

```http
Cache-Control: private
```

当指定 private 指令后，响应只以特定的用户作为对象，这与 public 指令的行为相反。**`缓存服务器会对该特定用户提供资源缓存的服务`** ，对于其他用户发送过来的请求，代理服务器则不会返回缓存。

**`no-cache 指令`**

```http
Cache-Control: no-cache
```

使用 no-cache 指令的目的是为了防止从缓存中返回过期的资源。客户端发送的请求中如果包含 no-cache 指令，则表示客户端将不会接收缓存过的响应。于是，中间的缓存服务器必须把客户端请求转发给源服务器。



**`控制可执行缓存的对象的指令`**

**`no-store 指令`**

```http
Cache-Control: no-store
```

当使用 **`no-store`** 指令时，暗示请求或响应中包含机密信息。因此，该指令规定缓存不能在本地储存请求或响应的任一部分。



从字面意思上很容易把 no-cache 误解成为不缓存，**`但事实上 no-cache 代表不缓存过期的资源，缓存会向源服务器进行有效期确认后处理资源`** 。 **`no-store 才是真正地不进行缓存`** 。



**`指定缓存期限和认证的指令`**

**`s-maxage 指令`**

```http
Cache-Control: s-maxage=604800（单位：秒）
```

另外，当使用 **`s-maxage`** 指令后，则直接忽略对 **`Expires`** 首部字段及 **`max-age`** 指令的处理。 



**`max-age 指令`**

```http
Cache-Control: max-age=604800（单位：秒）
```

当客户端发送的请求中包含 max-age 指令时，如果判定缓存资源的缓存时间数值比指定时间的数值更小，那么客户端就接收缓存的资源。另外，当指定 max-age 值为 0，那么 **`缓存服务器通常需要将请求转发给源服务器`** 。当服务器返回的响应中包含 max-age 指令时，缓存服务器将不对资源的有效性再做确认，而 max-age 数值代表资源保存为 **`缓存的最长时间`** 。应用 HTTP/1.1 版本的缓存服务器遇到同时存在 Expires 首部字段的情况时， **`会优先处理 max-age 指令，而忽略掉 Expires 首部字段`** 。而 HTTP/1.0 版本的缓存服务器的情况却相反，max-age 指令会被忽略掉。



#### 2. Connection

Connection 首部字段具备如下两个作用：

* 控制不再转发给代理的首部字段
* 管理持久连接

* 控制代理不再转发的首部字段

```http
Connection: 不再转发的首部字段名
```

在客户端发送请求和服务器返回响应内，使用 Connection 首部字段，可控制不再转发给代理的首部字段（即 Hop-by-hop 首部）。

* 管理持久连接

```http
Connection: close
```

HTTP/1.1 版本的默认连接都是 **`持久连接`** 。为此，客户端会在持久连接上连续发送请求。当服务器端想明确断开连接时，则指定 Connection 首部字段的值为 Close。HTTP/1.1 之前的 HTTP 版本的默认连接都是 **`非持久连接`** 。为此，如果想在旧版本的 HTTP 协议上维持持续连接，则需要指定 Connection 首部字段的值为 **`Keep-Alive`** 。



#### 3. Date

首部字段 Date 表明创建 HTTP 报文的日期和时间。HTTP/1.1 协议使用在 RFC1123 中规定的日期时间的格式，如下示例。

```http
Date: Tue, 03 Jul 2012 04:40:59 GMT
```



#### 4. Pragma

Pragma 是 HTTP/1.1 之前版本的历史遗留字段，仅作为与 HTTP/1.0 的向后兼容而定义。规范定义的形式唯一，如下所示：

```http
Pragma: no-cache
```

该首部字段属于通用首部字段，但只用在客户端发送的请求中。客户端会要求 **`所有的中间服务器不返回缓存的资源`** 。所有的中间服务器如果都能以 HTTP/1.1 为基准，那直接采用 Cache-Control: no-cache 指令缓存的处理方式是最为理想的。但要 **`整体掌握全部中间服务器使用的 HTTP 协议版本却是不现实的`** 。因此，发送的请求同时含有下面两个首部字段。

```http
Cache-Control: no-cache
Pragma: no-cache
```



#### 5. Trailer

首部字段 Trailer 会事先说明在报文主体后记录了哪些首部字段。该首部字段可应用在 HTTP/1.1 版本分块传输编码时。



#### 6. Transfer-Encoding

首部字段 Transfer-Encoding 规定了传输报文主体时采用的编码方式。



#### 7. Upgrade

首部字段 Upgrade 用于检测 HTTP 协议及其他协议是否可使用更高版本进行通信，其参数值可以用来指定一个完全不同的通信协议。                                                                                                                                                                                                                                                                                                                                                               



#### 8. Via

使用首部字段 Via 是为了追踪客户端与服务器之间的请求和响应报文的传输路径。



#### 9. Warning

HTTP/1.1 的 Warning 首部是从 HTTP/1.0 的响应首部演变过来的。该首部通常会 **`告知用户一些与缓存相关的问题的警告`** 。

```http
Warning: 113 gw.hackr.jp:8080 "Heuristic expiration" Tue, 03 Jul => 2012 05:09:44 GMT
```

Warning 首部的格式如下。最后的日期时间部分可省略。

```http
Warning: [警告码] [警告的主机:端口号] "[警告内容]" ([日期时间])
```



* **`HTTP/1.1 警告码`**

| 警告码 | 警告内容                                         | 说明                                                         |
| ------ | ------------------------------------------------ | ------------------------------------------------------------ |
| 110    | Response is stale（响应已过期）                  | 代理返回已过期的资源                                         |
| 111    | Revalidation failed（再验证失败）                | 代理再验证资源有效性时失败（服务器无法到达等原因）           |
| 112    | Disconnection operation（断开连接操作）          | 代理与互联网连接被故意切断                                   |
| 113    | Heuristic expiration（试探性过期）               | 响应的使用期超过 24 小时（有效缓存的设定时间大于 24 小时的情况下） |
| 199    | Miscellaneous warning（杂项警告）                | 任意的警告内容                                               |
| 214    | Transformation applied（使用了转换）             | 代理对内容编码或媒体类型等执行了某些处理时                   |
| 299    | Miscellaneous persistent warning（持久杂项警告） | 任意的警告内容                                               |



### 6.4 请求首部字段



#### 1. Accept

```http
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
```

Accept 首部字段可通知服务器， **`用户代理能够处理的媒体类型及媒体类型的相对优先级`** 。可使用 type/subtype 这种形式，一次指定多种媒体类型。下面我们试举几个媒体类型的例子。

* **`文本文件`** 

​	text/html,text/plain,text/css ...

​	application/xhtml+xml,application/xml ...

* **`图片文件`**

  image/jpeg,image/gif,image/png ...

* **`视频文件`**

  video/mpeg,video/quicktime ...

* **`应用程序使用的二进制文件`**

​	application/octet-stream,application/zip ...

比如，如果浏览器不支持 PNG 图片的显示，那 Accept 就不指定 image/png，而指定可处理的 image/gif 和 image/jpeg 等图片类型。若想要给显示的媒体类型增加优先级，则使用 q= 来额外表示权重值，用分号 **`（;）`** 进行分隔。**`权重值 q 的范围是 0 ~ 1（可精确到小数点后 3 位）`** ，且 1 为最大值。不指定权重 q 值时，默认权重为 q=1.0。当服务器提供多种内容时，将会首先返回权重值最高的媒体类型。



#### 2. Accept-Charset

```http
Accept-Charset: iso-8859-5, unicode-1-1;q=0.8
```

Accept-Charset 首部字段可用来通知 **`服务器用户代理支持的字符集及字符集的相对优先顺序`** 。另外，可一次性指定多种字符集。与首部字段 Accept 相同的是可用权重 q 值来表示相对优先级。 **`该首部字段应用于内容协商机制的服务器驱动协商`** 。



#### 3. Accept-Encoding

```http
Accept-Encoding: gzip, deflate
```

Accept-Encoding 首部字段用来告知服务器用户代理支持的内容编码及内容编码的优先级顺序。可一次性指定多种内容编码。下面试举出几个内容编码的例子。

* **`gzip`**

  由文件压缩程序 gzip（GNU zip）生成的编码格式，采用 Lempel-Ziv 算法及 32 位循环冗余校验。

* **`compress`**

* **`deflate`**

* **`identity`**

采用权重 q 值来表示相对优先级，这点与首部字段 Accept 相同。另外，也可使用星号 **`（*）`** 作为通配符，指定 **`任意的编码格式`** 。



#### 4. Accept-Language

```http
Accept-Language: zh-cn,zh;q=0.7,en-us,en;q=0.3
```

首部字段 Accept-Language 用来告知 **`服务器用户代理能够处理的自然语言集`** ，以及自然语言集的相对优先级。可一次指定多种自然语言集。和 Accept 首部字段一样，按权重值 q 来表示相对优先级。在上述图例中，客户端在服务器有中文版资源的情况下，会请求其返回中文版对应的响应，没有中文版时，则请求返回英文版的响应。



#### 5. Authorization

```http
Authorization: Basic dWVub3NlbjpwYXNzd29yZA==
```

首部字段 Authorization 是用来告知服务器， **`用户代理的认证信息`** 。通常，想要通过服务器认证的用户代理会在接收到返回的 401 状态码响应后，把首部字段 Authorization 加入请求中。共用缓存在接收到含有 Authorization 首部字段的请求时的操作处理会略有差异。



#### 6. Expect

```http
Expect: 100-continue
```

客户端使用首部字段 Expect 来告知服务器， **`期望出现的某种特定行为`** 。



#### 7. From

首部字段 From 用来告知服务器使用 **`用户代理的用户的电子邮件地址`** 。通常，其使用目的就是为了显示搜索引擎等用户代理的负责人的电子邮件联系方式。                                                                                                                                                                                                                                                                                                                                                                     



#### 8. Host

```http
Host: www.hackr.jp
```

首部字段 Host 会告知服务器， **`请求的资源所处的互联网主机名和端口号`** 。Host 首部字段在 HTTP/1.1 规范内是唯一一个必须被包含在请求内的首部字段。



#### 9. If-Match

形如 If-xxx 这种样式的请求首部字段，都可称为 **`条件请求`** 。服务器接收到附带条件的请求后，只有判断指定条件为真时，才会执行请求。

**`只有当 If-Match 的字段值跟 ETag 值匹配一致时，服务器才会接受请求`** 。

```http
If-Match: "123456"
```

首部字段 If-Match ，属附带条件之一，它会告知 **`服务器匹配资源所用的实体标记值`** 。这时的服务器无法使用弱 ETag 值。服务器会比对 If-Match 的字段值和资源的 ETag 值，仅当两者一致时，才会执行请求。反之，则返回状态码 412 的响应。还可以使用星号 **`（*）`** 指定 If-Match 的字段值。针对这种情况，服务器将会忽略 ETag 的值，只要资源存在就处理请求。                                                                                                              



#### 10. If-Modified-Since

如果在 If-Modified-Since 字段指定的日期时间后， **`资源发生了更新，服务器会接受请求`** 。

```http
If-Modified-Since: Thu, 15 Apr 2004 00:00:00 GMT
```

If-Modified-Since 用于确认代理或客户端拥有的 **`本地资源的有效性`** 。获取资源的更新日期时间，可通过确认首部字段 **`Last-Modified`**  来确定。 



#### 11. If-None-Match

用于指定 If-None-Match 可获取最新的资源。因此，这与使用首部字段 If-Modified-Since 时有些类似。



#### 12. If-Range

   

#### 13. If-Unmodified-Since



#### 14. Max-Forwards

```                    http
Max-Forwards: 10
```



#### 15. Proxy-Authorization

 ```http
 Proxy-Authorization: Basic dGlwOjkpNLAGfFY5
 ```

接收到从 **`代理服务器发来的认证质询时`** ，客户端会发送包含首部字段 Proxy-Authorization 的请求，以告知 **`服务器认证所需要的信息`** 。





#### 16. Range

```http
Range: bytes=5001-10000
```

对于只需获取 **`部分资源的范围请求`** ，包含首部字段 Range 即可告知服务器资源的指定范围。上面的示例表示请求获取从第 5001 字节至第 10000 字节的资源。接收到附带 Range 首部字段请求的服务器，会在处理请求之后返回状态码为 **`206 Partial Content`**  的响应。无法处理该范围请求时，则会返回状态码 **`200 OK`**  的响应及全部资源。



#### 17. Referer

```                                                                                                     http
Referer: http://www.hackr.jp/index.htm
```

首部字段 Referer 会告知 **`服务器请求的原始资源的 URI`** 。客户端一般都会发送 Referer 首部字段给服务器。但当直接在浏览器的地址栏输入 URI ，或出于安全性的考虑时，也可以不发送该首部字段。



#### 18. TE

```http
TE: gzip, deflate;q=0.5
```

首部字段 TE 会告知服务器 **`客户端能够处理响应的传输编码方式及相对优先级`** 。它和首部字段 Accept-Encoding 的功能很相像，但是用于传输编码。首部字段 TE 除指定传输编码之外，还可以指定伴随 **`trailer 字段的分块传输编码的方式`** 。应用后者时，只需把 trailers 赋值给该字段值。

```http
TE: trailers
```



#### 19. User-Agent

```http
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:13.0) Gecko/ => 20100101 Firefox/13.0.1
```

首部字段 User-Agent 会将 **`创建请求的浏览器和用户代理名称等信息传达给服务器`** 。





### 6.5 响应首部字段



#### 1. Accept-Ranges

```http
Accept-Ranges: bytes
```

首部字段 Accept-Ranges 是用来告知客户端 **`服务器是否能处理范围请求`** ，以指定获取服务器端某个部分的资源。可指定的字段值有两种，可处理范围请求时指定其为 **`bytes`** ，反之则指定其为 **`none`** 。



#### 2. Age

```http
Age: 600
```

首部字段 Age 能告知客户端， **`源服务器在多久前创建了响应`** 。字段值的单位为秒。若创建该响应的服务器是缓存服务器，Age 值是指缓存后的响应 **`再次发起认证到认证完成的时间值`** 。代理创建响应时必须加上首部字段 Age。



#### 3. ETag

```http
ETag: "82e22293907ce725faf67773957acd12"
```

首部字段 ETag 能告知 **`客户端实体标识`** 。它是一种可将资源以字符串形式做唯一性标识的方式。服务器会为每份资源分配对应的 ETag 值。另外， **`当资源更新时，ETag 值也需要更新`** 。生成 ETag 值时，并没有统一的算法规则，而仅仅是由服务器来分配。资源被缓存时，就会被分配唯一性标识。例如，当使用中文版的浏览器访问 **`http://www.google.com`** 时，就会返回中文版对应的资源，而使用英文版的浏览器访问时，则会返回英文版对应的资源。两者的 URI 是相同的，所以仅凭 URI 指定缓存的资源是相当困难的。若在下载过程中出现连接中断、再连接的情况，都会依照 ETag 值来指定资源。



**强 ETag 值和弱 ETag 值**

ETag 中有强 ETag 值和弱 ETag 值之分。

* **`强 ETag 值`**

​	强 ETag 值， **`不论实体发生多么细微的变化都会改变其值`** 。

```http
ETag: "usagi-1234"
```



* **`弱 ETag 值`**

​	弱 ETag 值只用于提示资源是否相同。只有资源发生了 **`根本改变`** ， **`产生差异时才会改变 ETag 值`** 。这时，会在字段值最开始处附加 **`W/`** 。

```http
ETag: W/"usagi-1234"
```



#### 4. Location

```http
Location: http://www.usagidesign.jp/sample.html
```

使用首部字段 Location 可以将响应接收方引导至某个与 **`请求 URI 位置不同的资源`** 。基本上，该字段会配合 **`3xx：Redirection`**  的响应，提供 **`重定向的 URI`** 。几乎所有的浏览器在接收到包含首部字段 Location 的响应后， **`都会强制性地尝试对已提示的重定向资源的访问`** 。



#### 5. Proxy-Authenticate

```http
Proxy-Authenticate: Basic realm="Usagidesign Auth"
```

首部字段 Proxy-Authenticate 会把 **`由代理服务器所要求的认证信息发送给客户端`** 。它与客户端和服务器之间的 HTTP 访问认证的行为相似，不同之处在于其认证行为是在客户端与代理之间进行的。而客户端与服务器之间进行认证时，首部字段 WWW-Authorization 有着相同的作用。有关 HTTP 访问认证，后面的章节会再进行详尽阐述。



#### 6. Retry-After

```http
Retry-After: 120
```

首部字段 Retry-After 告知 **`客户端应该在多久之后再次发送请求`** 。主要配合状态码 **`503 Service Unavailable`**  响应，或 **`3xx Redirect`** 响应一起使用。字段值可以指定为具体的日期时间（Wed, 04 Jul 2012 06:34:24 GMT 等格式），也可以是 **`创建响应后的秒数`** 。



#### 7. Server

```http
Server: Apache/2.2.17 （Unix）
```

首部字段 Server 告知客户端当前服务器上安装的 **`HTTP 服务器应用程序的信息`** 。不单单会标出 **`服务器上的软件应用名称`** ，还有可能 **`包括版本号和安装时启用的可选项`** 。

```http
Server: Apache/2.2.6 （Unix） PHP/5.2.5
```



#### 8. Vary

```http
Vary: Accept-Language
```

首部字段 Vary 可对 **`缓存进行控制`** 。源服务器会向代理服务器传达关于本地缓存使用方法的命令。从代理服务器接收到源服务器返回包含 Vary 指定项的响应之后，若再要进行缓存，仅对请求中含有相同 Vary 指定首部字段的请求返回缓存。即使对相同资源发起请求，但由于 Vary 指定的首部字段不相同，因此必须要从源服务器重新获取资源。



#### 9. WWW-Authenticate

```                                                                                                                                                                                                     http
WWW-Authenticate: Basic realm="Usagidesign Auth"
```

首部字段 WWW-Authenticate 用于 **`HTTP 访问认证`** 。它会告知客户端适用于访问请求 URI 所指定资源的认证方案（Basic 或是 Digest）和带参数提示的质询（challenge）。状态码 401 Unauthorized 响应中，肯定带有首部字段 WWW-Authenticate。上述示例中，realm 字段的字符串是为了辨别请求 URI 指定资源所受到的保护策略。有关该首部，请参阅本章之后的内容。





### 6.6 实体首部字段



#### 1. Allow

```http
Allow: GET, HEAD
```

首部字段 Allow 用于 **`通知客户端能够支持 Request-URI 指定资源的所有 HTTP 方法`** 。当服务器接收到不支持的 HTTP 方法时，会以状态码 **`405 Method Not Allowed`** 作为响应返回。与此同时，还会把所有能支持的 HTTP 方法写入首部字段 Allow 后返回。



#### 2. Content-Encoding

```http
Content-Encoding: gzip
```

首部字段 Content-Encoding 会告知客户端服务器对实体的主体部分选用的内容编码方式。内容编码是指在不丢失实体信息的前提下所进行的压缩。

* **`gzip`**
* **`compress`**
* **`deflate`**
* **`identity`**



#### 3. Content-Language

```http
Content-Language: zh-CN
```

首部字段 Content-Language 会告知客户端， **`实体主体使用的自然语言`**（指中文或英文等语言）。



#### 4. Content-Length

```http
Content-Length: 15000
```

首部字段 Content-Length 表明了 **`实体主体部分的大小（单位是字节）`** 。对实体主体进行内容编码传输时，不能再使用 Content-Length 首部字段。由于实体主体大小的计算方法略微复杂，所以在此不再展开。



#### 5. Content-Location

```http
Content-Location: http://www.hackr.jp/index-ja.html
```

首部字段 Content-Location 给出与 **`报文主体部分相对应的 URI`** 。和首部字段 Location 不同，Content-Location 表示的是 **`报文主体返回资源对应的 URI`** 。比如，对于使用首部字段 Accept-Language 的服务器驱动型请求，当返回的页面内容与实际请求的对象不同时，首部字段 Content-Location 内会写明 URI。



#### 6. Content-MD5

```http
Content-MD5: OGFKZDUwNGVHNGY3N2MxMDIwZmQ4NTBmY2IyTY==
```



#### 7. Content-Range

```http
Content-Range: bytes 5001-10000/10000
```

针对范围请求，返回响应时使用的首部字段 Content-Range，能告知客户端作为响应返回的实体的 **`哪个部分符合范围请求`** 。字段值以 **`字节`** 为单位，表示当前发送部分及整个实体大小。



#### 8. Content-Type

```http
Content-Type: text/html; charset=UTF-8
```

首部字段 Content-Type 说明了实体主体内对象的媒体类型。和首部字段 Accept 一样，字段值用 type/subtype 形式赋值。参数 charset 使用 iso-8859-1 或 euc-jp 等字符集进行赋值。



#### 9. Expires

```http
Expires: Wed, 04 Jul 2012 08:26:05 GMT
```

首部字段 Expires 会将 **`资源失效的日期告知客户端`** 。缓存服务器在接收到含有首部字段 Expires 的响应后，会以缓存来应答请求，在 Expires 字段值指定的时间之前，响应的副本会一直被保存。 **`当超过指定的时间后，缓存服务器在请求发送过来时，会转向源服务器请求资源`** 。源服务器不希望缓存服务器对资源缓存时，最好在 Expires 字段内写入与首部字段 Date 相同的时间值。但是，当首部字段 Cache-Control 有指定 max-age 指令时，比起首部字段 Expires，会优先处理 **`max-age`** 指令。



#### 10. Last-Modified

```http
Last-Modified: Wed, 23 May 2012 09:59:55 GMT
```

首部字段 Last-Modified 指名 **`资源最终修改的时间`** 。一般来说，这个值就是 Request-URI 指定资源被修改的时间。但类似使用 CGI 脚本进行动态数据处理时，该值有可能会变成数据最终修改时的时间。





### 6.7 为 Cookie 服务的首部字段

下面的表格内列举了与 Cookie 有关的首部字段。

* **`为 Cookie 服务的首部字段`**

| 首部字段名 | 说明                             | 首部类型     |
| ---------- | -------------------------------- | ------------ |
| Set-Cookie | 开始状态管理所使用的 Cookie 信息 | 响应首部字段 |
| Cookie     | 服务器接收到的 Cookie 信息       | 请求首部字段 |



#### 1. Set-Cookie

```                                                                                                                                                                         http
Set-Cookie: status=enable; expires=Tue, 05 Jul 2011 07:26:31 GMT; => path=/;domain=.hackr.jp;
```

当服务器准备开始管理客户端的状态时，会事先先告知各种信息。下面的表格列举了 Set-Cookie 的字段值。

* **`Set-Cookie 字段的属性`**

| 属性         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| NAME=VALUE   | 赋予 Cookie 的名称和其值（必需项）                           |
| expires=DATE | Cookie 的有效期（若不明确指定则默认为浏览器关闭前为止）      |
| path=PATH    | 将服务器上的文件目录作为 Cookie 的适用对象（若不指定则默认为文档所在的文件目录） |
| domain=域名  | 作为 Cookie 适用对象的域名（若不指定则默认为创建 Cookie 的服务器的域名） |
| Secure       | 仅在 HTTPS 安全通信时才会发送 Cookie                         |
| HttpOnly     | 加以限制，使 Cookie 不能被 JavaScript 脚本访问               |



**`expires 属性`**

Cookie 的 expires 属性指定浏览器可发送 Cookie 的有效期。当省略 expires 属性时，其有效期仅限于维持浏览器会话（Session）时间段内。这通常限于浏览器应用程序被关闭之前。另外，一旦 Cookie 从服务器发送至客户端，服务器端就不存在可以显式删除 Cookie 的方法。但可通过覆盖已过期的 Cookie，实现对客户端 Cookie 的实质性删除操作。



**`path 属性`**

Cookie 的 path 属性可用于限制指定 Cookie 的发送范围的文件目录。不过另有方法可避开这项限制，看来对其作为安全机制的效果不能抱有期待。



**`domain 属性`**

通过 Cookie 的 domain 属性指定的域名可做到与结尾匹配一致。比如，当指定 example.com 后，除 example.com 以外，**`www.example.com`** 或 **`www2.example.com`** 等都可以发送 Cookie。因此，除了针对具体指定的多个域名发送 Cookie 之外，不指定 domain 属性显得更安全。



**`secure 属性`**

Cookie 的 secure 属性用于限制 Web 页面仅在 HTTPS 安全连接时，才可以发送 Cookie。发送 Cookie 时，指定 secure 属性的方法如下所示。

```http
Set-Cookie: name=value; secure
```

以上例子仅当在 **`https://www.example.com/`**（HTTPS）安全连接的情况下才会 **`进行 Cookie 的回收`** 。也就是说，即使域名相同，**`http://www.example.com`**（HTTP）也不会发生 Cookie 回收行为。当省略 secure 属性时，不论 HTTP 还是 HTTPS，都会对 Cookie 进行回收。



**`HttpOnly 属性`**

Cookie 的 HttpOnly 属性是 **`Cookie 的扩展功能`** ， **`它使 JavaScript 脚本无法获得 Cookie`** 。其主要目的 **`为防止跨站脚本攻击（XSS）对 Cookie 的信息窃取`** 。发送指定 HttpOnly 属性的 Cookie 的方法如下所示。

```http
Set-Cookie: name=value; HttpOnly
```

通过上述设置，通常从 Web 页面内还可以对 Cookie 进行读取操作。但使用 JavaScript 的 document.cookie 就无法读取附加 HttpOnly 属性后的 Cookie 的内容了。因此，也就无法在 XSS 中利用 JavaScript 劫持 Cookie 了。虽然是独立的扩展功能，但 Internet Explorer 6 SP1 以上版本等当下的主流浏览器都已经支持该扩展了。另外顺带一提，该扩展并非是为了防止 XSS 而开发的。



#### 2. Cookie

```http
Cookie: status=enable
```

首部字段 Cookie 会告知服务器，当客户端想获得 HTTP 状态管理支持时，就会在 **`请求中包含从服务器接收到的 Cookie`** 。接收到多个 Cookie 时，同样可以以多个 Cookie 形式发送。





### 6.8 其他首部字段

HTTP 首部字段是可以自行扩展的。所以在 Web 服务器和浏览器的应用上，会出现各种非标准的首部字段。接下来，我们就一些最为常用的首部字段进行说明。

* **`X-Frame-Options`**
* **`X-XSS-Protection`**
* **`DNT`**
* **`P3P`**



#### 1. X-Frame-Options

```http
X-Frame-Options: DENY
```

首部字段 X-Frame-Options 属于 **`HTTP 响应首部`** ，用于 **`控制网站内容在其他 Web 网站的 Frame 标签内的显式问题`** 。其主要目的是 **`为了防止点击劫持攻击`** 。首部字段 X-Frame-Options 有以下两个可指定的字段值。



* **`DENY`**：拒绝
* **`SAMEORIGIN`**：仅同源域名下的页面匹配时许可。



#### 2. X-XSS-Protection

```http
X-XSS-Protection: 1
```

首部字段 X-XSS-Protection 属于 **`HTTP 响应首部`** ，它是 **`针对跨站脚本攻击（XSS）的一种对策，用于控制浏览器 XSS 防护机制的开关`** 。首部字段 X-XSS-Protection 可指定的字段值如下。

* 0：将 XSS 过滤设置成无效状态
* 1：将 XSS 过滤设置成有效状态



#### 3. DNT

```http
DNT: 1
```

首部字段 DNT 属于 **`HTTP 请求首部`** ，其中 DNT 是 Do Not Track 的简称，意为 **`拒绝个人信息被收集`** ，是表示 **`拒绝被精准广告追踪的一种方法`** 。首部字段 DNT 可指定的字段值如下。

* 0：同意被追踪
* 1：拒绝被追踪



由于首部字段 DNT 的功能具备有效性，所以 Web 服务器需要对 DNT 做对应的支持。



#### 4. P3P

```http
P3P: CP="CAO DSP LAW CURa ADMa DEVa TAIa PSAa PSDa" => IVAa IVDa OUR BUS IND UNI COM NAV INT"
```

首部字段 P3P 属于 **`HTTP 响应首部`** ，通过利用 P3P 技术，可以让 **`Web 网站上的个人隐私变成一种仅供程序可理解的形式，以达到保护用户隐私的目的`** 。要进行 P3P 的设定，需按以下操作步骤进行。

步骤 1：创建 P3P 隐私

步骤 2：创建 P3P 隐私对照文件后，保存命名在 /w3c/p3p.xml

步骤 3：从 P3P 隐私中新建 Compact policies 后，输出到 HTT P 响应中

















