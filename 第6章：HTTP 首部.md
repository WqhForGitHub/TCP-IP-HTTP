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

当指定 private 指令后，响应只以特定的用户作为对象，这与 public 指令的行为相反。缓存服务器会对该特定用户提供资源缓存的服务，对于其他用户发送过来的请求，代理服务器则不会返回缓存。





