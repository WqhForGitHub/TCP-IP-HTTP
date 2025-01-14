### 2.1 HTTP 协议用于客户端和服务器端之间的通信

​                                                                                                                                                                                                                                     







### 2.2 HTTP 是不保存状态的协议

 



### 2.3 HTTP 是不保存状态的协议





### 2.4 请求 URI 定位资源







### 2.5 告知服务器意图的 HTTP 方法

下面，我们介绍 HTTP/1.1 中可使用的方法。



* **`GET: 获取资源`**

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter2/get.png?raw=true)



**使用 GET 方法的请求 响应的例子**

| 请求                                                    | 响应                       |
| ------------------------------------------------------- | -------------------------- |
| GET /index.html HTTP/1.1 <br />Host: **`www.hackr.jp`** | 返回 index.html 的页面资源 |

| 请求                                                         | 响应                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| GET /index.html HTTP/1.1 <br />Host: **`www.hackr.jp`** <br />If-Modified-Since: Thu, 12 Jul 2012 07:30:00 GMT | 仅返回 2012 年 7 月 12 日 7 点 30 分以后更新过的 index.html 页面资源。如果未有内容更新，则以状态码 304 Not Modified 作为响应返回 |



* **`POST: 传输实体主体`**

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter2/post.png?raw=true)



**使用 POST 方法的请求 响应的例子**

| 请求                                                         | 响应                               |
| ------------------------------------------------------------ | ---------------------------------- |
| POST /submit.cgi HTTP/1.1 <br />Host: **`www.hackr.jp`** <br/>Content-Length: 1560（1560 字节的数据） | 返回 submit.cgi 接收数据的处理结果 |



* **`PUT: 传输文件`**

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter2/put.png?raw=true)	



**使用 PUT 方法的请求 响应的例子**

| 请求                                                         | 响应                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| PUT /example.html HTTP/1.1 <br />Host: **`www.hackr.jp`** <br />Content-Type: text/html <br />Content-Length: 1560（1560 字节的数据） | 响应返回状态码 204 No Content（比如：该 html 已存在于服务器上） |

   

* **`HEAD: 获得报文首部`**

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter2/head.png?raw=true)	



**使用 HEAD 方法的请求 响应的例子**

| 请求                                                     | 响应                           |
| -------------------------------------------------------- | ------------------------------ |
| HEAD /index.html HTTP/1.1 <br />Host: **`www.hackr.jp`** | 返回 index.html 有关的响应首部 |



* **`DELETE: 删除文件`**



![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter2/delete.png?raw=true)

**使用 DELETE 方法的请求 响应的例子**

| 请求                                                         | 响应                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| DELETE /example.html HTTP/1.1 <br />Host: **`www.hackr.jp`** | 响应返回状态码 204 No Content（比如：该 html 已从服务器上删除） |



* **`OPTIONS: 询问支持的方法`**

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter2/options.png?raw=true)	





**使用 OPTIONS 方法的请求 响应的例子**

| 请求                                              | 响应                                                         |
| ------------------------------------------------- | ------------------------------------------------------------ |
| OPTIONS * HTTP/1.1 <br />Host: **`www.hackr.jp`** | HTTP/1.1 200 OK <br />Allow: GET, POST, HEAD, OPTIONS <br />（返回服务器支持的方法） |



* **`TRACE: 追踪路径`**

  

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter2/trace.png?raw=true)



**使用 TRACE 方法的请求 响应的例子**

| 请求                                                        | 响应                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| TRACE / HTTP/1.1 <br />Host: hackr.jp <br />Max-Forwards: 2 | HTTP/1.1 200 OK <br />Content-Type: message/http <br />Content-Length: 1024 <br /> <br />TRACE / HTTP/1.1 <br />Host: hackr.jp <br />Max-Forwards: 2（返回响应包含请求内容） |





* **`CONNECT: 要求用隧道协议连接代理`**

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter2/connect.png?raw=true)	



**使用 CONNECT 方法的请求 响应的例子**

| 请求                                                         | 响应                                |
| ------------------------------------------------------------ | ----------------------------------- |
| CONNECT proxy.hackr.jp:8080 HTTP/1.1 <br />Host: proxy.hackr.jp | HTTP/1.1 200 OK（之后进入网络隧道） |





### 2.6 使用方法下达命令



**HTTP/1.0 和 HTTP/1.1 支持的方法**

| 方法    | 说明                   | 支持的 HTTP 协议版本 |
| ------- | ---------------------- | -------------------- |
| GET     | 获取资源               | 1.0、1.1             |
| POST    | 传输实体主体           | 1.0、1.1             |
| PUT     | 传输文件               | 1.0、1.1             |
| HEAD    | 获得报文首部           | 1.0、1.1             |
| DELETE  | 删除文件               | 1.0、1.1             |
| OPTIONS | 询问支持的方法         | 1.1                  |
| TRACE   | 追踪路径               | 1.1                  |
| CONNECT | 要求用隧道协议连接代理 | 1.1                  |
| LINK    | 建立和资源之间的联系   | 1.0                  |
| UNLINK  | 断开连接关系           | 1.0                  |



### 2.7 持久连接节省通信量

 

#### 1. 持久连接



#### 2. 管线化





### 2.8 使用 Cookie 的状态管理

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter2/cookie.png?raw=true)



* **`没有 Cookie 信息状态下的请求`**

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter2/noCookie.png?raw=true)

* **`第 2 次以后（存有 Cookie 信息状态）的请求`**



![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter2/secondCookie.png?raw=true)





1. **`请求报文（没有 Cookie 信息的状态）`**

```http
GET /reader/ HTTP/1.1
Host: hackr.jp

*首部字段内没有 Cookie 的相关信息
```



2. **`响应报文（服务器端生成 Cookie 信息）`**

```http
HTTP/1.1 200 OK
Date: Thu, 12 Jul 2012 07:12:20 GMT
Server: Apache
<Set-Cookie: sid=1342077140226724; path=/; expires=Wed, 10-Oct-12 07:12:20 GMT>
Content-Type: text/plain; charset=UTF-8
```



3. **`请求报文（自动发送保存着的 Cookie 信息）`**

```http
GET /image/ HTTP/1.1 
Host: hackr.jp
Cookie: sid=1342077140226724
```



​	