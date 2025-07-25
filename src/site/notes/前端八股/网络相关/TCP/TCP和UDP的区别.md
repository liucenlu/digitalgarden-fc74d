---
{"dg-publish":true,"permalink":"/前端八股/网络相关/TCP/TCP和UDP的区别/","created":"2025-05-25T13:25:03.578+08:00","updated":"2025-06-14T23:38:18.173+08:00"}
---

> [!NOTE]
> - **TCP 是面向连接的协议**，传输前需要建立连接，提供**可靠传输**，有**三次握手**、**数据确认**、**重传机制**，适合如网页、文件传输等对可靠性要求高的场景。
>     
> - **UDP 是无连接的协议**，不保证数据可靠性，没有连接建立和确认机制，**传输速度快、开销小**，适用于视频通话、直播、DNS 等对**实时性要求高**的应用。

### TCP与UDP的主要区别

#### 1. **连接方式**

TCP是一种面向连接的协议，在传输数据之前需要先建立连接并完成三次握手过程_1_。相比之下，UDP是无连接的协议，无需事先建立连接即可直接发送数据_2_。

#### 2. **可靠性**

TCP提供了可靠的数据传输服务，能够确保数据无差错、不丢失、不重复，并按照顺序到达目标设备_3_。它通过确认机制、重传机制、排序功能以及流量控制等功能来保障数据的完整性_5_。而UDP仅提供“尽力而为”的服务模式，无法保证数据的可靠性或顺序性_4_。

#### 3. **性能表现**

由于其复杂的可靠性机制，TCP在资源占用方面较高，这可能导致传输效率相对较低_1_。相反，UDP因缺乏这些额外的功能模块，所以具有更低的系统开销和更高的运行速度。

#### 4. **头部结构复杂度**

TCP拥有较大的头部信息量（固定部分至少20字节），用于支持多种高级特性如窗口尺寸调整等操作。与此同时，UDP仅有简单的8字节头部设计，其中包括源端口号、目的端口号、总长度字段及检验和项_4_。

#### 5. **通信模型灵活性**

基于点到点特性的限制下，每条独立存在的TCP链路只能服务于两个特定终端之间的一对一交互需求_3_。但是，借助于广播或多播技术的支持，UDP允许实现更为灵活多样化的组网形式——既可维持传统意义上的单向交流关系，也能轻松构建起一对多乃至多方共同参与的大规模协作环境。

---

### TCP与UDP的适用场景分析

#### 使用TCP的情况

当应用程序对于数据准确性有着极高要求时，应当优先考虑采用TCP协议来进行网络通讯活动。例如文件下载上传过程中，任何一点细微的信息偏差都可能会造成整个文档内容变得毫无意义；又或者是在执行远程登录指令期间，每一个字符命令都需要被精确传达给服务器侧才能顺利完成相应任务_1_^。

#### 应用UDP的情形

如果某个业务场景更关注的是时间敏感型事务而非绝对精准的结果反馈，则可以选择运用UDP方案加以解决。典型例子包括在线音视频播放平台上的媒体流推送服务，即使偶尔存在个别帧画面卡顿现象也基本不会显著影响用户体验效果；还有诸如DNS域名解析查询请求这类短小精悍的消息传递场合也非常适配使用UDP^。