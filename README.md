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







