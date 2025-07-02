---
{"dg-publish":true,"permalink":"/01_HTML+CSS/HTML/","created":"2025-06-22T10:46:28.670+08:00","updated":"2025-07-02T21:20:05.494+08:00"}
---

# HTML核心

## 1.第一个网页
**`!`**+**`Enter`**：自动生成HTML代码片段
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <!--  -->
  <a href="https://www.google.com.hk/" title="谷歌">google</a>
</body>
</html>
```
### 注释

注释为代码的阅读者提供帮助，注释不参与运行
在HTML中，注释使用如下格式书写：

```html
<!-- 注释内容 -->
```
`ctrl`+`?`

### 元素

> 其他叫法：标签、标记

```html
  <a href="https://www.google.com.hk/" title="谷歌">google</a>

  <title>google</title>
```

整体：element （元素）

元素 = 起始标记（begin tag） + 结束标记（end tag） + 元素内容 + 元素属性

属性 = 属性名 + 属性值

属性的分类：

- 局部属性：某些元素特有的属性
- 全局属性：所有元素通用


```html
<meta charset="UTF-8">
```

有些元素没有结束标记，这样的元素叫做：**空元素**

空元素的两种写法：

1. ```<meta charset="UTF-8">```
2. ```<meta charset="UTF-8" />```


### 元素的嵌套

元素不能相互嵌套

父元素、子元素、祖先元素、后代元素、兄弟元素（拥有同一个父元素的两个元素）

### 标准的文档结构

HTML：页面、HTML文档

```html
<!DOCTYPE html>
```

==文档声明==，告诉浏览器，当前文档使用的HTML标准是HTML5。

不写文档声明，将导致浏览器进入怪异渲染模式。

```html
<html lang="en">
</html>

<html lang="cmn-hans">
</html>
```

**cmn-hans**:最新的中文表达，而不是zh-CN

==根元素==，一个页面最多只能一个，并且该元素是所有其他元素的父元素或祖先元素。

HTML5版本中没有强制要求书写该元素

lang属性：language，全局属性，表示该元素内部使用的文字是使用哪一种自然语言书写而成的。

```html
<head>

</head>
```

==文档头==，文档头内部的内容，不会显示到页面上。

```html
<meta>
```

文档的元数据：附加信息。

charset：指定网页内容编码。

*计算机中，只能存储数字,文字和数字进行对应*
*比如：a —— 97， A —— 64*
*该字典叫做字符编码表，GB2312，GBK*

UTF-8 是 Unicode 编码的一个版本

```html
<title>Document</title>
```

==网页标题==

```html
<body>
</body>
```

==文档体==，页面上所有要参与显示的元素，都应该放置到文档体中。
## 2.语义化
### 什么是语义化
[[前端八股/HTML/前端面试 HTML篇_w3cschool#2. 对HTML语义化的理解|对HTML5语义化的理解]]

1. 每一个HTML元素都有具体的含义
	a元素：超链接
	p元素：段落
	h1元素：一级标题
2. 所有元素与展示效果无关
	元素展示到页面中的效果，应该由CSS决定。
	因为浏览器带有默认的CSS样式，所以每个元素有一些默认样式。
**重要：选择什么元素，取决于内容的含义，而不是显示出的效果**
```html
<h1>一级标题</h1>
<span style="font-weight: bold;font-size:2em;">一级标题</span>
```
一样的效果
### 为什么需要语义化？

1. 为了搜索引擎优化（SEO）

	搜索引擎：百度、搜搜、Bing、Google
	每隔一段时间，搜索引擎会从整个互联网中，抓取页面源代码

2. 为了让浏览器理解网页
	阅读模式、语音模式
## 3.文本元素
HTML5中支持的元素：[HTML5元素周期表](https://www.xuanfengge.com/funny/html5/element/)
![attachments 1/Paste-image-20250622.png](/img/user/01_HTML+CSS/attachments%201/Paste-image-20250622.png)
### h

标题：head

h1~h6：表示1级标题~6级标题

> [!note]- 小技巧
> 在vscode中输入`h$*6{$级标题}`，Emmet插件会自动生成以下内容
> `$`表示变量
> ![attachments 1/Paste-image-20250622-1.png](/img/user/01_HTML+CSS/attachments%201/Paste-image-20250622-1.png)
### p

段落，paragraphs

> lorem，乱数假文，没有任何实际含义的文字
> lorem1：只生成一个单词
> 快速生成：`p*6>lorem`

### span【无语义】

没有语义，仅用于设置样式

> 以前：某些元素在显示时会独占一行（块级元素），而某些元素不会（行级元素）
> 到了HTML5，已经弃用这种说法。

### pre

预格式化文本元素

**空白折叠**：在源代码中的连续空白字符（空格、换行、制表），在页面显示时，会被折叠为一个空格。

例外：在pre元素中的内容不会出现空白折叠

在pre元素内部出现的内容，会按照源代码格式显示到页面上。
![attachments/Paste-image-20250622-1.png](/img/user/01_HTML+CSS/attachments/Paste-image-20250622-1.png)
该元素通常用于在网页中显示一些代码。

pre元素功能的本质：它有一个默认的css属性

> 显示代码时，通常外面套code元素，code表示代码区域。
## 4.HTML实体

实体字符， HTML Entity

实体字符通常用于在页面中显示一些特殊符号。

1. ==&单词==;
2. ==&#数字==;

[list2table]

- 小于符号

	\&lt;

- 大于符号

	\&gt;

- 空格符号

	\&nbsp;

- 版权符号

	\&copy;

- &符号

	\&amp;
## 5.a元素

超链接

### href属性

hyper *reference*(引用)：通常表示跳转地址

1. 普通链接
2. 锚链接
	 `#+id`
	id属性：全局属性，表示元素在文档中的唯一编号
3. 功能链接
	点击后，触发某个功能
	- 执行JS代码，javascript:
	- 发送邮件，mailto:
	要求用户计算机上安装有邮件发送软件：exchange
	- 拨号，tel:
	要求用户计算机上安装有拨号软件，或使用的是移动端访问

[scroll]

```html
<!DOCTYPE html>

<html lang="en">

<head>

  <meta charset="UTF-8">

  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>Document</title>

</head>

<body>

  <!-- 功能链接 -->

  <a href="Javascript:alert('hello world')">弹出helloword</a>

  <br>

  <a href="mailto:m17179656827@163.com">发送邮件给我</a>

  <br>

  <a href="tel:10086">打电话</a>

  <br>

  <!-- 锚链接 -->

  <a href="#chapter1">章节1</a>

  <a href="#chapter2">章节2</a>

  <a href="#chapter3">章节3</a>

  <a href="#chapter4">章节4</a>

  <a href="#chapter5">章节5</a>

  <a href="#chapter6">章节6</a>

  <h1 id="chapter1">章节1</h1>

  <p>Lorem ipsum dolor sit, amet consectetur adipisicing elit. Facilis exercitationem veritatis enim debitis nam at aut quae, modi cupiditate accusantium distinctio non fugiat tempora impedit nostrum ab, blanditiis ratione sapiente. Sed fugiat </p>

  <h1 id="chapter2">章节2</h1>

  <p>Quia quos libero quis optio numquam, nihil iure impedit minus sapiente sint in eligendi accusamus corrupti pariatur! Expedita</p>

  <h1 id="chapter3">章节3</h1>

  <p>Nulla, voluptas corporis. Modi sint molestias placeat non deserunt atque aperiam? Officiis itaque ex nostrum impedit, nulla accusantium accusamus fugiat sint ipsum quibusdam provident eveniet vero sed a perferendis maiores non ipsam aspernatur q</p>

  <h1 id="chapter4">章节4</h1>

  <p>Nulla, voluptas corporis. Modi sint molestias placeat non deserunt atque aperiam? Officiis itaque ex nostrum impedit, nulla accusantium accusamus fugiat sint ipsum quibusdam provident eveniet vero sed a perferendis maiores non ipsam aspernatur q</p>

  <h1 id="chapter5">章节5</h1>

  <p>ernatur eius beatae. Necessitatibus sed neque atque ad! Tenetur praesentium consequatur omnis iure inventore molestiae animi quas, amet expedita dignissimo</p>

  <h1 id="chapter6">章节6</h1>

  <p>Eligendi in enim asperiores quibusdam suscipit, optio laborum obcaecati </p>

</body>

</html>
```
### target属性

表示跳转窗口位置。

target的取值：

- _self：在当前页面窗口中打开，默认值
- _blank: 在新窗口中打开
## 6.路径的写法
### 站内资源和站外资源

站内资源：当前网站的资源

站外资源：非当前网站的资源

### 绝对路径和相对路径

站外资源：绝对路径

站内资源：相对路径

1. 绝对路径

绝对路径的书写格式：

url地址：

```
协议名://主机名:端口号/路径

schema://host:port/path
```

当跳转目标和当前页面的协议相同时，可以省略协议

2. 相对路径

以`./`开头，`./`表示当前资源所在的目录

可以书写`./../`表示返回上一级目录

相对路径中：`./`可以省略
## 7.图片元素
### img元素

image缩写，空元素

- src属性：source

- alt属性：当图片资源失效时，将使用该属性的文字替代图片

```html
<img src='./solar.jpg' alt="这是一张太阳系图片">
```

### 和a元素联用
```html
<a target="_blank" href="https://baike.baidu.com/item/%E">
	<img src="./solar.jpg" alt="这是一张太阳系图片">
</a>
```
### 和map元素

>点击图片不同区域产生不同效果

map：地图

map的子元素：area

```html
  <a target="_blank" href="">

    <img usemap='#solarMap' src="" alt="这是一张太阳系图片">

  </a>
  <map name="solarMap">
    <area shape="circle" coords="672,789,90" href="" target="_blank">
  </map>
```

> [!NOTE]
> 圆形（圆心坐标、半径）
> 矩形（左上角坐标、右下角坐标）
> 多边形（每一个顶点的坐标）

衡量坐标时，为了避免衡量误差，需要使用专业的衡量工具：

ps、pxcook、cutpro
![attachments/Paste-image-20250623.png](/img/user/01_HTML+CSS/attachments/Paste-image-20250623.png)
### 和figure元素

指代、定义，通常用于把图片、图片标题、描述包裹起来

子元素：figcaption


[scroll]

```html
<body>

    <figure>

        <a target="_blank" href="https://baike.baidu.com/item/%E5%A4%AA%E9%98%B3%E7%B3%BB/173281?fr=aladdin">

            <img usemap="#solarMap" src="./img/solar.jpg" alt="这是一张太阳系的图片">

        </a>

        <figcaption>

            <h2>太阳系</h2>

        </figcaption>

        <p>

            太阳系是以太阳为中心，和所有受到太阳的引力约束天体的集合体。包括八大行星（由离太阳从近到远的顺序：水星、金星、地球、火星、木星、土星、天王星、海王星）、以及至少173颗已知的卫星、5颗已经辨认出来的矮行星和数以亿计的太阳系小天体,和哈雷彗星。

        </p>

    </figure>

  
  

    <map name="solarMap">

        <area shape="circle" coords="360,204,48" href="https://baike.baidu.com/item/%E6%9C%A8%E6%98%9F/222105?fr=aladdin" target="_blank">

        <area shape="rect" coords="323,282,395,320" href="https://baike.baidu.com/item/%E6%9C%A8%E6%98%9F/222105?fr=aladdin" target="_blank">

        <area shape="poly" coords="601,371,645,312,678,338,645,392" href="https://baike.baidu.com/item/%E5%86%A5%E7%8E%8B%E6%98%9F/137498?fr=aladdin" target="_blank">

    </map>

</body>
```


## 8.多媒体元素
video 视频

audio 音频

### video

- ==**controls**==: 控制控件的显示，取值只能为controls

- ==**布尔属性**==:某些属性，只有两种状态：1. 不写   2. 取值为属性名，这种属性叫做布尔属性

	- 布尔属性，在HTML5中，可以不用书写属性值

- ==autoplay==: 布尔属性，自动播放。

- ==muted==: 布尔属性，静音播放。

- ==loop==: 布尔属性，循环播放

```html
   <video src="./media/open.mp4"
  controls autoplay loop muted style="width:800px;"></video>
```
### audio

和视频完全一致


### 兼容性

1. 旧版本的浏览器不支持这两个元素
2. 不同的浏览器支持的音视频格式可能不一致

mp4、webm

为了更好的兼容性，上面的代码可以这么写，使用source元素

```html
<video controls autoplay muted loop style="width:500px;">
        <source src="media/open.mp4">
        <source src="media/open.webm">
        <p>
            对不起，你的浏览器不支持video元素，请点击这里下载最新版本的浏览器
        </p>
    </video>
```
## 9.列表元素
### 有序列表

- ol: ordered list

- li：list item 

属性
type：i（以罗马数字排序）、a（使用字母排序）、A（使用大写字母排序）
>除非是一些重要的法律条文，尽量避免使用type控制列表样式，而应该通过CSS属性进行控制

```html
  <ol type="i">
    <li>打开冰箱门</li>
    <li>大象进去</li>
    <li>冰箱门关上</li>
  </ol>
```
### 无序列表

把ol改成ul

ul：unordered list

无序列表常用于制作菜单 或 新闻列表。
![attachments/Paste-image-20250623-1.png](/img/user/01_HTML+CSS/attachments/Paste-image-20250623-1.png)
### 定义列表

通常用于一些术语的定义

> dl: definition list
> 
> dt: definition title
> 
> dd: definition description

```html
  <dl>
    <dt>HTML</dt>
    <dd>组成HTML文本的单元</dd>
  </dl>
```
## 10.容器元素
容器元素：该元素代表一个块区域，内部用于放置其他元素

### div元素

没有语义

### 语义化容器元素

- header: 通常用于表示页头，也可以用于表示文章的头部

- footer: 通常用于表示页脚，也可以用于表示文章的尾部

- article: 通常用于表示整篇文章

- section: 通常用于表示文章的章节

- aside: 通常用于表示侧边栏
## 11.元素包含关系

> 以前：块级元素可以包含行级元素，行级元素不可以包含块级元素，a元素除外

> 现在：元素的包含关系由元素的内容类别决定。符合语义。

例如，查看h1元素中是否可以包含p元素
不可以
![attachments/Paste-image-20250623-2.png](/img/user/01_HTML+CSS/attachments/Paste-image-20250623-2.png)
总结：

1. 容器元素中可以包含任何元素
2. a元素中几乎可以包含任何元素
3. 某些元素有固定的子元素（ul>li，ol>li，dl>dt+dd）
4. 标题元素和段落元素不能相互嵌套，并且不能包含容器元素
## 12.练习-百度新闻
仿百度新闻首页练习

[scroll]

```html
<!DOCTYPE html>

<html lang="en">

  

<head>

  <meta charset="UTF-8">

  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>百度新闻——海量中文资讯平台</title>

</head>

  

<body>

  <!-- 头部 -->

  <header>

    <!-- 顶部行 -->

    <div>

      <div>

        <ul>

          <li><a href="">网页</a></li>

          <li><a href="">新闻</a></li>

          <li><a href="">贴吧</a></li>

          <li><a href="">知道</a></li>

          <li><a href="">音乐</a></li>

          <li><a href="">图片</a></li>

          <li><a href="">视频</a></li>

          <li><a href="">地图</a></li>

          <li><a href="">文库</a></li>

        </ul>

      </div>

      <div>

        <ul>

          <li><a href="">百度首页</a></li>

          <li><a href="">我</a>

            <ul>

              <li><a href="">账号设置</a></li>

              <li><a href="">退出</a></li>

            </ul>

          </li>

        </ul>

      </div>

    </div>

    <!-- 搜索行 -->

    <div>

      <div>

        <a href="https://news.baidu.com/">

          <img src="./image/log-news.png" alt="百度新闻logo" style="width:600px;">

        </a>

      </div>

      <div>

        <input type="text">

        <button>

          百度一下

        </button>

      </div>

      <div>

        <a href="">帮助</a>

      </div>

    </div>

  </header>

  

  <!-- 中间主体 -->

  <div>

    <!-- 左边区域 -->

    <div>

      <div>

        <h2>热点要闻</h2>

      </div>

      <div>

        <ul>

          <li>

            <h3>Lorem ipsum dolor sit amet consectetur adipisicing elit.</h3>

          </li>

          <li>Lorem ipsum dolor sit amet consectetur adipisicing elit. Distinctio dignissimos sit, sint quae,

            necessitatibus voluptates cumque vitae, non aliquam quisquam delectus blanditiis nisi quibusdam? Sed vel

            laudantium ea iste nam!</li>

          <li>Nulla, commodi nobis ullam itaque ratione sit et odit, architecto iure recusandae esse exercitationem quam

            iusto laudantium tempore soluta. Quis recusandae praesentium ea quo sed repellat placeat eaque culpa atque!

          </li>

          <li>Sunt iure, laudantium accusamus veritatis incidunt blanditiis. Consectetur provident iusto reiciendis

            animi doloremque laboriosam porro praesentium dolor assumenda ea quibusdam, maiores incidunt, perspiciatis

            perferendis impedit nemo. Molestiae, sed doloremque? Sit.</li>

          <li>Maxime ex similique reprehenderit, odit quo tenetur repudiandae rem possimus ullam dolores voluptatibus,

            qui dolor maiores velit sit blanditiis provident natus delectus quis placeat labore autem perspiciatis?

            Provident, aliquam voluptatibus?</li>

        </ul>

        <ul>

          <li>

            <h3>Tempora voluptates recusandae vero dolorum? Quo, amet perferendis.</h3>

          </li>

          <li>Lorem ipsum, dolor sit amet consectetur adipisicing elit. Magnam cupiditate ab numquam doloremque

            dignissimos aut ex modi neque ullam ducimus a cumque quibusdam corrupti labore, optio velit, nam

            consequuntur dolores.</li>

          <li>Dolorem impedit ea, perspiciatis dignissimos, voluptatem reprehenderit quibusdam quia dolor unde accusamus

            inventore, voluptatum dolorum aliquam odio deleniti itaque debitis earum nesciunt ad cumque at. Dolores

            ipsum deleniti illo aperiam!</li>

          <li>Omnis modi reprehenderit aliquid alias sed est, fugit quos. Amet minus, velit aliquid voluptatum placeat

            provident ipsam vitae enim a obcaecati magni porro, repudiandae eaque corporis tenetur soluta ea maxime.

          </li>

          <li>Quos molestias quod est placeat, sint omnis quis numquam voluptate dolorem fuga. Iusto quo voluptatum

            ducimus excepturi autem velit at, nobis recusandae nostrum amet quod, ipsam consectetur possimus dolorum

            fugit.</li>

        </ul>

        <ul>

          <li>

            <h3>Doloremque quaerat necessitatibus consequuntur maxime inventore vitae impedit.</h3>

          </li>

          <li>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Non ducimus veniam libero. Soluta accusantium,

            ad numquam sed quasi commodi ea quidem cupiditate repellendus, sint, dolorum explicabo consequuntur qui

            velit impedit!</li>

          <li>Atque non eius dolor rem ipsa provident minus eveniet voluptatibus dolorem porro autem, dolorum distinctio

            voluptatem qui architecto a exercitationem commodi unde eligendi assumenda! Optio omnis tempora quis

            incidunt aut.</li>

          <li>Aliquam doloribus aut eos earum facilis nisi. Accusamus voluptas animi earum, aut qui deleniti cum facere

            repellendus explicabo excepturi modi pariatur quod, perspiciatis culpa dolorum voluptatibus. Reiciendis

            ipsam aliquam sit?</li>

          <li>Iure eveniet dolorem illo, consequuntur officia quos corporis vel. Ea consequatur inventore error porro

            enim sed et minus, laborum aliquid mollitia dolores provident iste sapiente, nisi saepe non ipsum incidunt.

          </li>

        </ul>

      </div>

    </div>

    <!-- 右边区域 -->

    <div>

      <!-- 上边区域 -->

      <div>

        <!-- 轮播图主体 -->

        <div>

          <!-- 图片+标题 -->

          <div>

            <div>

              <div>

                <a href=""><img src="./image/banner01.jpeg" alt="" target="_blank">

                  <h3>Lorem ipsum dolor sit amet.</h3>

                </a>

              </div>

              <div>

                <a href=""><img src="./image/banner02.jpeg" alt="" target="_blank">

                  <h3>Lorem ipsum dolor sit amet.</h3>

                </a>

              </div>

            </div>

          </div>

          <!-- 左右箭头 -->

           <div>

            <span>&lt</span><span>&gt</span>

           </div>

           <!-- 点点点 -->

          <div>

            <ul>

              <li></li>

              <li></li>

            </ul>

          </div>

        </div>

        <!-- 广告 -->

        <div>

          <a href=""><img src="./image/ad.png" alt=""></a>

        </div>

      </div>

      <!-- 下边区域 -->

      <div>

        <!-- 热搜词 -->

         <div>

          <h3>热搜新闻词<span>HOT WORDS</span></h3>

         </div>

         <div>

          <ul>

            <li>Lorem.</li>

            <li>Eveniet!</li>

            <li>Repudiandae?</li>

            <li>Soluta?</li>

            <li>Tenetur.</li>

          </ul>

         </div>

      </div>

    </div>

  </div>

  <!-- 页脚 -->

  <footer>

    <p>

      <a href="">用户协议</a>

      <a href="">隐私策略</a>

      <a href="">企业推广</a>

      <a href="">投诉中心</a>

      京公网安备11000002000001号 《互联网新闻信息服务许可》编号：11220180008 《互联网宗教信息服务许可证》编号：京（2022）0000043 ©2025Baidu 使用百度前必读

    </p>

  </footer>

</body>

  

</html>
```

# HTML进阶
## 1.iframe元素

框架页
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250702-1.png)
通常用于在网页中嵌入另一个页面

iframe 可替换元素

1. 通常行盒
2. 通常显示的内容取决于元素的属性
3. CSS不能完全控制其中的样式
4. 具有行块盒的特点
## 2.在页面中使用flash

在 HTML 中，Flash 曾是嵌入动态内容（如动画、视频、游戏）的主流技术，但随着 HTML5 的普及已逐渐被淘汰。

- object元素	
	它们都是可替换元素
	
	`type="application/x-shockwave-flash"`，type的值是资源的MIME类型。
	MIME(Multipurpose Internet Mail Extensions)
	
	多用途互联网邮件类型：
	
	比如，资源是一个jpg图片，MIME：image/jpeg
	- 子元素parm
	![](/img/user/01_HTML+CSS/attachments/Paste-image-20250702-2.png)
```html
<object data='./example.swf' type="application/x-shockwave-flash"></object>
```

- embed元素
	- 与object写法不同，功能相似
```html
<embed quality="high" src="./example.swf" type="application/x-shockwave-flash"></embed>
```
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250702-3.png)
## 3.表单元素

一系列元素，主要用于收集用户数据

### input元素

- 输入框
	- type属性：输入框类型
		type: text， 普通文本输入框
		type：password，密码框
		type: date, 日期选择框，兼容性问题
		type: search, 搜索框，兼容性问题
		type: number，数字输入框
		type: checkbox，多选框
		type: radio，单选框
		- 以上不同type有其特有的一些属性
	- value属性：输入框的值
	- placeholder属性：显示提示的文本，文本框没有内容时显示
	- checked属性：表示选中
	- input元素还有丰富的状态属性、限制输入属性、表单控制属性

`<input type="password" placeholder="请输入密码">`

- input元素可以制作按钮
	当type值为reset、button、submit时，input表示按钮。
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250702-4.png)

### select元素

下拉列表选择框
通常和option元素配合使用
- selected属性表示选中
#### 基本语法
```html
<select name="fruit">
  <option value="apple">苹果</option>
  <option value="banana">香蕉</option>
  <option value="orange">橙子</option>
</select>
```
#### selected常用属性

| 属性名         | 说明                                  | 示例                      |
| ----------- | ----------------------------------- | ----------------------- |
| `name`      | 表单提交时的键名                            | `<select name="city">`  |
| `id`        | 元素的唯一标识，可用于 JS 或 `<label for="id">` | `<select id="gender">`  |
| `required`  | 表示为必选字段                             | `<select required>`     |
| `disabled`  | 禁用选择框                               | `<select disabled>`     |
| `multiple`  | 允许多选，按 Ctrl 或 Shift 进行多选            | `<select multiple>`     |
| `size`      | 显示多少行选项（不设置时为下拉）                    | `<select size="3">`     |
| `autofocus` | 页面加载后自动聚焦                           | `<select autofocus>`    |
| `form`      | 指定该元素所属的表单 ID                       | `<select form="form1">` |
#### optgroup元素：选项分组
```html
<select name="country">
  <optgroup label="亚洲">
    <option value="cn">中国</option>
    <option value="jp">日本</option>
  </optgroup>
  <optgroup label="欧洲">
    <option value="uk">英国</option>
    <option value="fr">法国</option>
  </optgroup>
</select>

```
#### option元素常用属性

| 属性名        | 说明            | 示例                                  |
| ---------- | ------------- | ----------------------------------- |
| `value`    | 选项的实际值（提交时使用） | `<option value="cn">中国</option>`    |
| `selected` | 设置默认选中项       | `<option selected>`                 |
| `disabled` | 禁用该选项         | `<option disabled>`                 |
| `label`    | 提供选项的简短标签     | `<option label="China">中国</option>` |
### textarea元素

文本域，多行文本框
`<textarea name="comment"></textarea>`
### 按钮元素

button

type属性：reset、submit、button，默认值submit

`<button type="submit">提交</button>`

### 表单状态

readonly属性：布尔属性，是否只读，不会改变表单显示样式

disabled属性：布尔属性，是否禁用，会改变表单显示样式

### 配合表单元素的其他元素

#### label

普通元素，通常配合单选和多选框使用
`<label>` 元素是 HTML 表单中用于**定义标签文字**的元素，主要作用是**提升表单的可用性和可访问性**。它可以绑定到一个表单控件（如 `<input>`、`<select>`、`<textarea>`），**让用户点击文字时也能激活该控件**。

- 显示关联
	可以通过for属性，让label元素关联某一个表单元素，for属性书写表单元素id的值
	```html
	<label for="username">用户名：</label>
	<input type="text" id="username" name="username">

	```
- 隐式关联（嵌套写法）
	```html
	<label>
	  用户名：
	  <input type="text" name="username">
	</label>

	```

#### datalist元素

数据列表

该元素本身不会显示到页面，通常用于和普通文本框配合

```html
<label for="browser">请选择或输入浏览器：</label>
<input list="browsers" id="browser" name="browser">

<datalist id="browsers">
  <option value="Chrome">
  <option value="Firefox">
  <option value="Edge">
  <option value="Safari">
  <option value="Opera">
</datalist>

```
- `<input list="browsers">` 关联到 `<datalist id="browsers">`
    
- `<option>` 的 `value` 是可选项的值
    
- 用户既可以选，也可以输入其他不在列表中的值
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250702-5.png)
#### form元素

通常，会将整个表单元素，放置form元素的内部，作用是当提交表单时，会将form元素内部的表单内容以合适的方式提交到服务器。

form元素对开发静态页面没有什么意义。

```html
<form action="/submit" method="post">
  <label for="username">用户名：</label>
  <input type="text" id="username" name="username">
  
  <label for="password">密码：</label>
  <input type="password" id="password" name="password">
  
  <button type="submit">登录</button>
</form>

```

| 属性           | 说明                             | 示例                        |
| ------------ | ------------------------------ | ------------------------- |
| `action`     | 表单提交的目标地址（URL）                 | `<form action="/submit">` |
| `method`     | 提交方式：`get`（默认）或 `post`         | `<form method="post">`    |
| `target`     | 提交结果的展示位置（如 `_blank`, `_self`） | `<form target="_blank">`  |
| `name`       | 表单名称，可通过 JS 访问                 | `<form name="loginForm">` |
| `id`         | 唯一标识                           | `<form id="myForm">`      |
```html
    <form action="https://www.baidu.com/" method="GET">
        <p>
            账号：
            <input type="text" name="loginid">
        </p>
        <p>
            密码：
            <input type="password" name="loginpwd">
        </p>
        <p>
            <button type="submit">提交</button>
        </p>
    </form>
```
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250702-6.png)
#### fieldset元素

表单分组
`<fieldset>` 元素是 HTML 表单中用于**对表单中的控件进行分组**的标签，常与 `<legend>` 元素搭配使用，提升表单的**结构性与可读性**。
- `<legend>` 通常写在 `<fieldset>` 的**开头**。
- 内容会显示为该字段集的标题。

<fieldset>
  <legend>个人信息</legend>

  <label for="name">姓名：</label>
  <input type="text" id="name" name="name">

  <label for="email">邮箱：</label>
  <input type="email" id="email" name="email">
</fieldset>

```html
<fieldset>
  <legend>个人信息</legend>

  <label for="name">姓名：</label>
  <input type="text" id="name" name="name">

  <label for="email">邮箱：</label>
  <input type="email" id="email" name="email">
</fieldset>
```

## 4. 美化表单元素
### 新的伪类

1. focus

元素聚焦时的样式

2. checked

单选或多选框被选中的样式

### 常见用法

1. 重置表单元素样式

2. 设置textarea是否允许调整尺寸

css属性resize：

- both：默认值，两个方向都可以调整尺寸
- none：不能调整尺寸
- horizontal: 水平方向可以调整尺寸
- vertical：垂直方向可以调整尺寸

3. 文本框边缘到内容的距离

4. 控制单选和多选的样式
## 5.表单练习

## 6.表格元素
在css技术出现之前，网页通常使用表格布局。

后台管理系统中可能会使用表格。

前台：面向用户

后台：面向管理员。对界面要求不高，对功能性要求高。

表格不再适用于网页布局？表格的渲染速度过慢。
## 7.其他元素
1. abbr
	缩写词

2. time
    提供给浏览器或搜索引擎阅读的时间

3. b （bold）
    以前是一个无语义元素，主要用于加粗字体

4. q
    一小段引用文本

5. blockquote
    大段引用的文本

6. br
    无语义 主要用于在文本中换行

7. hr
    无语义 主要用于分割

8. meta
    还可以用于搜索引擎优化（SEO）

9. link
	链接外部资源（CSS、图标）
	
	rel属性：relation，链接的资源和当前网页的关系
	
	type属性：链接的资源的MIME类型