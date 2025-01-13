

### 4.1 状态码告知从服务器端返回的请求结果

* **`状态码的类别`**

|      | 类别                             | 原因短语                   |
| ---- | -------------------------------- | -------------------------- |
| 1XX  | Informational（信息性状态码）    | 接收的请求正在处理         |
| 2XX  | Success（成功状态码）            | 请求正常处理完毕           |
| 3XX  | Redirection（重定向状态码）      | 需要进行附加操作以完成请求 |
| 4XX  | Client Error（客户端错误状态码） | 服务器无法处理请求         |
| 5XX  | Server Error（服务器错误状态码） | 服务器处理请求出错         |



### 4.2 2XX 成功

2XX 的响应结果表明 **`请求被正常处理了`** 。



#### 1. 200 OK

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter4/200.png?raw=true)

表示从客户端发来的请求在服务器端被正常处理了。在响应报文内，随状态码一起返回的信息会因方法的不同而发生改变。比如，使用 GET 方法时，对应请求资源的实体会作为响应返回；而使用 **`HEAD`** 方法时，对应请求资源的实体主体不随报文首部作为响应返回（即 **`在响应中只返回首部，不会返回实体的主体部分`** ）。                                                                                                                                                                                                                                                                                                                                       



#### 2. 204 No Content

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter4/204.png?raw=true)

该状态码代表服务器接收的请求已成功处理，但在 **`返回的响应报文中不含实体的主体部分`** 。另外，也不允许返回任何实体的主体。比如，当从浏览器发出请求处理后，返回 204 响应，那么浏览器显示的页面不发生更新。 **`一般在只需要从客户端往服务器发送信息，而对客户端不需要发送新信息内容的情况下使用`** 。



#### 3. 206 Partial Content

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter4/206.png?raw=true)

该状态码表示客户端进行了 **`范围请求`** ，而服务器成功执行了这部分的 GET 请求。响应报文中包含由 **`Content-Range 指定范围的实体内容`** 。



### 4.3 3XX 重定向

3XX 响应结果表明浏览器需要执行某些特殊的处理以正确处理请求。



#### 1. 301 Moved Permanently

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter4/301.png?raw=true)

**`永久性重定向`** 。该状态码表示 **`请求的资源已被分配了新的 URI`** ，以后应使用资源现在所指的 URI。也就是说，如果已经把资源对应的 URI 保存为书签了，这时应该按 **`Location 首部字段提示的 URI 重新保存`** 。像下方给出的请求 URI，当指定资源路径的最后忘记添加斜杠 **`"/"`** ，就会产生 301 状态码。

```http
http://example.com/sample
```



#### 2. 302 Found

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter4/302.png?raw=true)

**`临时性重定向`** 。该状态码表示 **`请求的资源已被分配了新的 URI，希望用户（本次）能使用新的 URI 访问`** 。和 301 Moved Permanently 状态码相似，但 302 状态码代表的资源不是被永久移动，只是临时性质的。换句话说，已移动的资源对应的 URI 将来还有可能发生改变。比如，用户把 URI 保存成书签，但不会像 301 状态码出现时那样去更新书签，而是仍旧保留返回 302 状态码的页面对应的 URI。



#### 3. 303 See Other

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter4/303.png?raw=true)

该状态码表示由于 **`请求对应的资源存在着另一个 URI，应使用 GET 方法定向获取请求的资源`** 。303 状态码明确表示客户端应当采用 GET 方法获取资源，这点与 302 状态码有区别。比如，当使用 POST 方法访问 CGI 程序，其执行后的处理结果是希望客户端能以 GET 方法重定向到另一个 URI 上去时，返回 303 状态码。虽然 302 Found 状态码也可以实现相同的功能，但这里使用 303 状态码是最理想的。



#### 4. 304 Not Modified

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter4/304.png?raw=true)

该状态码表示 **`客户端发送附带条件的请求时`** ，服务器端允许请求访问资源，但因 **`发生请求未满足条件的情况后，直接返回 304 Not Modified（服务器端资源未改变，可直接使用客户端未过期的缓存）`** 。304 状态码返回时， **`不包含任何响应的主体部分`** 。304 虽然被划分在 3XX 类别中，但是和重定向没有关系。



#### 5. 307 Temporary Redirect



**`临时性重定向`** 。该状态码与 302 Found 有着相同的含义。尽管 302 标准禁止 POST 变换成 GET，但实际使用时大家并不遵守。 **`307 会遵照浏览器标准，不会从 POST 变成 GET`** 。但是，对于处理响应时的行为，每种浏览器有可能出现不同的情况。       



### 4.4 4XX 客户端错误

4XX 的响应结果表明客户端是发生错误的原因所在。



#### 1. 400 Bad Request

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter4/400.png?raw=true)

该状态码表示请求报文中存在 **`语法错误`** 。当错误发生时， **`需修改请求的内容后再次发送请求`** 。另外，浏览器会像 200 OK 一样对待该状态码。   



#### 2. 401 Unauthorized

该状态码表示发送的请求 **`需要有通过 HTTP 认证（BASIC 认证、DIGEST 认证）的认证信息`** 。另外若之前已进行过 1 次请求，则表示用户认证失败。返回含有 401 的响应必须包含一个适用于被请求资源的 **`WWW-Authenticate 首部用以质询（challenge）用户信息`** 。当浏览器初次接收到 401 响应，会弹出认证用的对话窗口。



#### 3. 403 Forbidden

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter4/403.png?raw=true)

该状态码表明对 **`请求资源的访问被服务器拒绝了`** 。服务器端没有必要给出拒绝的详细理由，但如果想作说明的话，可以在实体的主体部分对原因进行描述，这样就能让用户看到了。未获得文件系统的访问授权，访问权限出现某些问题（从未授权的发送源 IP 地址试图访问）等列举的i情况都可能是发生 403 的原因。



#### 4. 404 Not Found

该状态码表明 **`服务器上无法找到请求的资源`** 。除此之外，也可以在服务器端拒绝请求且不想说明理由时使用。



### 4.5 5XX 服务器错误

5XX 的响应结果表明服务器本身发生错误。



#### 1. 500 Internal Server Error

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter4/500.png?raw=true)

该状态码表明 **`服务器端在执行请求时发生了错误`** 。也有可能是 **`Web 应用存在的 bug 或某些临时的故障`** 。



#### 2. 503 Service Unavailable

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter4/503.png?raw=true)

该状态码表明 **`服务器暂时处于超负载或正在进行停机维护 ，现在无法处理请求`** 。如果事先得知解除以上状况需要的时间，最好写入 **`Retry-After 首部字段`** 再返回给客户端。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              

