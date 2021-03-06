# network-protocol
***
## TCP/IP 协议  
参考：《图解TCP/IP 协议》
***
### 计算机网络结构层  
  
层次|名称  |功能|
----|----|---|
 7| 应用层 | 针对特定应用的协议|
6 | 表示层  | 设备固有数据格式和网络标准数据格式的转换 |
5 | 会话层 | 通信管理。负责建立和断开通信连接，管理传输层以下分层|
 4| 传输层  |管理两个节点间的数据传输，负责可靠传输  |
3 | 网络层  | 地址管理与路由选择 |
2 | 数据链路层 | 互联设备之间传送和识别数据帧 |
1 |  物理层 |   界定连接器和网线规格|
---

MAC地址：设备物理地址，无层次性，地址转发表  
IP地址：网络地址，有层次性，路由控制表

---

### 网络层协议：

IP协议：IP地址作为主机的标识，分组交换的一种协议，但是不具有重发机制，属于非可靠传输协议。   
ICMP协议：ip数据包发送途中发生异常，需要发送一个异常通知。用于诊断网络的健康状况。  
ARP协议：从分组数据包的IP地址中解析出MAC地址的协议。  

---

### 传输层协议：
TCP协议：面向有链接的传输协议，可靠传输协议。  
UDP协议：面向无链接的传输协议，不可靠传输协议。

---

### 应用层协议：
http协议：互联网协议  
SMTP协议：邮件协议  
FTP协议：文件传输协议

---

### MAC地址转发表:  

例如从主机A（端口A）发送数据到主机B（端口B）：  
1.从源MAC地址可知，主机A与交换机端口A  
2.交换机获取其他连接主机的MAC地址  
3.获取的MAC地址中存在端口B  
4.主机A过端口A转发到端口B，主机B接受到数据  

---

### 环路检测  
1.生成树方式  
2.源路由方式

---
### IP协议
1.面向无连接  
2.(ipv4)32位正整数表示，分为4组  

ip地址=网络标识(网络地址)+主机标识(主机地址)  
例如IP：192.169.128(网络地址).10(主机地址)

分类|网络地址  |主机地址|
----|----|---|
A类| 0.0.0.0~127.0.0.0 | 后24位|
B类| 128.0.0.1~191.255.0.0  | 后 16位|
C类 | 192.168.0.0~239.255.255.0 | 后8位|
D类 | 224.0.0.0~239.255.255.255 |无 |

路由控制：最长匹配原则  

DNS:域名系统，解析域名  
ARP:地址解决协议，获取MAC地址  
ICMP:控制报文协议，检查网络是否可达  
DHCP:动态主机配置协议,自动设置IP
NAT:网络地址转换，实现内网和互联网通信，有效缓解了IPV4地址的耗尽  

---

### TCP与UDP  

TCP | UDP|
---|---|
 面向连接的，可靠的流协议|面向无连接的，不可靠数据报协议  |

识别一个通信：源IP地址、目标IP地址、协议号、源端口号、目标端口号。  
只要其中有一个不同，就不是同一个通信  
#### 常见端口号

端口号 | 服务
---|---
21 | ftp
22 | ssh
25 | smtp
80 | http
443 | https
515 | printer
</br>
tcp连接建立：主机A与主机B连接(三次握手，四次挥手)  


过程| 动作
---|---
A->B| SYN(请求建立连接)
B->A |ACK(针对SYN的确认应答)，SYN(请求建立连接)
A->B |ACK(针对SYN的确认应答)，连接建立完成发送数据
A->B |FIN(请求切断连接)
B->A |ACK(针对FIN的确认应答)
B->A |FIN(请求切断连接)
A->B |ACK(针对FIN的确认应答)  

---

### 路由协议 
静态路由：人工设置  
动态路由：协议控制  


路由算法：距离向量算法、链路状态算法  
RIP：路由信息协议，基于距离矢量算法的路由协议，利用跳数来作为计量标准。

OSPF:链路状态型路由协议，出现环路也能稳定控制路由。

---

http协议状态  

状态 | 动作
---|---
信息提供 |
100 | continue
101 | switching protocols
肯定应答| 
200 | OK
201 | Created
202 | Accept
203 | Non-Authoritative info
204 | No Content
205 | Reset Content
206 | Partial Content
重定向请求|
300 | Multiple Choices
301 | Moved Permanently
302 | Move temporarily
303 | See Other
304 | Not Modified
305 | Use Proxy
请求错误|
400 | Bad Request
401 | Unauthorized
402 | Payment Required
403 | Forbidden
404 | Not Found
405 | Method Not Allowed
406 | Not Acceptable
407 | Proxy Authentication Required
408 | Request Timeout
409 | Conflict
410 | Gone
411 | Length Required
412 | Precondition Failed
413 | Request Entity Too Large
414 | Request-URI Too Long
415 | Unsupported Media Type
服务器错误|
500 | Internal Server Error
501 | Not Implemented
502 | Bad Gateway
503 | Service Unavailable
504 | Gateway Timeout
505 | Http Version Not Supported
600 | Unparseable Response Headers
----
## HTTP协议  
参考:《图解HTTP》 

----
HTTP：超文本传输协议  
访问一个页面，例如 www.a.com  

流程 | 动作
---|---
客户端->DNS服务器| 请求www.a.com的IP地址
DNS->客户端 | 返回请求的IP地址
客户端->服务端| HTTP请求报文</br>TCP将请求报文可靠发送给对方</br>IP协议，搜索地址，中转和传送</br>TCP收到请求报文，重组报文</br>HTTP处理请求的web内容
服务端->客户端|同上回传

</br>
URI：统一资源标识符  

URL：统一资源定位符  
</br>
绝对URI格式：  
http://user:pass@www.a.com:80/dir/index.html?uid=1#ch1

字符 | 内容
---|---
http | 协议方案名
user:pass | 登陆信息(认证)
www.a.com | 服务器地址
80 | 服务端口号
/dir/index.html | 带层次的文件路径
uid=1 | 查询字符串
ch1| 片段标识符

---
请求报文：请求方法+请求URI+协议版本+可选的请求首部字符+内容实体  
</br>

POST 　　  /form/entry　　      HTTP/1.1  
Host:a.com  
Connection:keep-alive  
Content-Type:application/x-www-form-urlencoded  
Content-Length:16  
name=Alice&age=13  

响应报文：协议版本+状态码+原因短语+可选的响应首部字段+实体主体  
</br>
HTTP/1.1　　200　ok  
Date: Tue ,10 Jul 2017 06:50:15 GMT  
Content-Length:362  
Content-Type:text/html  


---

### HTTP方法  

GET：用来请求访问已经被URI识别的资源  
请求：GET/index.html　HTTP/1.1  
响应：返回index.html的页面资源  

---

POST：传输实体的主体  
请求:POST/submit.cgi　HTTP/1.1  
　　 Host:www.a.com  
　　 Content-Length:1560  
响应:返回submit.cgi接受数据的处理结果

---


PUT：传输文件，一般不用  

---

HEAD:获取报文首部，不返回报文主体部分，用于确认URI有效性等  
请求:HEAD/index.html　HTTP/1.1  
　　HOST：www.a.com  
响应:返回index.html有关响应的首部

---

DELETE：删除文件，一般不用  

---

OPTIONS:询问支持的方法  
请求：OPTIONS*HTTP/1.1  
　　　HOST:www.a.com  
响应:HTTP/1.1 200 ok  
　　Allow:GET,POST,HEAD,OPTIONS  
　　返回服务器支持的方法  

---

TRACE:追踪路径，一般不用  

---
CONNECT：使用隧道协议连接代理  

---

### Cookie  
HTTP是无状态协议，为了保存用户状态引入了Cookie  

请求报文(无Cookie信息的状态)  
GET/reader/HTTP/1.1  
HOST:a.com  


响应报文(服务端生成了Cookie信息)  
HTTP/1.1 200 OK  
Date：Thu，12，Jul 2012 07:12:20 GMT  
Server:Apache  
<Set-Cookie:sid=12331444141; path=/; expires=Wed,10-Oct-12 07:12:20 GMT>  
Content-Type:text/plain;charset=UTF-8


请求报文(自动发送保存的Cookie信息)  
GET/image/HTTP/1.1  
HOST:a.com  
Cookie:sid=1232312312312  

---
### HTTP报文  

 名称| 作用
---|---
报文首部 | 服务端或客户端需处理的请求或响应的内容及属性
空行(CR+LF) | 回车符和换行符
报文主体 | 应被发送的数据


</br>

报文结构
请求报文 | 响应报文
---|---
请求行  | 状态行
请求首部字段 |响应首部字段
通用首部字段 |通用首部字段
实体首部字段 |实体首部字段
其他 |其他

请求行：包含请求方法，请求URI和HTTP版本  

状态行：包含表面响应结果的状态码，原因短语和HTTP版本  

首部字段：包含表示请求和响应的各种条件和属性的各类首部，通用首部、请求首部、响应首部、实体首部  

其他：可能包含HTTP的RFC里未定义的首部(Cookie等)

---
### HTTP状态码  

名称 | 类别| 原因短语
---|---|---  
1XX | informational(信息性状态码)| 接收的请求正在处理
2XX | Success(成功状态码)| 请求正常处理完毕
3XX | Redirection(重定向状态码)| 需要进行附加操作完成请求
4XX | Client Error(客户端错误状态码)| 服务器无法处理请求
5XX | Server Error(服务器错误状态码)| 服务器处理请求出错  


</br>

通用首部字段 | 说明
---|---
Cache-Control | 控制缓存行为
Connection| 逐跳首部、连接管理
Date | 创建报文的日期时间
Pragma | 报文指令
Trailer | 报文末端的首部一览
Transfer-Encoding | 指定报文主体的传输编码方式
Upgrade | 升级为其他协议
Via | 代理服务器相关信息
Wanring | 错误通知

</br>

请求首部字段 | 说明
---|---
Accept | 用户代理可处理的媒体类型
Accept-Charset | 优先字符集
Accept-Language | 优先语言
Authorization | Web认证信息
Expert | 服务器的特定行为
From |  用户的电子邮箱地址
 Host|请求资源所在的服务器
 Proxy-Authoriztation | 代理服务器要求客户端的认证信息
 User-Agent | HTTP客户端程序信息
 
 </br>
 

响应首部字段 | 说明
---|---
Accept-Ranges | 是否接受字节范围请求
Age | 推算资源创建经过的时间
Location | 令客户端重定向至指定URI
Proxy-Authenticate |代理服务器对客户端的认证信息
Retry-After |   对再次发起请求的时机要求
Server | HTTP服务器的安装信息
Vary | 代理服务器的缓存管理信息
 WWW-Authenticate|  服务器对客户端的认证信息 
 
 
 </br>
 

实体首部字段 | 说明
---|---
Allow | 资源可支持的HTTP方法
Content-Encoding | 实体主体适用的编码方式
Content-Language | 实体主体的自然语言 
Content-Length | 实体主体的大小(字节)
 Contnet-MD5|实体主体的报文摘要
  Content-Range|    实体主体的位置范围
  Content-Type |    实体主体的媒体类型
   Expires|实体主体过期日期
Last-Moidfied    |资源最后的修改的日期 


</br>

### Cookie
网景公司开发定义的标准


首部字段名 | 说明| 首部类型
---|---|---
Set-Cookie | 开始状态管理所使用的Cookie信息| 响应首部字段
Cookie | 服务器接收到的Cookie信息| 请求首部字段

Set-Cookie实例:  
```
Set-Cookie:status=enbale,expires=Tur,05 Jul 2017 07:01:23 GMT;  path=/;domin=.a.com;
```

Set-Cookie字段属性  

属性 | 说明
---|---
NAME=VALUE | 赋予Cookie的名称和其值(必需项)
exoires=DATE | Cookie的有效期(默认为浏览器关闭为止)
path=PATH |将服务器上的文件目录作为Cookie的适用对象(默认为文档所在目录) 
 domain=域名|作为Cookie适用对象的域名(默认为创建Cookie的服务器域名)
 Secure | 仅在HTTPS安全通信时才会发送Cookie
 HttpOnly|加以限制，使Cookie不能被javascrip脚本访问
 
 ---
 
 ### HTTPS
 
 HTTP缺点：  
 1.通信使用明文，内容可能被窃听  
 ```
 对应方案：  
 1.通信加密，使用SSL(安全套接层)和TLS(安全传输协议)  
 2.内容加密，报文主体加密  
 ```
 
 2.不验证通信方的身份，因此有可能遭遇伪装
 ```
 .无法确定请求发送至目标的web服务器是否是按真实意图返回响应的那台服务器。有可能是已伪装的Web服务器
 .无法确定响应返回的客户端是否为真的客户端。有可能为伪装的客户端。
 .无法确定正在通信的对方是否具备访问权限。
 .无法判定请求来自哪里。
 .即使无意义的访问也接收。无法阻止DDOS攻击。
 
 对应方案：
 1.使用SSL证书
 ```
 
 
 3.无法证明报文的完整性，可能被篡改  
 ```
 .接收的内容可能有误，可能遭遇中间人攻击(MITM)
 
 对应方案：
 1.使用MD5和SHA-1等散列值校验法
 ```
 
完整的解决方案：  
HTTP+加密+认证+完整保护=HTTPS  
特点：
1.HTTPS采用混合加密机制，使用共享密钥和公开密钥加密(CA证书认证)  


---

### 确认用户身份认证
HTTP认证方式：
1.BASIC认证(基本认证)
2.DIGEST认证(摘要认证)
3.SLL客户端认证
4.FormBase认证(基于表单认证)
 
 

一般为基于表单认证，比如：邮箱登陆验证

HTTP为无状态协议，使用Cookie来管理Session
```
客户端->服务器     发送已登陆的信息
服务器->客户端     向用户发放Session ID，记录认证状态
客户端->服务器     发送包含Session ID的Cookie，服务器验证接收的Session ID
```












