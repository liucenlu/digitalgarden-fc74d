---
{"dg-publish":true,"permalink":"/01_HTML+CSS/HTML/","created":"2025-06-22T10:46:28.670+08:00","updated":"2025-06-22T15:23:13.074+08:00"}
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

1. &单词;
2. &#数字;


- 小于符号

&lt;

- 大于符号

&gt;

- 空格符号

&nbsp;

- 版权符号

&copy;

- &符号

&amp;
## 5.a元素
超链接

### href属性

hyper reference：通常表示跳转地址

1. 普通链接
2. 锚链接

id属性：全局属性，表示元素在文档中的唯一编号

3. 功能链接

点击后，触发某个功能

- 执行JS代码，javascript:
- 发送邮件，mailto:

要求用户计算机上安装有邮件发送软件：exchange

- 拨号，tel:

要求用户计算机上安装有拨号软件，或使用的是移动端访问

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

以./开头，./表示当前资源所在的目录

可以书写../表示返回上一级目录

相对路径中：./可以省略
## 7.图片元素
### img元素

image缩写，空元素

src属性：source

alt属性：当图片资源失效时，将使用该属性的文字替代图片

### 和a元素联用

### 和map元素

map：地图

map的子元素：area

衡量坐标时，为了避免衡量误差，需要使用专业的衡量工具：

ps、pxcook、cutpro（本人开发）

### 和figure元素

指代、定义，通常用于把图片、图片标题、描述包裹起来

子元素：figcaption
## 8.多媒体元素
video 视频

audio 音频

### video

controls: 控制控件的显示，取值只能为controls

某些属性，只有两种状态：1. 不写   2. 取值为属性名，这种属性叫做布尔属性

布尔属性，在HTML5中，可以不用书写属性值

autoplay: 布尔属性，自动播放。

muted: 布尔属性，静音播放。

loop: 布尔属性，循环播放

### audio

和视频完全一致


### 兼容性

1. 旧版本的浏览器不支持这两个元素
2. 不同的浏览器支持的音视频格式可能不一致

mp4、webm
## 9.列表元素
### 有序列表

ol: ordered list

li：list item 

### 无序列表

把ol改成ul

ul：unordered list

无序列表常用于制作菜单 或 新闻列表。

### 定义列表

通常用于一些术语的定义

dl: definition list

dt: definition title

dd: definition description
## 10.容器元素
容器元素：该元素代表一个块区域，内部用于放置其他元素

### div元素

没有语义

### 语义化容器元素

header: 通常用于表示页头，也可以用于表示文章的头部

footer: 通常用于表示页脚，也可以用于表示文章的尾部

article: 通常用于表示整篇文章

section: 通常用于表示文章的章节

aside: 通常用于表示侧边栏
## 11.元素包含关系
以前：块级元素可以包含行级元素，行级元素不可以包含块级元素，a元素除外

元素的包含关系由元素的内容类别决定。

例如，查看h1元素中是否可以包含p元素

总结：

1. 容器元素中可以包含任何元素
2. a元素中几乎可以包含任何元素
3. 某些元素有固定的子元素（ul>li，ol>li，dl>dt+dd）
4. 标题元素和段落元素不能相互嵌套，并且不能包含容器元素
## 12.练习-百度新闻


# HTML进阶
## 1.iframe元素
框架页

通常用于在网页中嵌入另一个页面

iframe 可替换元素

1. 通常行盒
2. 通常显示的内容取决于元素的属性
3. CSS不能完全控制其中的样式
4. 具有行快盒的特点
## 2.在页面中使用flash
object

embed

它们都是可替换元素

MIME(Multipurpose Internet Mail Extensions)

多用途互联网邮件类型：

比如，资源是一个jpg图片，MIME：image/jpeg
## 3.表单元素
一系列元素，主要用于收集用户数据

### input元素

输入框

- type属性：输入框类型

type: text， 普通文本输入框
type：password，密码框
type: date, 日期选择框，兼容性问题
type: search, 搜索框，兼容性问题
type: number，数字输入框
type: checkbox，多选框
type: radio，单选框

- value属性：输入框的值
- placeholder属性：显示提示的文本，文本框没有内容时显示


input元素可以制作按钮

当type值为reset、button、submit时，input表示按钮。

### select元素

下拉列表选择框

通常和option元素配合使用

### textarea元素

文本域，多行文本框

### 按钮元素

button

type属性：reset、submit、button，默认值submit

### 表单状态

readonly属性：布尔属性，是否只读，不会改变表单显示样式

disabled属性：布尔属性，是否禁用，会改变表单显示样式

### 配合表单元素的其他元素

#### label

普通元素，通常配合单选和多选框使用

- 显示关联

可以通过for属性，让label元素关联某一个表单元素，for属性书写表单元素id的值

- 隐式关联

#### datalist

数据列表

该元素本身不会显示到页面，通常用于和普通文本框配合

#### form元素

通常，会将整个表单元素，放置form元素的内部，作用是当提交表单时，会将form元素内部的表单内容以合适的方式提交到服务器。

form元素对开发静态页面没有什么意义。

#### fieldset元素

表单分组
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