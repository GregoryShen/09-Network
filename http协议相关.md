# [硬核！30 张图解 HTTP 常见的面试题](https://mp.weixin.qq.com/s/bUy220-ect00N4gnO0697A)

文章结构：

1. HTTP 基本概念
2. Get和Post
3. HTTP特性
4. HTTPS与HTTP
5. HTTP/1.1、HTTP/2、HTTP/3的演变

## HTTP基本概念

### HTTP 是什么？描述一下？

HTTP 是「超文本传输协议」， 也就是 ==H==yper==T==ext ==T==ransfer ==P==rotocol

### 能否详细解释「超文本传输协议」?

HTTP的名字「超文本传输协议」,可以拆成三个部分:

* 超文本
* 传输
* 协议

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZfXG1113Sjm0iaOXfoOv0tlU4cfNS4t8C0AjG8YleW3FjITV4h4aQNn1iboHhjALOGicsFsLuQAXwVaQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />

1. 协议

在生活中, 我们也能随处可见「协议」, 例如:

* 刚毕业时会签一个「三方协议」
* 找房子时会签一个「租房协议」

生活中的协议, 本质上与计算机中的协议是相同的, 协议的特点:

* 「协」字, 代表的意思是==必须有两个以上的参与者==. 例如三方协议里的参与者有三个;租房协议里的参与者有两个
* 「议」字, 代表的意思是==对参与者的一种行为约定和规范==. 例如三方协议里规定试用期期限、毁约金等; 租房协议里规定租期期限、每月租金金额、违约如何处理等.

针对 HTTP 协议, 我们可以这么理解:

HTTP 是一个用在计算机世界里的协议. 它使用计算机能够理解的语言确立了一种计算机之间交流通信的规范(两个以上的参与者), 以及相关的各种控制和错误处理方式 (行为约定和规范)

2. 传输

所谓的「传输」, 很好理解, 就是把一堆东西从A点搬到B点, 或者从B点搬到A点.

别轻视了这个简单的动作, 它至少包含两项重要的信息.

HTTP 是一个==双向协议==.

我们在上网冲浪时, 浏览器是请求方A, 百度网站就是应答方B. 双方约定用 HTTP 协议来通信, 于是浏览器把请求数据发送给网站, 网站再把一些数据返回给浏览器, 最后由浏览器渲染在屏幕, 就可以看到图片、视频了.

数据虽然是在A和B之间传输, 但==允许中间有中转或接力==.

在 HTTP 里, 需要中间人遵从 HTTP 协议, 只要不打扰基本的数据传输, 就可以添加任意额外的东西.

针对传输, 我们可以进一步理解HTTP.

HTTP 是一个在计算机世界里专门用来在**<u>两点之间传输数据</u>**的约定和规范.

1. 超文本

HTTP 传输的内容是「超文本」.

「文本」: 在互联网早期的时候只是简单的字符文字, 但现在「文本」的含义已经扩展为图片、视频、压缩包等, 在HTTP 眼里这些都算作「文本」

「超文本」:就是超越了普通文本的文本, 它是文字、图片、视频等的混合体, <u>**最关键有超链接, 能从一个超文本跳转到另外一个超文本.**</u>

HTML 就是最常见的超文本了, 它本身只是纯文字文件, 但内部用很多标签定义了图片、视频等链接, 再经过浏览器等解释, 呈现给我们的就是一个文字、有画面的网页了.

经过了对 HTTP 里这三个名词的详细解释, 就可以给出比「超文本传输协议」更准确更有技术含量的答案:

**HTTP 是一个在计算机世界里专门在「两点」之间「传输」文字、图片、音频、视频等「超文本」数据等「约定和规范」**.

### 那「HTTP 是用于从互联网服务器传输超文本到本地浏览器等协议HTTP」这种说法正确吗?

这种说法是不正确的. 因为也可以是「服务器< - - >服务器」, 所以采用两点之间的描述会更准确.

### HTTP 常见的状态码有哪些？

| 状态码 | 具体含义                                               | 常见状态码         |
| :----: | :----------------------------------------------------- | ------------------ |
|  1xx   | 提示信息, 表示目前是协议处理的中间状态, 还需要后续操作 |                    |
|  2xx   | 成功, 报文已经收到并被正确处理                         | 200、204、206      |
|  3xx   | 重定向, 资源位置发生变动, 需要客户端重新发送请求       | 301、302、304      |
|  4xx   | 客户端错误, 请求报文有误, 服务器无法处理               | 400、403、404      |
|  5xx   | 服务器错误, 服务器在处理请求时内部发生了错误           | 500、501、502、503 |

#### 1xx

`1xx` 类状态码属于提示信息, 是协议处理中的一种中间状态, 实际用到的比较少.

#### 2xx

`2xx`类状态码表示服务器成功处理了客户端的请求, 也是我们最愿意看到的状态.

「200 OK」是最常见的成功状态码, 表示一切正常. 如果是非 HEAD 请求, 服务器返回的响应头都会有 body 数据.

「204 No Content」也是常见的成功状态码, 与200 OK 基本相同, 但响应头没有 body 数据.

「206 Partial Content」是应用于 HTTP 分块下载或断点续传, 表示响应返回的body 数据并不是资源的全部, 而是其中的一部分, 也是服务器处理成功的状态.

#### 3xx

`3xx` 类状态码表示客户端请求的资源发生了变动, 需要客户端用新的URL 重新发送请求获取资源, 也就是**重定向**

「**301 Moved Permanently**」表示永久重定向, 说明请求的资源已经不存在了, 需该用新的URL再次访问.

「**302 Moved Temporarily**[^1]」表示临时重定向, 说明请求的资源还在, 但暂时需要用另一个URL来访问.

301和302 都会在响应头里使用字段 Location, 指明后续要跳转的URL, 浏览器会自动重定向新的URL.

「**304 Not Modified**」不具有跳转的含义, 表示资源未修改, 重定向已存在的缓冲文件, 也称缓存重定向, 用于缓存控制.

#### 4xx

`4xx` 类状态码表示客户端发送的报文有误, 服务器无法处理, 也就是错误码的含义.

「**400 Bad Request**」表示客户端请求的报文有错误, 但只是个笼统的错误.

「**403 Forbidden**」表示服务器禁止访问资源, 并不是客户端的请求出错.

「**404 Not Found**」表示请求的资源在服务器上不存在或未找到, 所以无法提供给客户端.

#### 5xx

`5xx` 类状态码表示客户端请求报文正确, 但是**服务器处理时内部发生了错误**, 属于服务器端的错误码.

「**500 Internal Server Error**」与 400 类型, 是个笼统的错误码, 服务器发生了什么错误, 我们并不知道.

「**501 Not Implemented**」表示客户端请求的功能还不支持, 类似“即将开业, 敬请期待”的意思.

「**502 Bad Gateway**」通常是服务器作为网关或代理时返回的错误码, 表示服务器自身工作正常, 访问后端服务器发生了错误.

「**503 Service Unavailable**」表示服务器当前很忙, 暂时无法响应服务器, 类似“网络服务正忙, 请稍后重试”的意思.

### http 常见字段有哪些?

#### Host

客户端发送请求时, 用来指定服务器的域名.

```html
Host: www.A.com
```

有了 Host 字段, 就可以将请求发往「同一台」服务器上的不同网站.

#### Content-Length

服务器在返回数据时, 会有 Content-Length 字段, 表明本次回应的数据长度.

```html
Content-Length: 1000
```

如上面则是告诉浏览器, 本次服务器回应的数据长度是1000个字节, 后面的字节就属于下一个回应了

#### Connection

Connection 字段最常用于<u>客户端要求服务器使用 TCP 永久连接, 以便其他请求复用.</u>

HTTP/1.1 版本的默认连接都是持久连接, 但为了兼容老版本的HTTP, 需要指定 Connection 首部字段的值为 keep-alive.

```html
Connection: keep-alive
```

一个可以复用的TCP连接就建立了, 直到客户端或服务器主动关闭连接. 但是, 这不是标准字段.

#### Content-Type

Content-Type 字段<u>用于服务器回应时, 告诉客户端, 本次数据是什么格式.</u>

```html
Content-Type: text/html; charset=utf-8
```

上面的类型表明, 发送的是网页, 而且编码是UTF-8

客户端请求的时候, 可以使用 Accept 字段声明自己可以接受哪些数据格式.

```html
Accpt: */*
```

上面代码中, 客户端声明自己可以接受任何格式的数据

#### Content-Encoding

Content-Encoding 字段<u>说明数据的压缩方法. 表示服务器返回的数据使用了什么压缩格式.</u>

```html
Content-Encoding: gzip
```

上面表示服务器返回的数据采用了gzip 方式压缩, 告知客户端需要用此方式解压.

客户端在请求时, 用 `Accept-Encoding`字段说明自己可以接受哪些压缩方法.

```html
Accept-Encoding: gzip, deflate
```

## GET 与 POST

### 说一下 GET 和 POST 的区别？

Get 方法的含义是请求从服务器获取资源, 这个资源可以是静态的文本、页面、图片视频等.

比如, 你打开我的文章, 浏览器就会发送 GET 请求给服务器, 服务器就会返回文章的所有文字及资源.

而 POST 方法则是相反操作, 它向 URI 指定的资源提交数据, 数据就放在报文的body里.

比如, 你在我文章底部, 敲入了留言后点击「提交」, 浏览器就会执行一次POST 请求, 把你的留言文字放进了报文body里, 然后拼接好 POST 请求头, 通过TCP 协议发送给服务器.

### GET 和 POST 方法都是安全和幂等的吗？

先说下安全和幂等的概念:

* 在 HTTP 协议里, 所谓的「安全」是指请求方法不会「破坏」服务器上的资源
* 所谓的「幂等」,意思是多次执行相同的操作, 结果都是「相同」的

那么很明显 GET 方法就是安全且幂等的, 因为它是「只读」操作, 无论操作多少次, 服务器上的数据都是安全的, 且每次的结果都是相同的.

POST 因为是「新增或提交数据」的操作, 会修改服务器上的资源, 所以是**<u>不安全</u>**的, 且多次提交数据就会创建多个资源, 所以<u>**不是幂等**</u>的.

## HTTP 特性

### 你知道的 HTTP(1.1) 的优点有哪些，怎么体现的？

HTTP 最突出的优点是“简单、灵活和易于扩展、应用广泛和跨平台”

1. #### 简单

HTTP 基本的报文格式就是 header + body, 头部信息也是 key-value 简单文本的形式，易于理解，降低了学习和使用门槛。

2. #### 灵活和易于扩展

HTTP 协议里的各类请求方法、URI\URL、状态码、头字段等每个组成要求都没有被固定死，都允许开发人员自定义和扩充。

同时 HTTP 由于是工作在应用层（OSI 第七层），则它下层可以随意变化

HTTPS 也就是在 HTTP 与 TCP 层之间增加了 SSL/TLS 安全传输层，HTTP/3 甚至把 TCPP 层 换成了基于 UDP 的 QUIC。

3. #### 应用广泛和跨平台

互联网发展至今， HTTP 的应用范围非常的广泛，从台式机的浏览器到手机上的各种APP， 从看新闻、刷贴吧到购物、理财等， HTTP 的应用遍地开花，同时天然具有跨平台的优越性。

### 那它的缺点呢？

HTTP 协议里有优缺点一体的双刃剑，分别是“无状态、明文传输”， 同时还有一大缺点“不安全”。

#### 无状态双刃剑

无状态的好处，因为服务器不会去记忆 HTTP 的状态，所以不需要额外的资源来记录状态信息，这能减轻服务器的负担，能够把更多的 CPU 和内存用来对外提供服务。

无状态的坏处， 既然服务器没有记忆能力，它在完成有关联性的操作时会非常麻烦。

例如：登录-> 添加购物车 -> 下单 -> 结算 -> 支付， 这系列操作都要知道用户的身份才行。但服务器不知道这些请求是有关联的，每次都要问一遍身份信息。

这样每操作一次， 都要验证信息。对于无状态的解决方案，比较简单的方式是用 Cookie

Cookie 通过在请求和响应报文中写入 Cookie 信息来控制客户端的状态。

#### 明文传输的双刃剑

明文意味着在传输过程中的信息，是可方便阅读的，通过浏览器F12或 Wireshark 抓包都可以直接肉眼查看。

但正是这样， HTTP 的所有信息都暴露在了光天化日之下，相当于信息裸奔。

### 不安全

HTTP 比较严重的缺点就是不安全：

* 通信使用明文（不加密），内容可能会被窃听。比如，账号信息容易泄露。
* 不验证通信方的身份，因此有可能遭遇伪装。比如，访问假的淘宝、拼多多
* 无法验证报文的完整性，所以有可能已遭篡改。比如，网页上植入垃圾广告，视觉污染。

HTTP 的安全问题，可以用HTTPS 解决，也就是通过引入 SSL/TLS 层，使得在安全上达到了极致

### 那你说下 HTTP/1.1 的性能如何？

HTTP 协议是基于 TCP/IP， 并且使用了“请求- 应答” 的通信模式，所以性能的关键就在这两点：

#### 长连接

早起 HTTP/1.0 性能上的一个很大的问题，就是每发起一个请求，都要新建一次 TCP 连接（三次握手），而且是串行请求，做了无谓的 TCP 连接建立和断开，增加了通信开销。

为了解决上述 TCP 连接问题，HTTP/1.1 提出了长连接的通信方式，也较持久连接。这种方式的好处在于较少了 TCP 连接的重复建立和断开所造成的额外开销，并减轻了服务器端的负载。

<u>持久连接的特点是，==只要任意一端没有明确提出断开连接，则保持TCP 连接状态==。</u>

#### 管道网络传输

HTTP/1.1 采用了长连接的方式，这使得管道（pipeline）网络传输成为了可能。

即可在同一个 TCP 连接里面，客户端可以发起多个请求，只要第一个请求发出去了，不必等其回来，就可以发第二个请求出去，可以减少整体的响应时间。

举例来说，客户端需要请求两个资源。以前的做法是，在同一个TCP连接里面，先发送A请求，然后等待服务器做出回应，收到后再发出B请求。管道机制允许浏览器同时发出A 请求和B 请求。

但服务器还是按照顺序，先回应A请求，完成后再回应B请求。要是前面回应的特别慢，后面就会有很多请求排队等着，这种称为队头阻塞。

#### 队头阻塞

“请求 - 应答” 模式加剧了 HTTP 的性能问题。

因为当顺序发送的请求序列中的一个请求因为某种原因被阻塞时，在后面排队的所有请求也一同被阻塞了，会招致客户端一直请求不到数据。

## HTTP 与 HTTPS

### HTTP 与 HTTPS 有哪些区别？

1. HTTP 是超文本传输协议，信息是明文传输，存在安全风险的问题。HTTPS 则解决 HTTP 不安全的缺陷，在 TCP 和 HTTP 网络层之间加入了 SSL/TLS 安全协议，使得报文能够加密传输。
2. HTTP 连接建立相对简单，TCP 三次握手之后便可以进行 HTTP 报文传输。而 HTTPS 在 TCP 三次握手之后，还需要进行 SSL/TLS 的握手过程，才可以进入加密报文传输。
3. HTTP 的端口号是 80， HTTPS 的端口号是 443
4. HTTPS 协议需要向 CA（证书权威机构）申请数字证书，来保证服务器的身份是可信的。

### HTTPS 解决了 HTTP 的哪些问题？

HTTP 由于是明文传输，所以安全上存在以下三个风险：

* 窃听风险，比如通信链路上可以获取通信内容，用户号容易没
* 篡改风险，比如强制入垃圾广告，视觉污染，用户眼容易瞎
* 冒充风险，比如冒充淘宝网站，用户钱容易没

HTTPS 在 HTTP 和 TCP 层之间 加入了 SSL/TLS 协议

<img src="https://mmbiz.qpic.cn/mmbiz_jpg/J0g14CUwaZfXG1113Sjm0iaOXfoOv0tlUzdWm2toFZmoutgdMlZichgjsFggJOHXg6Z09ckSyeTPpkdywfljh3uw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />



可以很好地解决了上述风险：

* 信息加密：交互信息无法被窃取，但你的号会因为“自身忘记”账号而没
* 校验机制：无法篡改通信内容，篡改了就不能正常显示，但百度“竞价排名”依然可以搜索垃圾广告
* 身份证书：证明淘宝网是真的淘宝网

可见，只要自身不作恶，SSL/TLS 协议是能保证通信是安全的

### HTTPS 是如何解决上面的三个风险的？

* 混合加密的方式实现信息的机密性，解决了窃听的风险
* 摘要算法的方式来实现完整性，它能够为数据生成独一无二的“指纹”，指纹用于校验数据的完整性，解决了篡改的风险
* 将服务器公钥放入到数字证书中，解决了冒充的风险

#### 混合加密

通过混合加密的方式可以保证信息的机密性，解决了窃听的风险

<img src="https://mmbiz.qpic.cn/mmbiz_jpg/J0g14CUwaZfXG1113Sjm0iaOXfoOv0tlUYNGEmfY95A74GR3xicqXKZCDI7Q4icgQu7CuSSx9QiaFlr4Py49RHonjw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />

HTTPS 采用的是 对称加密 和 非对称加密 结合的 混合加密方式：

* 在通信建立前采用非对称加密的方式交换“会话秘钥”，后续就不再使用非对称加密
* 在通信过程中全部使用对称加密的“会话密钥”的方式加密明文数据

采用“混合加密”的方式的原因：

* 对称加密只使用一个密钥，运算速度快，密钥必须保密，无法做到安全的密钥交换
* 非对称加密使用两个密钥：公钥和私钥，公钥可以任意分发而私钥保密，解决了密钥交换问题但速度慢

#### 摘要算法

摘要算法用来实现完整性，能够为数据生成独一无二的“指纹”，用于校验数据的完整性，解决了篡改的风险。

<img src="https://mmbiz.qpic.cn/mmbiz_jpg/J0g14CUwaZfXG1113Sjm0iaOXfoOv0tlUicIliaBcr2XAXpMdeibLG4MMticpkX0e6xZHbXeiavMu7faJcL2TdVj0Udw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />

客户端在发送明文之前会通过摘要算法算出明文的“指纹”，发送时把指纹+明文一同加密成密文后，发送给服务器，服务器解密后，用相同的摘要算法算出发送过来的明文，通过比较客户端携带的“指纹”和当前算出的“指纹”做比较，若“指纹”相同，说明数据是完整的。

#### 数字证书

客户端先向服务器端索要公钥，然后用公钥加密信息，服务器收到密文后，用自己的私钥解密。

这就存在问题，如何保证公钥不被篡改和信任度？

所以这里就需要借助第三方权威机构 CA（数字证书认证机构），将服务器公钥放在数字证书（由数字证书认证机构颁发）中，只要证书是可信的，公钥就是可信的。

<img src="https://mmbiz.qpic.cn/mmbiz_jpg/J0g14CUwaZfXG1113Sjm0iaOXfoOv0tlUibyiaEab7NMrTn632LZmYQe5qaibibT0xsOs7ic6u98ypWJBjbPMzOUCb2g/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />

通过数字证书的方式保证服务器公钥的身份，解决冒充的风险。

### HTTPS是如何建立连接的？其间交互了什么？

SSL/TLS 协议基本流程：

* 客户端向服务器索要并验证服务器的公钥
* 双方协商生产“会话密钥”
* 双方采用“会话密钥”进行加密通信

前两步也就是 SSL/TLS 的建立过程， 也就是握手阶段。

SSL/TLS 的“握手阶段”涉及四次通信，可见下图：

![](https://mmbiz.qpic.cn/mmbiz_jpg/J0g14CUwaZfXG1113Sjm0iaOXfoOv0tlUMRTqQDVOJHMZe3JoN5TqSb0uYicOqMH2qHgic7M6rtCrjPOToDjBm11A/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

SSL/TLS 协议建立的详细流程：

我觉得这个应该不会问。。先不看了。。。

#### ClientHello

#### ServerHello

#### 客户端回应

#### 服务器的最后回应

## HTTP/1.1、HTTP/2、HTTP/3 演变

### 说说 HTTP/1.1 相比 HTTP/1.0 提高了什么性能？

HTTP/1.1 相比 HTTP/1.0 性能上的改进：

* 使用 TCP 长连接的方式改善了 HTTP/1.0 短连接造成的性能开销
* 支持管道（pipeline）网络传输，只要第一个请求发出去了，不必等其回来，就可以发第二个请求出去，可以减少整体的响应时间

但 HTTP/1.1 还是有性能瓶颈：

* 请求/响应头部（Header）未经压缩就发送，首部信息越多延迟越大。只能压缩Body 的部分
* 发送冗长的首部，每次互相发送相同的首部造成的浪费较多
* 服务器是按请求的顺序响应的，如果服务器响应慢，会招致客户端一直请求不到数据，也就是队头阻塞
* 没有请求优先级控制
* 请求只能从客户端开始，服务器只能被动响应

### 那上面的 HTTP/1.1 的性能瓶颈，HTTP/2 做了什么优化？

HTTP/2 协议是基于 HTTPS 的，所以 HTTP/2 的安全性也是有保障的

HTTP/2 相比 HTTP/1.1 性能上的改进：

#### 头部压缩

HTTP/2 会==压缩头==（Header），如果你同时发出多个请求，他们的头是一样的或是相似的，那么，==协议会帮你消除重复的部分==。

这就是所谓的 HPACK 算法：在客户端和服务器同时维护一张头信息表，所有字段都会存入这个表，生成一个索引号，以后就不发送同样字段了，只发送索引号，这样就提高速度了。

<img src="https://mmbiz.qpic.cn/mmbiz_jpg/J0g14CUwaZfXG1113Sjm0iaOXfoOv0tlUicf9XsgyOGDvTA9SsOicIz8t3pSibrAHTN6TW83WCmZsSeDqtZibJnoRHg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

#### 二进制格式

HTTP/2 不再像 HTTP/1.1 里的纯文本形式的报文，而是全面采用了**二进制格式**。

头信息和数据体都是二进制，并且统称为帧：头信息帧和数据帧

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZfXG1113Sjm0iaOXfoOv0tlUahoiazC1GOBz9ICKnAd4f1PesMoT4wK4RiciaSO8e4jVakTIKfvgYCdpg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:75%;" />

这样虽然对人不友好，但是对计算机非常友好，因为计算机只懂二进制，那么受到报文后，无需再将明文的报文转成二进制，而是直接解析二进制报文，这**<u>增加了数据传输的效率</u>**。

#### 数据流

HTTP/2 的数据包不是按顺序发送的，同一个连接里面连续的数据包，可能属于不同的回应。因此，必须要对数据包做标记，指出它属于哪个回应。

**<u>每个请求或回应的所有数据包，称为一个数据流（Stream）</u>**

每个数据流都标记着一个独一无二的编号，其中规定客户端发出的数据流编号为奇数，服务端发出的数据流编号为偶数

客户端还可以指定数据流的优先级，优先级高的请求，服务器就先响应该请求。

#### 多路复用

HTTP/2 是可以==在一个连接中并发多个请求或回应，而不用按顺序一一对应==。

移除了 HTTP/1.1 中的串行请求，不需要排队等待，也就不会再出现“队头阻塞”问题，降低了延迟，大幅度提高了连接的利用率。

举例来说，在一个TCP连接里，服务器收到了客户端A和B两个请求，如果发现A处理过程非常耗时，于是就回应A请求已经处理好的部分，接着回应B请求，完成后，再回应A请求剩下的部分。

#### 服务器推送

HTTP/2 还在一定程度上改善了传统的“请求 - 应答”工作模式，服务不再是被动地响应，也可以**<u>主动向客户端发送消息</u>**。

举例来说，在浏览器刚请求 HTML 的时候，就提前把可能会用到的JS、CSS文件等静态资源主动发给客户端，较少延时的等待，也就是服务器推送（Server Push,也叫Cache Push）

### HTTP/2 有哪些缺陷？HTTP/3 做了哪些优化？

HTTP/2 主要的问题在于：多个HTTP请求在复用一个TCP连接，下层的TCP协议是不知道有多少个HTTP请求的。

所以一旦发生了丢包现象，就会触发TCP的重传机制，这样在一个TCP连接中的所有HTTP请求都必须等待这个丢了的包被重传回来。

* HTTP/1.1 中的管道（pipeline）传输中如果有一个请求阻塞了，那么队列后请求也通通被阻塞了
* HTTP/2 多请求复用一个TCP连接，一旦发生丢包，就会阻塞住所有的HTTP请求。

这都是基于TCP传输层的问题，所以==HTTP/3把HTTP下层的TCP协议改成了UDP==

![](https://mmbiz.qpic.cn/mmbiz_jpg/J0g14CUwaZfXG1113Sjm0iaOXfoOv0tlUy5OSaaTftjD7JmdU4AUMnlrGOWXnMYss5sCxMMTPUibLeHIgdsdkklQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

UDP 发生是不管顺序，也不管丢包的，所以不会出现HTTP/1.1 的队头阻塞和HTTP/2的一个丢包全部重传问题。

大家都知道UDP是不可靠传输的，但基于UDP的QUIC协议可以实现类似TCP的可靠性传输

* QUIC 有自己的一套机制可以保证传输的可靠性。当某个流发生丢包时，只会阻塞这个流，其他流不会受到影响
* TLS升级成了最新的1.3版本，头部压缩算法也升级成了QPack
* HTTPS要建立一个连接，要花费6次交互，先是建立三次握手，然后是TLS/1.3的三次握手。QUIC直接把以往的TCP和TLS/1.3的6次交互合并成了3次，减少了交互次数。

![](https://mmbiz.qpic.cn/mmbiz_jpg/J0g14CUwaZfXG1113Sjm0iaOXfoOv0tlUyP3HNicKS2J21mHQD9EepOiciakC8nRkrX9C3I0hjC6Fhjvd4nLiakuLeg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

所以，QUIC是一个在UDP之上的伪TCP+TLS+HTTP/2的多路复用的协议。

QUIC是新协议，对于很多网络设备，根本不知道什么是QUIC，只会当做UDP，这样会出现新的问题。所以HTTP/3现在普及的进度非常缓慢。

# [探究！一个数据包在网络中的心路历程](https://mp.weixin.qq.com/s/iSZp41SRmh5b2bXIvzemIw)

一个简单的网络模型

![](https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvsInYzWibsjcxkyWMoKXUUvgnbg7zrZaghyUSI6dW1jZO3UcJqL66hdA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 孤单小弟 —— HTTP

### 浏览器做的第一步工作是解析 URL

首先浏览器做的第一步工作就是要对 URL 进行解析，从而生成发送给 Web 服务器的请求信息。

让我们看看一条长长的 URL 里的各个元素都代表什么，见下图：

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvcTsJcAXekhUYmHxS7JZ140D1q9bPNOZ2xeML16Hia4K6ByOjq0rcMPg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

所以图中长长的 URL 实际上是==请求服务器里的文件资源==。

### 要是上图中的蓝色部分 URL 元素都省略了，哪应该是请求哪个文件呢？

当没有路径名时，就代表访问根目录下事先设置的默认文件，也就是 /index.html 或者 /default.html 这些文件，这样就不会发生混乱了。

### 生产 HTTP 请求信息

对 URL 进行解析之后，浏览器确定了 Web 服务器和文件名，接下来就是根据这些信息来生成 HTTP 请求消息了。

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvCl3iaCJeUV6Oa8zESpNKPDicgibjwANs465zibfWwwUQlMZsjciaNicO1Vwg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />



## 真实地址查询 —— DNS

通过浏览器解析 URL 并生成 HTTP 消息后，需要委托操作系统将消息发送给 Web 服务器。

但在发送之前，还有一项工作需要完成，那就是查询服务器域名对应的 IP 地址，因为委托操作系统发送消息时，必须提供通信对象的 IP 地址。

比如我们打电话的时候，必须要知道对方的电话号码，但由于电话号码难以记忆，所以通常我们会将对方电话号码 +  姓名保存在通讯录里。

所以，有一种服务器就专门保存了 Web 服务器域名和 IP 的对应关系，它就是 DNS 服务器。

### 域名的层级关系

DNS 中的域名都是用句点来分隔的，比如 www.server.com，这里的句点代表了不同层次之间的界限。

在域名中，越靠右的位置表示其层级越高。

根域是在最顶层，它的下一层就是 com 顶级域，再下面是 server.com

所以域名的层级关系类似一个树状结构：

* 根 DNS 服务器
* 顶级域 DNS 服务器（com）
* 权威 DNS 服务器 （server.com）

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvN6F6eZ2vAU04o8gh1mJ6l7ovc7wsCvTVMvCFHyHqfsRUKtWYnblsCA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

根域的 DNS 服务器信息保存在互联网中所有的 DNS 服务器中。

这样一来，任何 DNS 服务器就都可以找到并访问根域 DNS 服务器了。

因此，客户端只要能够找到任意一台 DNS 服务器，就可以通过它找到根域 DNS 服务器，然后再一路顺藤摸瓜找到位于下层的某台目标 DNS 服务器。

### 域名解析的工作流程

1. 客户端首先会发出一个 DNS 请求，问 www.server.com 的 IP 是啥，并发给本地 DNS 服务器（也就是客户端的 TCP/IP 设置中填写的 DNS 服务器地址）。
2. 本地域名服务器收到客户端的请求后，如果缓存里的表格能找到 www.server.com，则它直接返回 IP 地址，如果没有，本地 DNS 会去问它的根域名服务器：“老大，能告诉我 www.server.com 的 IP 地址吗？”根域名服务器是最高层次的，它不直接用于域名解析，但能指明一条道路。
3. 根 DNS 收到来自本地 DNS 的请求后，发现后置是 .com，说：“www.server.com 这个域名归 .com 区域管理，我给你 .com 顶级域名服务器地址给你，你去问问它吧。”
4. 本地 DNS 收到顶级域名服务器的地址后，发起请求问“老二，你能告诉我 www.server.com 的 IP 地址吗？”
5. 顶级域名服务器说：“我给你负责 www.server.com 区域的权威 DNS 服务器的地址，你去问问它应该能问到。”[^2]
6. 本地 DNS 于是转向问权威 DNS 服务器：“老三，www.server.com 对应的 IP 是啥啊？” server.com 的权威 DNS 服务器，它是域名解析结果的原出处。为啥叫权威呢？就是我的域名我做主。
7. 权威 DNS 服务器查询后将对应的 IP 地址 X.X.X.X 告诉本地 DNS。
8. 本地 DNS 再将 IP 地址返回客户端，客户端和目标建立连接。

至此，我们完成了 DNS 的解析过程。现在总结一下，看下图：

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCv5bBPibRf9nk4wIb6J3jP62L6NEmPk3HicMUgf8VatcBicynP6BKLeT6GQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

DNS 域名解析过程蛮有意思的，整个过程就和我们日常生活中找人问路的过程类似，只指路不带路。

## 指南好帮手 —— 协议栈

通过 DNS 获取到 IP 后，就可以把 HTTP 的传输工作交给操作系统中的协议栈。

协议栈的内部分为几个部分，分别承担不同的工作。上下关系是有一定规则的，上面的部分会向下面的部分委托工作，下面的部分收到委托的工作并执行。

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvbLic0XNMIJgJ0pDm6K4s39vgGO4enAIT1jzDXfQPYrdiaQe8TMy11Wicw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

应用程序（浏览器）通过调用 Socket 库，来委托协议栈工作。协议栈的上半部分有两块，分别是负责收发数据的 TCP 和 UDP 协议，他们俩会接收应用层的委托执行收发数据的操作。

协议栈的下面一半是用 IP 协议控制网络包收发操作，在互联网上传数据时，数据会被切分成一块块的网络包，而将网络包发送给对方的操作就是由 IP 负责的。

此外 IP 中还包括 ICMP 协议和 ARP 协议。

* ICMP 用于告知网络包传送过程中产生的错误以及各种控制信息。
* ARP 用于根据 IP 地址查询响应的以太网 MAC 地址。

IP 下面的网卡驱动程序负责控制网卡硬件，而最下面的网卡则负责完成实际的收发操作，也就是对网线中的信号执行发送和接收操作。

## 可靠传输 —— TCP

HTTP 是基于 TCP 协议传输的，所以在这我们先了解下 TCP 协议。

### TCP 报头格式

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvWT9m8xicZXKk6ayV6nKAiaUAhdpdicfibLGEYhHx9OBo7EocXKx8wgIgww/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

首先，<u>源端口号</u>和<u>目的端口号</u>是不可少的，如果没有这两个端口号，数据就不知道该发给哪个应用。

接下来有包的<u>序号</u>，这是为了<u>解决包乱序的问题</u>。

还应该有的是<u>确认号</u>，目的是<u>确认发出去对方是否有收到</u>。如果没有收到就应该重新发送, 直到送达, 这是为了<u>解决不丢包的问题</u>.

接下来还有一些状态位. 例如 SYN 是发起一个连接, ACK 是回复, RST 是重新连接, FIN 是结束连接等. TCP 是面向连接的, 因而双方要维护连接的状态, 这些带状态位的包的发送, 会引起双方的状态变更.

还有一个重要的就是<u>窗口大小</u>. TCP 要做<u>流量控制</u>, 通信双方各声明一个窗口(缓存大小), 标识自己当前能够的处理能力, 别发送的太快, 撑死我, 也别发的太慢, 饿死我.

除了做流量控制以外, TCP 还会做<u>拥塞控制</u>, 对于真正的通路堵车不堵车, 它无能为力, 唯一能做的就是控制自己, 也即控制发送的速度. 不能改变世界, 就改变自己.

### TCP 传输数据之前，要先三次握手建立连接

在 HTTP 传输数据之前, 首先需要 TCP 建立连接, TCP 连接的建立, 通常称为三次握手.

这个所谓的「连接」,只是双方计算机里维护一个状态机, 在连接建立的过程中, 双方的状态变化时序图就像这样:

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvCUKg39o6S5sL4ZlRym1oibb3yLbN5NhCTBHIm2VhYzdbcykNy5mGEJA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

* 一开始, 客户端和服务端都处于 CLOSED 状态. 先是服务端主动监听某个端口, 处于 LISTEN 状态.
* 然后客户端主动发起连接 SYN, 之后处于 SYN-SENT 状态
* 服务端收到发起的连接, 返回 SYN, 并且 ACK 客户端的 SYN, 之后处于 SYN-RCVD 状态
* 客户端收到服务端发送的 SYN 和 ACK 之后, 发送 ACK 的 ACK, 之后处于 ESTABLISHED 状态, 因为它一发一收成功了.
* 服务端收到 ACK 的 ACK 之后, 处于 ESTABLISHED 状态, 因为它也一发一收成功了.

所以三次握手的目的是<u>**保证双方都有发送和接收的能力**</u>.

### 如何查看 TCP 的连接状态？

TCP 的连接状态查看, 在 Linux 可以通过 `netstat -napt` 命令查看:

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvgY3pZypoxcTEb4lFv3hKN9Mcm7zny8vzzjKDBRPPWjqb30ecKEYKfQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

### TCP 分割数据

如果 HTTP 请求消息比较长, 超过了 MSS 的长度, 这时 TCP 就需要把 HTTP 的数据拆解成一块块的数据发送, 而不是一次性发送所有数据.

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvGwQX0SDsblRZJf7OJuQPibox3JGIlRVTuCouOjMzgwPSoyx5orIMFmQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

* MTU: 一个网络包的最大长度, 以太网中一般为 1500 字节.
* MSS: 除去 IP 和 TCP 头部之后, 一个网络包所能容纳的 TCP 数据的最大长度.

数据会被以 MSS 的长度为单位进行拆分, 拆分出来的每一块数据都会被放进单独的网络包中. 也就是在每个被拆分的数据加上 TCP 头部信息, 然后交给 IP 模块来发送数据.

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvdOWGU3dj3HDafoDgY5BCAj3KichEvUCdID2p7bC5Jn7wiaUgHaN7Gjpw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

### TCP 报文生成

TCP 协议里面会有两个端口, 一个是浏览器监听的端口(通常是随机生成的), 一个是 Web 服务器监听的端口(HTTP默认端口号是80, HTTPS 默认端口号是443).

在双方建立了连接后, TCP 报文中的数据部分就是存放 HTTP 头部 + 数据, 组装好 TCP 报文之后, 就需交给下面的网络层处理.

至此, 网络包的报文如下图:

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvTzcpo31hh6dibOX6PEGUYrK5sHeMv4YS0D9UjTRZyIDRE0IfbjJSdaA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

## 远程定位 —— IP

TCP 模块在执行连接、收发、断开等各阶段操作时, 都需要委托 IP 模块将数据封装成网络包发送给通信对象.

### IP 包头格式

我们先看看 IP 报文头部的格式:

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvLibU5EShhIAC4HcLbP2Cq6ogwg74BIX3aBc8j0l2mV9DVCCuzfEjhVQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

在 IP 协议里面需要有<u>源地址 IP</u> 和 <u>目标地址 IP</u>:

* 源地址IP, 即是客户端输出的 IP 地址
* 目标地址IP, 即通过 DNS 域名解析得到的 Web 服务器 IP.

因为 HTTP 是经过 TCP 传输的, 所以在 IP 包头的协议号, 要填写为06(十六进制), 表示协议为 TCP.

### 假设客户端有多个网卡，就会有多个 IP 地址，那 IP 头部的源地址应该选择哪个 IP 呢?

当存在多个网卡时, 在填写源地址 IP 时, 就需要判断到底该填写哪个地址. 这个判断相当于在多块网卡中判断应该使用哪一块网卡来发包.

这个时候就需要根据路由表规则, 来判断哪一个网卡作为源地址 IP.

在 Linux 操作系统, 我们可以使用 `route -n` 命令来查看当前系统的路由表.

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvyXicb8HyS1MX3KCbUzZV0xjHj6Mc3JxHwCyrT9zaQ7jFbgX9Uz8Mibrg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

举个例子, 根据上面的路由表, 我们假设 Web 服务器的目标地址是 192.168.10.200

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvZww6ogwicmBKNwWaUjzR4wpXtJhC5EicXMIc1hEn1Vq65YFEKOic1Wmsw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

1. 首先先和第一条条目的子网掩码(Genmask) 进行「与运算」, 得到结果为 192.168.10.0, 但是第一个条目的 Destination 是 192.168.3.0, 两者不一致所以匹配失败.
2. 再与第二条目的子网掩码进行「与运算」, 得到的结果为 192.168.10.0, 与第二条目的 Destination 192.168.10.0 匹配成功, 所以将使用 eth1 网卡的 IP 地址作为 IP 包头的源地址

那么假设 Web 服务器的目标地址是 10.100.20.100, 那么依然依照上面的路由表规则判断, 判断后的结果是和第三条目匹配.

第三条目比较特殊, 它目标地址和子网掩码都是 0.0.0.0, 这表示默认网关, 如果其他所有条目都无法匹配, 就会自动匹配这一行. 并且后续就把包发给路由器, Gateway 即是路由器的 IP 地址.

### IP 报文生成

至此, 网络包的报文如下图:

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvObeicZLtRqF6wjeAR2vYP1eAh7WRXmcS3vlwMzmzswyqtWrJyiaZ57xg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

## 两点传输 —— MAC

生成了 IP 头部之后， 接下来网络包还需要在 IP 头部的前面加上 MAC 头部。

### MAC 包头格式

MAC 头部是以太网使用的头部，它包含了接收方和发送方的 MAC 地址等信息。

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvxJ9alzpuxFNK4SicsCtCVDwtDoI32RXUxko9p25kgDQSHToomIibDIaA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

在 MAC 包头里需要<u>发送方 MAC 地址</u>和<u>接收方目标 MAC 地址</u>，用于<u>两点之间的传输</u>。

一般在 TCP/IP 通信里， MAC 包头的协议类型只能用：

* 0800： IP 协议
* 0806： ARP 协议

### MAC 发送方和接收方如何确认?

发送方的 MAC 地址获取就比较简单了，MAC 地址是在网卡生产时写入到 ROM 里的，只要将这个值读取出来写入到 MAC 头部就可以了。

接收方的 MAC 地址就有点复杂了，只要告诉以太网对方的 MAC 地址，以太网就会帮我们把包发送过去，那么很显然这里应该填写对方的 MAC 地址。

所以先得搞清楚应该把包发给谁，这个只要查一下路由表就知道了。在路由表中找到相匹配的条目，然后把包发给 Gateway 列中的 IP 地址就可以了。

### 既然不知道要发给谁，那如何获取对方的 MAC 地址呢？

不知道对方 MAC 地址，就需要 ARP 协议帮我们找到路由器的 MAC 地址。

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvFq3nxQ0G2DUEKY4JtiaIDKaYE53ciaDohvicTYM0lN7DGatSWfFt7FJ9w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

ARP 协议会在以太网中以广播的形式，对以太网所有的设备喊出”这个 IP 地址是谁的？ 请把你的 MAC 地址告诉我“。

然后就会有人回答：“这个 IP 地址是我的，我的 MAC 地址是 xxx”。

如果对方和自己处于同一个子网中，那么通过上面的操作就可以得到对方的 MAC 地址。然后，我们将这个 MAC 地址写入 MAC 头部，MAC 头部就完成了。

### 好像每次都要广播获取，这不是很麻烦吗？

在后续操作系统会把本次查询结果放到一块叫做 ARP 缓存的内存空间留着以后用，不过缓存的时间就几分钟。

也就是说，在发包时：

* 先查询 ARP 缓存，如果其中已经保存了对方的 MAC 地址，就不需要发送 ARP 查询，直接使用 ARP 缓存中的地址。
* 而当 ARP 缓存中不存在对方 MAC 地址时，则发送 ARP 广播查询。

### 查看 ARP 缓存内容

在 Linux 系统中，我们可以使用 `arp -a` 命令来查看 ARP 缓存的内容。

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvTQuqsWJyLf9ia4JrTx2AAicnhSw1vBgesrd9EIToVaMEj3SESXHtDTOQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

### MAC 报文生成

至此，网络包的报文如下图：

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvXwUb0quVf04jOA6PSQBw9JawNDhW2qykDZeicGBK1DQ6BSITEUMHjZQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

## 出口 —— 网卡

IP 生成的网络包只是存放在内存中的一串二进制数字信息，没有办法直接发送给对方。因此，我们需要将数字信息转换为电信号，才能在网线上传输，也就是说，这才是真正的数据发送过程。

负责执行这一操作的是<u>网卡</u>，要控制网卡还需要靠<u>网卡驱动程序</u>。

网卡驱动从 IP 模块获取到包之后，会将其<u>复制</u>到网卡内的缓存区中，接着会在其<u>开头加上报头和起始帧分界符，在末尾加上用于检测错误的帧校验序列。</u>

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvRO9LjjVa7839p3IrJsdCAT6DSicnLVOBadYNbD79VdJR3iaguEhlMBWg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

* 起始帧分界符是一个用来标记包起始位置的标记
* 末尾的 FCS（帧校验序列）用来检查包传输过程是否有损坏

最后网卡会将包转为电信号，通过网线发送出去。

## 送别者 —— 交换机

下面来看一下包是如何通过交换机的。交换机的设计是将网络包原样转发到目的地。交换机工作在 MAC 层，也称为二层网络设备。

### 交换机的包接收操作

首先，电信号到达网线接口，交换机里的模块进行接收，接下来交换机里的模块将电信号转换为数字信号。

然后通过包末尾的 FCS 校验错误，如果没问题则放到缓冲区。这部分操作基本和计算机的网卡相同，但交换机的工作方式和网卡不同。

计算机的网卡本身具有 MAC 地址，并通过核对收到的包的接收方 MAC 地址判断是不是发给自己的，乳沟不是发给自己的则丢弃；相对的，交换机的端口不核对接收方 MAC 地址，而是直接接收所有的包并放到缓冲区中。因此，和网卡不同，交换机的端口不具有 MAC 地址。

将包存入缓冲区后，接下来需要查询一下这个包的接收方 MAC 地址是否已经在 MAC 地址表中有记录了。

交换机的 MAC 地址表主要包含两个信息：

* 一个是设备的 MAC 地址
* 另一个是该设备连接在交换机的哪个端口上

> 交换机内部有一张 MAC 地址与网线端口的映射表。当接收到包时，会将相应的端口号和发送 MAC 地址写入表中，这样就可以根据地址判断出该设备连接在哪个端口上了。交换机就是根据这些信息判断应该把包转发到哪里的。
>
> <img src="https://mmbiz.qpic.cn/mmbiz_jpg/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvBd1zjI0wTj16RGEP45hOVYIVwuUoSfpNU25hOKCzXfUuicibarvJ48kw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:67%;" />

举个例子，如果收到的包的接收方 MAC 地址为  00-02-B3-1C-9C-F9，则与表中第3行匹配，根据端口列的信息，可知这个地址位于3号端口上，然后就可以通过交换电路将包发送到相应的端口了。

所以，<u>交换机根据 MAC 地址表查找 MAC 地址，然后将信号发送到相应的端口。</u>

### 当 MAC 地址表找不到指定的 MAC 地址会怎么样？

地址表中找不到指定的 MAC 地址。这可能是因为具有该地址的设备还没有向交换机发送过包，或者这个设备一段时间没有工作导致地址被从地址表中删除了。

这种情况下，交换机无法判断应该把包转发到哪个端口，只能将包转发到除了源端口之外的所有端口上，无论该设备连接在哪个端口上都能收到这个包。

这样做不会产生什么问题，因为以太网的设计本来就是将包发送到整个网络的，然后<u>**只有相应的接收者才接收包，而其他设备则会忽略这个包。**</u>

有人会说：“这样做会发送多余的包，会不会造成网络拥塞呢？”

其实完全不用过于担心，因为发送了包之后目标设备会作出响应，只要返回了响应包，交换机就可以将它的地址写入 MAC 地址表，下次也就不需要把包发送到所有端口了。

局域网中每秒可以传输上千个包，多出一两个包并无大碍。

此外，如果接收方 MAC 地址是一个<u>广播地址</u>，那么交换机会将包发送到除源端口之外的所有端口。

以下两个属于广播地址：

* MAC 地址中的 FF:FF:FF:FF:FF:FF
* IP 地址中的 255.255.255.255

> 数据包通过交换机转发抵达了路由器，准备要离开土生土长的子网了

## 出境大门 —— 路由器

### 路由器与交换机的区别

网络包经过交换机后，现在到达了路由器，并在此被转发到下一个路由器或目标设备。

这一步转发的工作原理和交换机类似，也是通过查表判断包的转发目标。

不过在具体的操作过程上，路由器和交换机是有区别的。

* 因为路由器是基于 IP 设计的，俗称三层网络设备，路由器的各个端口都具有 MAC地址和 IP 地址
* 而交换机是基于以太网设计的，俗称二层网络设备，交换机的端口不具有 MAC 地址。

### 路由器基本原理

路由器的端口具有 MAC 地址，因此它就能够称为以太网的发送方和接收方；同时还具有 IP 地址，从这个意义上来说，它和计算机网卡是一样的。

当转发包时，首先路由器端口会接收发给自己的以太网包，然后路由表查询转发目标，再由相应的端口作为发送方将以太网包发送出去。

### 路由器的包接收操作

首先，电信号到达网线接口部分，路由器中的模块会将电信号转成数字信号，然后通过包末尾的 FCS 进行错误校验。

如果没问题则检查 MAC 头部中的接收方 MAC 地址，看看是不是发给自己的包，如果是就放到缓冲区中，否则就丢弃这个包。

总的来说，路由器的端口都具有 MAC 地址，只接收与自身地址匹配的包，遇到不匹配的包则直接丢弃。

### 查询路由表确定输出端口

完成包接收操作之后，路由器就会去掉包开头的 MAC 头部。

MAC 头部的作用就是将包送达路由器，其中的接收方 MAC 地址就是路由器端口的 MAC 地址。因此，当包到达路由器之后，MAC 头部的任务就完成了，于是 MAC 头部就会被丢弃。

接下来，路由器会根据 MAC 头部后方的 IP  头部中的内容进行包的转发操作。

转发操作分为几个阶段，首先是查询路由表判断转发目标。

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvyX1FEqkw7A0mBUbp1kDwK6X0XJe8P3bHia3ljXFGI3gfLZUnJyR5q6A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

具体的工作流程根据上图，举个例子。

假设地址为 10.10.1.101 的计算机要向地址为 192.168.1.100 的服务器发送一个包，这个包首先到达图中的路由器。

判断转发目标的第一步，就是根据包的接收方 IP 地址查询路由表中的目标地址栏，以找到相匹配的记录。

路由匹配和前面讲的一样，每个条目的子网掩码和 192.168.1.100 IP 做 & 与运算后，得到的结果与对应条目的目标地址进行匹配，如果匹配就会作为候选转发目标，如果不匹配就继续与下个条目进行路由匹配。

如第二条目的子网掩码 255.255.255.0 与 192.168.1.100 IP 做 & 与运算后，得到结果是 192.168.1.0，这与第二条条目的目标地址 192.168.1.0 匹配，该第二条目记录就会被作为转发目标。

实在找不到匹配路由时，就会选择默认路由，路由表中子网掩码为 0.0.0.0 的记录表示默认路由。

### 路由器的发送操作

接下来就会进入包的发送操作。

首先，我们需要根据路由表的网关列判断对方的地址。

* 如果网关是一个 IP 地址，则这个 IP 地址就是我们要转发到的目标地址，还未抵达终点，还继续需要路由器转发
* 如果网关为空，则 IP 头部中的接收方 IP 地址就是要转发到的目标地址，也就是最终找到 IP 包头 里的目标地址了，说明已抵达终点。

知道对方的 IP 地址后，接下来需要通过 ARP 协议根据 IP 地址查询 MAC 地址，并将查询结果作为接收方 MAC 地址。

路由器也有 ARP 缓存，因此首先会在 ARP 缓存中查询，如果找不到则发送 ARP 查询请求。

接下来是发送方 MAC 地址字段，这里填写输出端口的 MAC 地址。还有一个以太类型字段，填写 0080（十六进制）表示 IP 协议。

网络包完成后，接下来会将其转换成电信号并通过端口发送出去。这一步的工作过程和计算机也是相同的。

发送出去的网络包会通过交换机到达下一个路由器。由于接收方 MAC 地址就是下一个路由器的地址，所以交换机会根据这一地址将包传输到下一个路由器。

接下来，下一个路由器会将包转发给再下一个路由器，经过层层转发之后，网络包就到达了最终的目的地。

在网络包传输的过程中，源 IP 和目标 IP 始终是不会变的，一直变化的是 MAC 地址，因为需要 MAC 地址在以太网内进行两个设备之间的包传输。

## 互相扒皮 —— 服务器 与 客户端

<img src="https://mmbiz.qpic.cn/mmbiz_png/J0g14CUwaZdCwxNydn5YuT0s7aLuqWCvv55hSUSrw3kicf3mvfwRtibaqWnRBgtxDoXBklA4kokSqEfhMzicEe1lA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" style="zoom:80%;" />

数据包抵达服务器后，服务器会先扒开数据包的 MAC 头部，查看是否和服务器自己的 MAC 地址符合，符合就将包收起来

接着继续扒开数据包的 IP 头，发现 IP 地址符合，根据 IP 头中协议项，知道自己上层是 TCP 协议。

于是，扒开 TCP 的头，里面有序列号，需要看一看这个序列号是不是我们想要的，如果是就放入缓存中然后返回一个 ACK，如果不是就丢弃。TCP 头部里面还有端口号，HTTP 的服务器正在监听这个端口号。

于是，服务器自然就知道是 HTTP 进程想要这个包，于是就将包发给 HTTP 进程。

服务器的 HTTP 进程看到，原来这个请求是要访问一个页面，于是就把这个网页封装在 HTTP 响应报文里。

HTTP 响应报文也需要穿上TCP、IP、MAC 头部，不过这次源地址是服务器 IP地址，目的地址是客户端 IP 地址。

串号头部衣服后，从网卡出去，交由交换机转发到出城的路由器，路由器就把响应数据包发到下一个路由器。

最后跳到了客户端的城门把手的路由器，路由器扒开 IP 头部发现是要找城内的人，于是把包发给了城内的交换机，再由交换机转发到客户端。

客户端收到了服务器的响应数据包后，把收到的数据包打开剩下 HTTP 响应报文后，交给浏览器去渲染页面

最后，客户端向服务器发起了 TCP 四次回收，至此双方데连接就断开了。

### 一个数据包臭不要脸的感受

可靠传输的 TCP、远程定位的IP、指明下一站位置的 MAC，在交换机和路由器的转发下，抵达了目的地。



[^1]: 现在 302 叫 FOUND 了， 不是 Moved Temporarily
[^2]:这个地方还挺有意思的, 根DNS返回顶级DNS这个很好理解, 毕竟顶级DNS就只有那么几个, 而顶级DNS返回权威DNS这个就有点意思了, 我理解, 其实顶级DNS里已经存储了每个网址的名字, 但是对应IP是权威DNS, 相当于一批网址对应的IP具体信息放在某一台权威DNS上, 具体信息要到那台权威DNS上查看.



