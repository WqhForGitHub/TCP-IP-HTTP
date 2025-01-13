### 3.1 HTTP 报文

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter3/HTTPMessageStructure.png?raw=true)



HTTP 报文大致可分为 **`报文首部`** 和 **`报文主体`** 两块。两者由最初出现的 **`空行（CR+LF）`** 来划分。通常，并不一定要有报文主体。





### 3.2 请求报文及响应报文的结构

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter3/MessageStructure.png?raw=true)



* **`请求行`**

​	包含用于请求的方法，请求 URI 和 HTTP 版本。

* **`状态行`**

​	包含表明响应结果的状态码，原因短语和 HTTP 版本。

* **`首部字段`**

  包含表示请求和响应的各种条件和属性的各类首部。一般有 4 种首部，分别是：通用首部、请求首部、响应首部和实体首部。

* **`其他`**

  可能包含 HTTP 的 RFC 里未定义的首部（Cookie 等）。



### 3.3 编码提升传输速率



#### 1. 报文主体和实体主体的差异

* **`报文`**

  是 HTTP 通信中的基本单位，由 **`8 位组字节流组成`** ，通过 HTTP 通信传输。

* **`实体`**

  作为请求或响应的有效载荷数据被传输，其内容由 **`实体首部`** 和 **`实体主体`** 组成。

HTTP 报文的主体用于传输请求或响应的实体主体。通常， **`报文主体等于实体主体`** 。只有当传输中进行编码操作时，实体主体的内容会发生变化，才导致它和报文主体产生差异。



#### 2. 压缩传输的内容编码

常用的内容编码有以下几种。

* **`gzip（GNU zip）`**
* **`compress（UNIX 系统的标准压缩）`**
* **`deflate（zlib）`**
* **`identity（不进行编码）`**



#### 3. 分割发送的分块传输编码





### 3.4 发送多种数据的多部分对象集合

多部分对象集合包含的对象如下。

* **`multipart/form-data`**

  在 Web 表单文件上传时使用

* **`multipart/byteranges`**

​	状态码 206（Partial Content，部分内容）响应报文包含了多个范围的内容时使用。

* **`multipart/form-data`**

  ```http
  Content-Type: multipart/form-data; boundary=AaB03x
  
  --AaB03x
  Content-Dispposition: form-data; name="field1"
  
  Joe Blow
  --AaB03x
  Content-Disposition: form-data; name="pics"; filename="file1.txt"
  Content-Type: text/plain
  
  ...（file1.txt 的数据）...
  --AaB03x--
  ```

* **`multipart/byteranges`**

  ```http
  HTTP/1.1 206 Partial Content
  Date: Fri, 13 Jul 2012 02:45:26 GMT
  Last-Modified: Fri, 31 Aug 2007 02:02:20 GMT
  Content-Type: multipart/byteranges; boundary=THIS_STRING_SEPARATES
  
  --THIS_STRING_SEPARATES
  Content-Type: application/pdf
  Content-Range: bytes 500-999/8000
  
  ...（范围指定的数据）...
  --THIS_STRING_SEPARATES
  Content-Type: application/pdf
  Content-Range: bytes 7000-7999/8000
  
  ...（范围指定的数据）...
  --THIS_STRING_SEPARATES
  ```



在 HTTP 报文中使用多部份对象集合时，需要在首部字段里加上 **`Content-Type`** 。有关这个首部字段，我们稍后讲解。使用 **`boundary 字符串`** 来划分多部分对象集合指明的各类实体。在 boundary 字符串指定的各个实体的起始行之前插入 "--" 标记（例如：--AaB03x、--THIS_STRING_SEPARATES），而在多部分对象集合对应的字符串的最后插入 "--" 标记（例如：--AaB03x、--THIS_STRING_SEPARATES）作为结束。多部分对象集合的每个部分类型中，都可以含有首部字段。另外，可以在某个部分中嵌套使用多部分对象集合。



### 3.5 获取部分内容的范围请求

![](https://github.com/WqhForGitHub/TCP-IP-HTTP/blob/%E5%9B%BE%E8%A7%A3HTTP/static/Chapter3/content-range.png?raw=true)



* **`5001 ~ 10000字节`**

  ```http
  Range: bytes=5001-10000
  ```

* **`从 5001 字节之后全部的`**

  ```http
  Range: bytes=5001-
  ```

* **`从一开始到 3000 字节和 5000 ~ 7000 字节的多重范围`**

  ```http
  Range: bytes=0-3000, 5000-7000                                                                                               
  ```



### 3.6 内容协商返回最合适的内容



