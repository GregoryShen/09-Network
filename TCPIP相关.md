# [硬不硬你说了算！近 40 张图解被问千百遍的 TCP 三次握手和四次挥手面试题](https://mp.weixin.qq.com/s/tH8RFmjrveOmgLvk9hmrkw)

## TCP 基本知识

### 瞧瞧 TCP 头格式

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS843ZPb6tFLvCVuXEn98khfs7y2KRvOV0ia5icVByzIK3aAKRURuVZKagsKw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />

<u>序列号</u>：在建立连接时由计算机生成的随机数作为其初始值，通过SYN包传给接收端主机，每发送一次数据，就累加一次该数据字节数大小。<u>用来解决网络包乱序问题。</u>

<u>确认应答号</u>：指下一次“期望” 收到的数据的序列号，发送端收到这个确认应答以后可以认为在这个序号以前的数据都已经被正常接收。<u>用来解决不丢包的问题。</u>

<u>控制位</u>：

* <u>ACK</u>：该位为1时，“确认应答” 的字段变为有效，TCP规定<u>除了最初建立连接时的 SYN 包之外该位必须设置为1.</u>
* <u>RST</u>：该位为1时，表示TCP连接中<u>出现异常必须强制断开连接</u>
* <u>SYN</u>：该位为1时，表示<u>希望建立连接，并在其“序列号”的字段进行序列号初始值的设定</u>
* <u>FIN</u>：该位为1时，表示<u>今后不会再有数据发送，希望断开连接。</u>当通信结束希望断开连接时，通信双方的主机就可以相互交换FIN位置为1的TCP段。

### 为什么需要 TCP 协议？TCP 工作在哪一层？

IP 层是“不可靠”的，它不保证网络包的交付、不保证网络包的按序交付、也不保证网络包中的数据的完整性。

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS843tzTAWL4l6rZB0pulNqkLno7buMqnh5Hlphn7aibB798ga1t3a0Dqmzg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />

如果需要保障网络数据包的可靠性，就需要由上层（传输层）的TCP协议来负责。

因为TCP是一个工作在**传输层**的**可靠**数据传输服务，它能确保接收端接收的网络包是**无损坏**、**无间隔**、**非冗余和按序**的。

### 什么是 TCP ？

TCP 是**面向连接的**、**可靠的**、**基于字节流**的传输层通信协议。

* 面向连接：一定是“一对一”才能连接，不能像UDP协议，可以一个主机同时向多个主机发送消息，也就是一对多是无法做到的
* 可靠的：无论在网络链路中出现了怎样的链路变化，TCP都可以保证一个报文一定能够到达接收端
* 字节流：消息是“没有边界”的，所以无论我们消息有多大都可以进行传输。并且消息是“有序的”，当前一个消息没有收到的时候，即使它先收到了后面的字节，也不能扔给应用层去处理，同时对重复的报文会自动丢弃。

### 什么是 TCP 连接？

我们来看看RFC 793 是如何定义“连接”的：

> Connections:
>
> The reliability and flow control mechanisms described above require that TCPs initialize and maintain certain status information for each data stream.
>
> The combination of this information, including sockets, sequence numbers, and window sizes, is called a connection.

简单来说就是，用于保证可靠性和流量控制维护的某些状态信息，这些信息的组合，包括Socket、序列号和窗口大小称为连接。

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS843wVoVXxKKTibcN9sLAuSgibkDfV2X8LH8eicpV1yAJ1uffibGqAuWShXibYg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />

所以我们可以知道，建立一个TCP连接是需要客户端与服务器端达成上述三个信息的共识。

* Socket：由IP地址和端口号组成
* 序列号：用来解决乱序问题等
* 窗口大小：用来做流量控制

### 如何唯一确定一个 TCP 连接呢？

TCP 四元组可以唯一地确定一个连接，四元组包括如下：

* 源地址
* 源端口
* 目标地址
* 目标端口

源地址和目的地址的字段（32位）是在IP头部中，作用是通过IP协议发送报文给对方主机。

源端口和目的端口字段（16位）是在TCP头部中，作用是告诉TCP协议应该把报文发给哪个进程。

### 有一个 IP 的服务器监听了一个端口，它的 TCP 的最大连接数是多少？

服务器通常固定在某个本地端口上监听，等待客户端的连接请求。因为，客户端IP和端口是可变的，其理论值计算公式如下：

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS843wBh1Ca3jpEqO0Xia0YzlicCgFdhLw8N4f0TCfglTwtxzecpECvmhBtEQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

对 IPv4, 客户端的IP数最多为2的32次方，客户端的端口数最多为2的16次方，也就是服务端单机最大TCP连接数约为2的48次方。

当然，服务端最大并发TCP连接数远不能达到理论上限。

* 首先主要是文件描述符限制，Socket都是文件，所以首先要通过 `ulimit` 配置文件描述符的数目
* 另一个是内存限制，每个TCP连接都要占用一定内存，操作系统是有限的。

### UDP 和 TCP 有什么区别呢？分别的应用场景是？

UDP 不提供复杂的控制机制，利用IP提供面向“无连接”的通信服务。

UDP协议真的非常简，头部只有8个字节（64位），UDP的头部格式如下：

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS8431Mymq2yPGjMPGodSEg8b31eoyQbibzGjDEHiaQUUDlbvCEwcXN3aicOTw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />

* 目标和源端口：主要是告诉UDP 协议应该把报文发给哪个进程
* 包长度：该字段保存了UDP首部的长度跟数据的长度之和
* 校验和：校验和是为了提供可靠的UDP首部和数据而设计

#### TCP和UDP区别

##### 连接

* TCP 是面向连接的传输层协议，传输数据前要先建立连接
* UDP 是不需要连接，即刻传输数据

##### 服务对象

* TCP 是一对一的两点服务，即一条连接只有两个端点
* UDP 支持一对一、一对多、多对多的交互通信

##### 可靠性

* TCP 是可靠交付数据的，数据可以无差错、不丢失、不重复、按需到达
* UDP 是尽最大努力交付，不保证可靠数据交付

##### 拥塞控制、流量控制

* TCP 有拥塞控制和流量控制机制，保证数据传输的安全性
* UDP 则没有，即使网络非常拥堵了，也不会影响 UDP 的发送速率。

##### 首部开销

* TCP 首部长度较长，会有一定的开销，首部在没有使用“选项”字段时是20个字节，如果使用了“选项”字段则会变长
* UDP 的首部只有8个字节，并且是固定不变的，开销较小

#### TCP和UDP应用场景

由于TCP是面向连接，能保证数据的可靠性交付，因此经常用于：

* FTP 文件传输
* HTTP / HTTPS

由于UDP面向无连接，它可以随时发送数据，再加上UDP本身的处理既简单又高效，因此经常用于：

* 包总量较少的通信，如DNS，SNMP 等
* 视频、音频等多媒体通信
* 广播通信

为什么 UDP 头部没有「首部长度」字段，而 TCP 头部有「首部长度」字段呢？

为什么 UDP 头部有「包长度」字段，而 TCP 头部则没有「包长度」字段呢？

## TCP 连接建立

### TCP 三次握手过程和状态变迁

TCP 是面向连接的协议，所以使用TCP前必须先建立连接，而建立连接是通过三次握手而进行的。

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS843fFol7gd3035Kibg3gPMSAZQLVibf9nwEblOUaX80hoOaRLVpaYCAI44w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

1. 一开始，客户端和服务端都处于 CLOSED 状态。显示服务端主动监听某个端口，处于LISTEN状态

	<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS843V0vbLBibXMvJbdiaqbfw4CictHX1Uc3OpOFWvZwxeI8B5Pv7y3beeAN9A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

2. 客户端会随机初始化序号（client_isn），将此序号置于TCP首部的“序号”字段中，同时把SYN标志位置为1，表示SYN 报文。接着把第一个SYN报文发送给服务端，表示向服务端发起连接，该报文不包含应用层数据，之后客户端处于SYN-SENT状态

	<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS84320oABn0E6jjsYHLicn6L5mlunbCDWGImCCHs41AWjZMnV8P1qdM99fQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

3. 服务端收到客户端的 SYN 报文后，首先服务端也随机初始化自己的序号（server_isn），将此序号填入TCP首部的“序号”字段中，其次把TCP首部的“确认应答号”字段填入client_isn+1,接着把SYN和ACK标志位置为1.最后把该报文发给客户端，该报文也不包含应用层数据，之后服务端处于 SYN-PCVD 状态

	<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS843OM01fA1X8oZ3wpr2AV8ngpjSJcyhoTQEAFKo8UdYMr456Fb5dv0alQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

4. 客户端收到服务端报文后，还要向服务端回应最后一个应答报文，首先该应答报文TCP首部ACK 标志位置为1，其次“确认应答号”字段填入 server_isn + 1, 最后把报文发送给服务端，这次报文可以携带客户到服务器的数据，之后客户端处于 ESTABLISHED 状态

5. 服务器收到客户端的应答报文后，也进入 ESTABLISHED 状态

从上面的过程可以发现第三次握手是可以携带数据的，前两次握手是不可以携带数据的，这也是面试常问的题。

一旦完成三次握手，双方都处于 ESTABLISHED 状态，至此连接就已建立完成，客户端和服务端就可以相互发送数据了。

### 如何在 Linux 系统中查看 TCP 状态？

TCP 的连接状态查看在Linux可以通过 `netstat -napt` 命令查看。

![](https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS843TdYaGI3f27nYYR47ibmH0iaV6zODCZhwpVoX7t7iasTTplcibpXXMib2DJA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 为什么是三次握手？不是两次、四次？

相信大家比较常回答的是：“因为三次握手才能保证双方具有接收和发送的能力“。

这回答是片面的，并没有说出主要的原因。

在前面我们知道了什么是 TCP 连接：

* 用于保证可靠性和流量控制维护某些状态信息，这些信息的组合，包括Socket、序列号和窗口大小称为连接

所以，重要的是为什么三次握手才可以初始化Socket、序列号和窗口大小并建立TCP连接。

接下来以三个方面分析三次握手的原因：

* 三次握手才可以组织历史重复连接的初始化（主要原因）
* 三次握手才可以同步双方的初始序列号
* 三次握手才可以避免浪费

#### 原因一：避免历史连接

我们来看看 RFC793 指出的TCP连接使用三次握手的首要原因：

The principle reason for the three-way handshake is to prevent old duplicate connection initiations from causing confusion.

简单来说，三次握手的首要原因是为了防止旧的重复连接初始化造成混乱。

网络环境是错综复杂的，往往并不是如我们期望的一样，先发送的数据包，就先到达目标主机，反而它很骚，可能会由于网络拥堵等乱七八糟的原因，会使得旧的数据包，先到达目标主机，那么这种情况下TCP三次握手是如何避免的：

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS8436nKau10lAsztRqbyhjC1C1GRcsEz04icZmomMjwcxgeGn97BnKUoxibw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

客户端连续发送多次SYN建立连接的报文，在网络拥堵等情况下：

* 一个“旧SYN报文”比“最新的SYN”报文早到达了服务端
* 那么此时服务端就会回一个SYN+ACK报文给客户端
* 客户端收到后可以根据自身的上下文，判断这是一个历史连接（序列号过期或超时），那么客户端就会发送RST报文给服务端，表示中止这一次连接。

如果是两次握手连接，就不能判断当前连接是否是历史连接，三次握手则可以在客户端（发送方）准备发送第三次报文时，客户端因有足够的上下文来判断当前连接是否是历史连接：

* 如果是历史连接（序列号过期或超时），则第三次握手发送的报文是RST报文，所以中止此次历史连接
* 如果不是历史连接，则第三次发送的报文是ACK报文，通信双方就会成功建立连接

所以，TCP使用<u>三次握手建立连接的最主要原因是==防止历史连接初始化了连接==。</u>

#### 原因二：同步双方初始序列号

TCP协议的通信双方，都必须维护一个“序列号”，序列号是可靠传输的一个关键因素，它的作用：

* 接收方可以去除重复的数据
* 接收方可以根据数据包的序列号按序接收
* 可以标识发送出去的数据包中，哪些是已经被对方收到的

可见，序列号在TCP连接中占据着非常重要的作用，所以当客户端发送携带“初始序列号”的SYN报文的时候，需要服务端回一个ACK应答报文，表示客户端的SYN报文已被服务端成功接收，那当服务端发送“初始序列号”给客户端的时候，依然也要得到客户端的应答回应，这样一来一回才能确保双方的初始序列号能被可靠的同步。

四次握手其实也能够可靠的同步双方的初始化序号，但由于第二步和第三步可以优化成一步，所以就成了三次握手。

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS843HWajXhQQfx6CH4EUxLqib0AAOXolZfIvuoEDkDoXaQ3RIceibo8ia9MQQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

而两次握手只保证了一方的初始序列号能被对方成功接收，没办法保证双方的初始序列号都能被确认接收。

#### 原因三：避免资源浪费

如果只有“两次握手”，当客户端的SYN请求连接在网络中阻塞，客户端没有接收到ACK报文，就会重新发送SYN，由于没有第三次握手，服务器不清楚客户端是否收到了自己发送的建立连接的ACK确认信号，所以每收到一个SYN就只能先主动建立一个连接，这会造成：

如果客户端的SYN阻塞了，重复发送多次SYN报文，那么服务器在收到请求后就会建立多个冗余的无效链接，造成不必要的资源浪费。

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS843CaTeGEvR5jg3iaHbUTEroayMBUoK3yfy9zGwlIia8pJu8x4RDkDGFLicg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />

即两次握手会造成消息滞留情况下，服务器重复接受无用的连接请求SYN报文，而造成重复分配资源。

#### 小结

TCP建立连接时，通过三次握手能防止历史连接的建立，能减少双方不必要的资源开销，能帮助双方同步初始化序号。序列号能保证数据包不重复、不丢弃和按序传输。

不使用 两次握手 和 四次握手 的原因：

* 两次握手： 无法防止历史连接的建立，会造成双方资源的浪费，也无法可靠的同步双方序列号
* 四次握手：三次握手就已经理论上最少可靠连接建立，所以不需要使用更多的通信次数。

为什么客户端和服务端的初始序列号 ISN 是不相同的？

初始序列号 ISN 是如何随机产生的？

既然 IP 层会分片，为什么 TCP 层还需要 MSS 呢？

什么是 SYN 攻击？如何避免 SYN 攻击？

## TCP 连接断开

### TCP 四次挥手过程和状态变迁

TCP 断开连接是通过四次挥手方式.

双方都可以主动断开连接, 断开连接后主机中的「资源」将被释放.

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZeo9xBVAyPJ8iaWCC6sYS843KaMMu2mHfFLZNgiaREDZ5JicRYrlaiciayQjh9HDsacxIbMT0emGUpAX5w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />

1. 客户端打算关闭连接, 此时会发送一个TCP首部FIN标志位被置为1的报文, 也即FIN报文, 之后客户端进入 FIN_WAIT_1 状态
2. 服务端收到该报文后, 就向客户端发送ACK应答报文, 接着服务端进入CLOSED_WAIT 状态
3. 客户端收到服务端的ACK 应答报文后, 之后进入 FIN_WAIT_2 状态
4. 等待服务端处理完数据后, 也向客户端发送FIN报文, 之后服务端进入LAST_ACK 状态
5. 客户端收到服务端的FIN报文后,回一个ACK应答报文, 之后服务端进入TIME_WAIT状态
6. 服务端收到了ACK应答报文后, 就进入了CLOSE状态, 至此服务端已经完成连接的关闭
7. 客户端在经过2MSL 一段时间后, 自动进入CLOSE状态, 至此客户端也完成连接的关闭

你可以看到, 每个方向都需要一个 FIN 和 一个 ACK, 因此通常被称为四次握手.

这里一点需要注意的是: **<u>主动关闭连接的, 才有 TIME_WAIT 状态</u>**

### 为什么挥手需要四次？

再来回顾下四次挥手双方发 FIN 包的过程, 就能理解为什么需要四次了.

* 关闭连接时, 客户端向服务端发送 FIN 时, 仅仅表示客户端不再发送数据了但是还能接收数据
* 服务器收到客户端的FIN报文时, 先回一个ACK应答报文, 而服务端可能还有数据需要处理和发送, 等服务端不再发送数据时, 才发送FIN报文给客户端来表示同意现在关闭连接.

从上面过程可知, 服务端通常需要等待完成数据等发送和处理, 所以服务端的ACK和FIN一般都会分开发送, 从而比三次握手导致多了一次.

### 为什么 TIME_WAIT 等待的时间是 2MSL？



### 为什么需要 TIME_WAIT 状态？



TIME_WAIT 过多有什么危害？

如何优化 TIME_WAIT？

### 如果已经建立了连接，但是客户端突然出现故障了怎么办？



## Socket 编程

针对 TCP 应该如何 Socket 编程？

listen 时候参数 backlog 的意义？

客户端调用 close 了，连接是断开的流程是什么？

# [你还在为 TCP 重传、滑动窗口、流量控制、拥塞控制发愁吗？看完图解就不愁了](https://mp.weixin.qq.com/s/Tc09ovdNacOtnMOMeRc_uA)

## 重传机制

#### 超时重传

超时时间应该设置为多少呢？

#### 快速重传

#### SACK 方法

#### Duplicate SACK

### 滑动窗口

引入窗口概念的原因

窗口大小由哪一方决定？

发送方的滑动窗口

程序是如何表示发送方的四个部分的呢？

接收方的滑动窗口

接收窗口和发送窗口的大小是相等的吗？

### 流量控制

#### 操作系统缓冲区与滑动窗口的关系

那操心系统的缓冲区，是如何影响发送窗口和接收窗口的呢？

#### 窗口关闭

窗口关闭潜在的危险

TCP 是如何解决窗口关闭时，潜在的死锁现象呢？

#### 糊涂窗口综合症

怎么让接收方不通告小窗口呢？

怎么让发送方避免发送小数据呢？

### 拥塞控制

为什么要有拥塞控制呀，不是有流量控制了吗？

什么是拥塞窗口？和发送窗口有什么关系呢？

那么怎么知道当前网络是否出现了拥塞呢？

拥塞控制有哪些控制算法？

#### 慢启动

那慢启动涨到什么时候是个头呢？

#### 拥塞避免算法

#### 拥塞发生

发生超时重传的拥塞发生算法

发生快速重传的拥塞发生算法

#### 快速恢复

# [IP 基础知识“全家桶”，45 张图一套带走](https://mp.weixin.qq.com/s/qydIO7NDfFTYs4-ZZlfgRg)

## IP 基本认识

### 网络层与数据链路层有什么关系呢？

## IP 地址的基础知识

### IP 地址的分类

#### 什么是 A、B、C 类地址？

#### A、B、C 分类地址最大主机个数是如何计算的呢？

#### 广播地址用于什么？

#### 什么是 D、E 类地址？

#### 多播地址用于什么？

#### IP 分类的优点

#### IP 分类的缺点

### 无分类地址 CIDR

#### 怎么划分网络号和主机号的呢？

#### 为什么要分离网络号和主机号？

#### 怎么进行子网划分？

### 公有 IP 地址与私有 IP 地址

#### 公有 IP 地址由谁管理呢？

### IP 地址与路由控制

#### 环回地址是不会流向网络

### IP 分片与重组

### IPv6 基本认识

#### IPv6 的亮点

#### IPv6 地址的标识方法

#### IPv6 地址的结构

#### IPv6 单播地址类型

### IPv4 首部与 IPv6 首部

## IP 协议相关技术

### DNS

#### 域名的层级关系

#### 域名解析的工作流程

### ARP

#### 那么 ARP 又是如何知道对方 MAC 地址的呢？

#### RARP 协议你知道是什么吗？

### DHCP

#### 咦，用的是广播，那如果 DHCP 服务器和客户端不是在同一个局域网内，路由器又不会转发广播包，那不是每个网络都要配一个 DHCP 服务器？

### NAT

#### 那不是 N 个 私有 IP 地址，你就要 N 个公有 IP 地址？这怎么就缓解了 IPv4 地址耗尽的问题？这不瞎扯吗？

#### NAT 那么牛逼，难道就没缺点了吗？

#### 如何解决 NAT 潜在的问题呢？

### ICMP

#### ICMP 功能都有啥？

#### ICMP 类型

### IGMP

#### IGMP 工作机制