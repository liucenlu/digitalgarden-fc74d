---
{"dg-publish":true,"permalink":"/前端八股/网络相关/http/http和https的关系与区别/","created":"2025-05-25T13:24:32.141+08:00","updated":"2025-06-14T23:37:58.972+08:00"}
---

> [!NOTE]
> https是一个基于http的保密通信协议，它在http基础上增加了一个安全套接层，https由于需要在通信过程中进行加密解密，因此性能低于http，当然安全性高于http。在https网页中发送http的ajax请求将会被浏览器block，因为浏览器认为这是不安全的操作，而在http网页中发送https请求是被允许的。
> 安全性、端口号（http40、https443）、SEO效果、性能

[HTTPS的加密原理](HTTPS的加密原理.md)
[Session、Cookie、Token](Session、Cookie、Token.md)
### HTTP 和 HTTPS 的主要区别及它们之间的关系

HTTP（HyperText Transfer Protocol，超文本传输协议）是一种用于在网络上传输数据的应用层协议。它定义了客户端如何向服务器请求资源以及服务器如何响应这些请求的方式_1_。

HTTPS（HyperText Transfer Protocol Secure，安全的超文本传输协议）是在HTTP的基础上增加了SSL/TLS加密层的一种通信方式。通过这种机制，可以实现数据的安全传输，防止中间人攻击和窃听行为的发生_1_。

#### 主要区别

1. **安全性**
    
    - HTTP 是明文传输，任何第三方都可以轻松截获并读取其中的内容。
    - HTTPS 使用 SSL 或 TLS 加密技术来保护数据，在发送之前先对其进行加密处理后再传递给接收方解密查看原始信息_1_。
2. **端口号**
    
    - 默认情况下，HTTP 协议使用的端口为80；而HTTPS 则默认使用的是443端口_1_。
3. **性能影响**
    
    - 由于存在额外的握手过程与加解密操作等原因使得启用HTTPS 后可能会稍微增加一些延迟时间，但这部分差异随着硬件设备的进步已经变得越来越不明显。
4. **搜索引擎优化(SEO)效果**
    
    - 谷歌明确表示会将是否采用了HTTPS 安全连接作为一个轻量级正面信号纳入其桌面版搜索排名考量之中，并给予那些切换至HTTPS 版本页面更高的权重分数从而获得更好的曝光率表现机会相比仅支持标准模式下的竞争对手而言更具竞争力的优势地位_1_。
