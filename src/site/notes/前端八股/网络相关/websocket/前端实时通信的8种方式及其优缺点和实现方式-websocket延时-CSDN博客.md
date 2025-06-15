---
{"dg-publish":true,"permalink":"/前端八股/网络相关/websocket/前端实时通信的8种方式及其优缺点和实现方式-websocket延时-CSDN博客/","created":"2025-05-25T11:37:43.419+08:00","updated":"2025-06-15T13:14:55.167+08:00"}
---

[Websocket](Websocket.md)
[轮询与websocket](轮询与websocket.md)
## 1.短轮询

短轮询的原理很简单，每隔一段时间客户端就发出一个请求，去获取服务器最新的数据，一定程度上模拟实现了即时通讯。

- 优点：兼容性强，实现非常简单
- 缺点：延迟性高，请求中有大半是无用，非常消耗带宽和服务器资源，影响性能
- 应用： 二维码扫码确认、信息通知
- 实现方式：  
    借用定时器实现短轮询

```js
created(){
	this.shortPolling = setInterval(function(){
	    that.getRuset()
	},5000)
},
...
getResult(){
	var that = this
	this.$axios('xxx,',post).then(res=>{
		if(res.code === 200){//拿到想要的结果
			 ...
			 //定时器是否清除由业务场景决定
			 clearInterval(this.shortPolling)
		}
	})
}
```

## 2.comet(长轮询、长连接)

comet有两种主要实现手段，一种是基于 [AJAX](https://so.csdn.net/so/search?q=AJAX&spm=1001.2101.3001.7020) 的长轮询（long-polling）方式，另一种是基于 Iframe 及 htmlfile 的流（streaming）方式，通常被叫做长连接。  
具体两种手段的操作方法请移步Comet技术详解：基于HTTP长连接的Web端实时通信技术

### 2.1、长轮询

客户端向服务器发送Ajax请求，服务器接到请求后hold住连接，直到有新消息才返回响应信息并关闭连接，客户端处理完响应信息后再向服务器发送新的请求。

- 优点：兼容性好，在无消息的情况下不会频繁的请求，资源浪费较小
- 缺点：服务器hold连接会消耗资源，返回数据顺序无保证，难于管理维护
- 应用： webQQ、开心网、校内，Hi网页版、Facebook IM等等
- 实现方式：  
    主要由后端hold住连接，我们就是正常的发送请求即可

```js
getResult(){
	var that = this
	this.$axios('xxx,',post).then(res=>{
		if(res.code === 200){
			...
		}else{
			this.getResult()
		}
		...
	})
}
```

正常来说我们前端会设置请求超时时间，那么我们就和后端约定，在超时范围内必须返回结果在前端即可。

### 2.2、长连接

在页面里嵌入一个隐蔵[iframe](https://so.csdn.net/so/search?q=iframe&spm=1001.2101.3001.7020)，将这个隐蔵iframe的src属性设为对一个长连接的请求或是采用xhr请求，服务器端就能源源不断地往客户端输入数据。 此方法已经过时，我推荐使用，毕竟现在都已经放弃iframe

- 优点：兼容性好，消息即时到达，不发无用请求
- 缺点：服务器维护长连接消耗资源
- 实例：Gmail聊天
- 实现方式：

```js
//在vue中嵌入iframe
<iframe ref="iframe" v-show="iframeShow"></iframe>

watchIframe(){
	//先找到iframe的窗口
	this.iframeWin = this.$refs.iframe.contentWindow;
	//向iframe发送信息,大括号内是发送的内容;
	this.iframeWin.postMessage(
	     { 
	
	      },"*"
	);
	//怎样监听iframe传过来的信息
	window.addEventListener("message", this.handleMessage);
	//获取iframe传过来的信息
	handleMessage(res){
	  //res为传过来的信息
	 ...//渲染页面
	}
}
```

## 3.SSE 使用指南请看Server-Sent Events 教程

SSE（Server-Sent Event，服务端推送事件）是一种允许服务端向客户端推送新数据的HTML5技术

- 优点：基于HTTP而生，因此不需要太多改造就能使用，使用方便，而websocket非常复杂，必须借助成熟的库或框架
- 缺点：基于文本传输效率没有websocket高，不是严格的双向通信，客户端向服务端发送请求无法复用之前的连接，需要重新发出独立的请求，并且不兼容IE

```js
source.addEventListener('open', function (event) {
  // ...
}, false);
//客户端收到服务器发来的数据，就会触发message事件，可以在onmessage属性的回调函数。
source.addEventListener('message', function (event) {
  var data = event.data;
  // handle message
}, false);

//如果发生通信错误（比如连接中断），就会触发error事件，可以在onerror属性定义回调函数。
source.addEventListener('error', function (event) {
  // handle error event
}, false);

//close方法用于关闭 SSE 连接。
source.close();
```

我们也可以自定义事件，Server-Sent Events 教程里都有明确的使用方法

## 4.Websocket

Websocket是一个全新的、独立的协议，基于TCP协议，与http协议兼容、却不会融入http协议，仅仅作为html5的一部分，其作用就是在服务器和客户端之间建立实时的双向通信。

- 优点：真正意义上的实时双向通信，性能好，低延迟
- 缺点：独立与http的协议，因此需要额外的项目改造，使用复杂度高，必须引入成熟的库，无法兼容低版本浏览器
- 实现方式：

浏览器为 HTTP 通信提供了 XMLHttpRequest 对象，同样的，也为 WebSocket 通信提供了一个通信操作接口：WebSocket。

```js
 var ws = new WebSocket("wss://echo.websocket.org");

  // 当连接建立成功，触发 open 事件
  ws.onopen = function(evt) {
    console.log("建立连接成功 ...");

    // 连接建立成功以后，就可以使用这个连接对象通信了
    // send 方法发送数据
    ws.send("Hello WebSockets!");
  };

  // 当接收到对方发送的消息的时候，触发 message 事件
  // 我们可以通过回调函数的 evt.data 获取对方发送的数据内容
  ws.onmessage = function(evt) {
    console.log("接收到消息: " + evt.data);

    // 当不需要通信的时候，可以手动的关闭连接
    // ws.close();
  };

  // 当连接断开的时候触发 close 事件
  ws.onclose = function(evt) {
    console.log("连接已关闭.");
  }
```

## 5.Web Worker

Web Worker 的作用，就是为 JavaScript 创造多线程环境，允许主线程创建 Worker 线程，将一些任务分配给后者运行

- 优点：实现多线程环境，摆脱了js的单线程
- 缺点：无法访问DOM节点；无法访问全局变量或是全局函数；无法调用alert()或者confirm之类的函数；无法访问window、document之类的浏览器全局变量；  
    注意：**Web Worker中的Javascript依然可以使用setTimeout(),setInterval()之类的函数，也可以使用XMLHttpRequest对象来做Ajax通信**
- 实例：大数据的处理；高频的用户交互：
- 实现方式：

Web workers可分为两种类型：专用线程、共享线程。  
专用线程随当前页面的关闭而结束；这意味着专用线程只能被创建它的页面访问。  
与之相对应的共享线程可以被多个页面访问。

### 5.1、专用线程

使用 onmessage() ， postmessage()通信

```js
/** 主线程 **/
//注册专用线程
let worker = new Worker ('worker.js')
worker.onmessage = (e) => {
  console.log(e.data) // I post a message to main thread
}
worker.postMessage('main thread got a message')
 
/**  子线程 worker.js  **/
onmessage = (e) => {
    console.log(e.data) // main thread got a message
}
postMessage('I post a message to main thread')

// 在主线程中终止
worker.terminate()
 
// 在子线程中终止自身
self.close()

```

### 5.2、共享线程

SharedWorker需要用到port属性，接收需要先connect

```js
//注册共享线程
let worker = new SharedWorker("sharedworker.js");
/**  主线程  **/
worker.port.onmessage = function(e){}
worker.port.postMessage('data');
 
/** 子线程 **/
addEventListener('connect', function(event){
    var port = event.ports[0]
    //接收
    port.onmessage = function(event){
        console.log(event.data);
    };
    //发送
    port.postMessage("data");
    port.start();
});

// 在主线程中终止
worker.terminate()
 
// 在子线程中终止自身
self.close()
```

两种方式的错误监听同SSE一样

```js
worker.addEventListener("error", function(evt){  
	alert("Line #" + evt.lineno + " - " + evt.message + " in " + evt.filename);  
	}, false);  
	worker.postMessage(10000);  
});  
```

## 6.Service workers

Service workers 本质上充当Web应用程序与浏览器之间的代理服务器，也可以在网络可用时作为浏览器和网络间的代理，创建有效的离线体验。 它是 Web Worker 的一个类型

- 优点：可以秒开或者离线访问
- 缺点：IE11 、Opera Mini 、IOS不支持
- 应用：推送通知 — 允许用户选择从网络应用程序及时更新。
- 实现方式：

```js
// serviceWorker.js
import { register } from 'register-service-worker'

if (process.env.NODE_ENV === 'production') {
  register('service-worker.js', {
    ready () {
      console.log(
        'App is being served from cache by a service worker.'
      )
    },
    registered () {
      console.log('Service worker has been registered.')
    },
    cached () {
      console.log('Content has been cached for offline use.')
    },
    updatefound () {
      console.log('New content is downloading.')
    },
    updated () {
      console.log('New content is available; please refresh.')
      window.location.reload(true)   // 这里需要刷新页面
    },
    offline () {
      console.log('No internet connection found. App is running in offline mode.')
    },
    error (error) {
      console.error('Error during service worker registration:', error)
    }
  })
}

```

在 plugins 加入

```js
plugins: [
    new SWPrecacheWebpackPlugin({
      cacheId: 'my-project-name',
      filename: 'service-worker.js',
      staticFileGlobs: ['dist/**/*.{js,html,css}'],
      minify: true,
      stripPrefix: 'dist/'
    }),

    new WebpackPwaManifest({
      name: 'My Progressive Web App',
      short_name: 'MyPWA',
      description: 'My awesome Progressive Web App!',
      background_color: '#ffffff',
      crossorigin: 'use-credentials', //can be null, use-credentials or anonymous
      icons: [
        {
          src: path.resolve('src/assets/icon.png'),
          sizes: [96, 128, 192, 256, 384, 512] // multiple sizes
        },
        {
          src: path.resolve('src/assets/large-icon.png'),
          size: '1024x1024' // you can also use the specifications pattern
        }
      ]
    }),
    // ...
]

```

这个时候打包出来的代码根目录里面多了个 service-worker.js ，html文件里面 pwa 相关元素也加上了。  
在入口 main.js 引入该文件：

```js
import './serviceWorker'
```

## 7、Flash Socket

在页面中内嵌入一个使用了Socket类的 Flash 程序JavaScript通过调用此Flash程序提供的Socket接口与服务器端的Socket接口进行通信，JavaScript在收到服务器端传送的信息后控制页面的显示。 一般用在网络游戏中，web端基本不适用，加上早在 2017 年 7 月，Flash 的娘家 Adobe 已宣布在 2020年 底终止对 Flash 的支持。各个浏览器也在2020年底左右终止对 Flash 的支持

- 优点：实现真正的即时通信，而不是伪即时。
- 缺点：客户端必须安装Flash插件；非HTTP协议，无法自动穿越防火墙。
- 实例：网络互动游戏。
- 实现方式：因为都已经抛弃了，加上我并非游戏类前端，我就没了解Flash实现方式，有兴趣的小伙伴可以自行去研究一下

## 8、总结

- 我在实际项目中，只使用过短轮询和长轮询，其他的实时通讯方法并没有真正使用过（业务场景并没有其他需求）而且后端也给不了太多支持来实现是否可行。
- 长轮询与服务器的通信会比短轮询更实时，短轮询是在采用定时器，定时器就有时间差，比如我们定时5秒钟。可能一秒钟内我们就实现了数据通信，那么会有4秒的等待时间。而长轮询就可以这个顾虑。
- 是否可以使用回调递归实现实时通信，可以，他类比短轮询，但是回调递归并发量太大了，很容易造成服务器死机，并且消耗宽带影响到前端性能，所以我们正常不会使用回调递归实现，而且回调递归也不叫作短轮询。
- 为了方便以后使用，并单纯的学习。
- 此次总结是看了N篇文章的结合，有不足之处，敬请指出。
