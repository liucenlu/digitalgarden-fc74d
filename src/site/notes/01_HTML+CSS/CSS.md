---
{"dg-publish":true,"permalink":"/01_HTML+CSS/CSS/","created":"2025-06-22T11:11:06.656+08:00","updated":"2025-06-27T12:52:30.475+08:00"}
---

# CSS基础
## 1.为网页添加样式
### 术语解释

```css
h1{
    color:red;
    background-color:lightblue;
    text-align: center;
}
```

==CSS规则 = 选择器 + 声明块==

#### 选择器

选择器：选中元素

1. ID选择器：选中的是对应id值的元素
2. 元素选择器
3. 类选择器

#### 声明块

出现在大括号中

声明块中包含很多声明（属性），每一个声明（属性）表达了某一方面的样式。

[scroll]

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    /* 元素选择器 */
    h1 {
      color: red;
      background-color: lightblue;
      text-align: center;
    }
    /* 类选择器 */
    .red {
      color: red;
    }
    .big-center {
      font-size: 3em;
      text-align: center;
    }
    /* id选择器 */
    #test {
      color: blue;
    }
  </style>
</head>
<body>
  <h1 class="red">为网页添加样式</h1>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Vitae, excepturi.</p>
  <p id="test">Lorem ipsum dolor sit amet consectetur, adipisicing elit. Quisquam, illo?</p>
  <p class="red big-center">Velit necessitatibus id minima vel laborum. Voluptatem esse maxime ducimus?</p>
  <p class="red">Atque esse nostrum enim iste numquam earum nisi aliquam quod!</p>
</body>
</html>
```

### CSS代码书写位置

1. 内部样式表
	+ 书写在style元素中,style元素在head元素中，避免浏览器先渲染出没有样式的html
	+ 如上例子
2. 内联样式表，元素样式表
	+ 直接书写在元素的style属性中
		```html
		<h1 style="color:red;">为网页添加样式</h1>
		```
3. 外部样式表[推荐]
	将样式书写到独立的css文件中,然后在head>link中导入
	```html
	<link rel="stylesheet" href="css/style.css">
	```
	
	1). 外部样式可以解决多页面样式重复的问题
	2). 有利于浏览器缓存，从而提高页面响应速度
	3). 有利于代码分离（HTML和CSS），更容易阅读和维护

## 2.常见样式声明

1. ==color==
	:元素内部的文字颜色
	**预设值**：定义好的单词
	**三原色，色值**：光学三原色（红、绿、蓝），每个颜色可以使用0-255之间的数字来表达，色值。

	```
	rgb表示法：rgb(红色值,绿色值,蓝色值)
	rgb(0, 255, 0)
	
	hex（16进制）表示法：
	#红(2位)绿(2位)蓝(2位)
	淘宝红：#ff4400, #f40
	黑色：#000000，#000
	白色：#ffffff, #fff
	红：#ff0000, #f00
	绿：#00ff00, #0f0
	蓝：#0000ff, #00f
	紫：#f0f
	青：#0ff
	黄：#ff0
	灰色：#ccc
	```

2. ==background-color==
	元素背景颜色
3. ==font-size==
	元素内部文字的尺寸大小

	1）px：像素，绝对单位，简单的理解为文字的高度占多少个像素
	2）em：相对单位，相对于父元素的字体大小
		==2em：父元素字体大小的2倍==
	每个元素必须有字体大小，如果没有声明，则直接使用父元素的字体大小，如果没有父元素（html），则使用基准字号（浏览器设置的）。
> 	user agent，UA，用户代理（浏览器）
> 	![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626.png)

4. ==font-weight==	
	文字粗细程度，可以取值数字，可以取值为预设值（normal（相当于数值400）、bold（数值700））
> 	strong，默认加粗

5. ==font-family==
	文字类型
	必须用户计算机中存在的字体才会有效。
	使用多个字体，以匹配不同环境
	sans-serif，非衬线字体
	微软雅黑、楷体、Comic Sans MS
6. ==font-style==
	字体样式，通常用它设置**斜体**
	```css
	font-style: italic;
	```

> 	i元素，em元素，默认样式，是倾斜字体; 实际使用中，通常用它表示一个图标（icon）
> 	![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-1.png)

7. ==text-decoration==
	文本修饰，给文本加线。

> 	a元素
> 	del元素：错误的内容
> 	s元素：过期的内容

```html
  <div>成语：<del>章</del>张口就来</div>
  <p>活动价格：9.9&nbsp 原价：<s>12.9</s></p>
```
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-2.png)
8. ==text-indent==
	首行文本缩进

9.  ==line-height==

	每行文本的高度，该值越大，每行文本的距离越大。
	设置行高为容器的高度，可以让单行文本垂直居中
	行高可以设置为纯数字，表示相对于当前元素的字体大小

	```html
	  <div style="background-color: #008c8c;color:#fff;height: 50px;line-height:50px">Lorem ipsum dolor sit amet.</div>
	
	  <p style="text-indent: 2em;line-height: 1.5;">Lorem ipsum dolor sit amet consectetur adipisicing elit. Similique ipsum voluptatem rem dolor officiis, aut placeat exercitationem? Dolorem tempore rem fugit accusamus eveniet ratione, nam, fuga, quos in deserunt voluptate.</p>
	```
	![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-3.png)
10.  ==width==
	宽度

11.  ==height==
	高度

12.  ==letter-space==
	文字间隙

13. ==text-align==
	left/center/right
	元素内部文字的水平排列方式
	
## 3.选择器

选择器：帮助精准的选中想要的元素

### 简单选择器

1. ID选择器
2. 元素选择器
3. 类选择器
4. 通配符选择器
	\*，选中所有元素
5. 属性选择器
	根据属性名和属性值选中元素
	```css
	[href="https://www.xina.com"] {
	  color:red;
	}
	```
6. 伪类选择器
	选中某些元素的某种状态
	1）link: 超链接未访问时的状态
	2）visited: 超链接访问过后的状态
	3）hover: 鼠标悬停状态
	4）active：激活状态，鼠标按下状态
	如果4个规则都写，按以上顺序，否则可能失效
	爱恨法则：love hate
	```css
	/* 选中鼠标悬停的a元素 */
	a :hover{
	  color: brown;
	}
	```
7. 伪元素选择器
	通常用于生成或选中某元素内部的第一个子元素或最后一个子元素
	+ before
	+ after
```css
/* <div><span>HTML&CSS</span></div> */
span::before {
	content:"《";
}
span::after {
	content:"》";
	color:red
}
```
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-4.png)
### 选择器的组合

1. 并且`p.red{}`
2. 后代元素 —— 空格`.red li{}`
3. 子元素 —— >`.red>li{}`(只能选中子元素，区别于后代)
4. 相邻兄弟元素 —— +
5. 后面出现的所有兄弟元素 —— ~

### 选择器的并列

多个选择器, 用逗号分隔

>这是一个语法糖

## 4.层叠

>声明冲突：同一个样式，多次应用到同一个元素

==层叠==：解决声明冲突的过程，浏览器自动处理（也叫权重计算）

![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-5.png)
### 1. 比较重要性

重要性从高到底：

> 作者样式表：开发者书写的样式

  1）作者样式表中的!important样式（慎加）
2)  作者样式表中的普通样式
3)  浏览器默认样式表中的样式

### 2. 比较特殊性
看选择器
总体规则：选择器选中的范围越窄，越特殊越重要
权重计算具体规则：通过选择器，计算出一个4位数（x x x x）

1. 千位：如果是内联样式，记1，否则记0
2. 百位：等于选择器中所有id选择器的数量
3. 十位：等于选择器中所有类选择器、属性选择器、伪类选择器的数量
4. 个位：等于选择器中所有元素选择器、伪元素选择器的数量
[1. CSS选择器及其优先级](../前端八股/CSS/前端面试%20CSS篇_w3cschool.md#1.%20CSS选择器及其优先级)
### 3. 比较源次序
代码书写靠后的胜出

### 应用

1. 重置样式表
	+ 书写一些作者样式，覆盖浏览器的默认样式
	+ 重置样式表 -> 浏览器的默认样式
	+ 常见的重置样式表：normalize.css、reset.css、meyer.css
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-6.png)
2. 爱恨法则
	+ link > visited > hover > active
	+ 层叠到源次序，源次序靠后的重要

## 5.继承
子元素会继承父元素的某些CSS属性
通常，跟文字内容相关的属性都能被继承
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-7.png)
## 6.属性值的计算过程
一个元素一个元素依次渲染，顺序按照页面文档的树形目录结构进行

![attachments/Paste-image-20250622.png](/img/user/01_HTML+CSS/attachments/Paste-image-20250622.png)

渲染每个元素的前提条件：该元素的所有CSS属性必须有值
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-8.png)
一个元素，从所有属性都没有值，到所有的属性都有值，这个计算过程，叫做属性值计算过程
[属性值计算过程简介](属性值计算过程简介.pdf)
1. 确定声明值
2. 层叠冲突
3. 使用继承
4. 使用默认值
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-9.png)
![](/img/user/01_HTML+CSS/attachments/attachments/20250626190025.png)
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-11.png)
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-12.png)
`color:inherit;`

特殊的两个CSS取值：

- inherit：手动（强制）继承，将父元素的值取出应用到该元素
    `color:inherit;`
- initial：初始值，将该属性设置为默认值
## 7.盒模型

box：盒子，每个元素在页面中都会生成一个矩形区域（盒子）

盒子类型：

1. 行盒，display等于inline的元素
2. 块盒，display等于block的元素

行盒在页面中不换行、块盒独占一行

display默认值为inline

浏览器默认样式表设置的块盒：容器元素、h1~h6、p

常见的行盒：span、a、img、video、audio

### 盒子的组成部分

无论是行盒、还是块盒，都由下面几个部分组成，从内到外分别是：
![](/img/user/01_HTML+CSS/attachments/attachments/Pasted image 20250626195811.png)
1. 内容  content
	width、height，设置的是盒子内容的宽高
	*内容部分通常叫做整个盒子的**内容盒 content-box***
	
2. 填充(内边距)  padding
	*盒子边框到盒子内容的距离*
	padding-left、padding-right、padding-top、padding-bottom
	padding: 简写属性
	padding: 上 右 下 左
	
	*填充区+内容区 = **填充盒 padding-box***
	
3. 边框  border
	边框 = 边框宽度 + 边框样式 + 边框颜色

	边框样式：border-style
	边框宽度：border-width
	边框颜色：border-color
	
	*边框+填充区+内容区 = **边框盒 border-box***
	
4. 外边距  margin

	边框到其他盒子的距离
	
	margin-top、margin-left、margin-right、margin-bottom
	
	速写属性margin
## 8.盒模型应用
### 改变宽高范围

默认情况下，width 和 height 设置的是内容盒宽高。

> 页面重构师：将psd文件（设计稿）制作为静态页面

衡量设计稿尺寸的时候，往往使用的是边框盒，但设置width和height，则设置的是内容盒

1. 精确计算
2. CSS3：==box-sizing==（border-box、content-box）

### 改变背景覆盖范围

默认情况下，背景覆盖边框盒

可以通过==background-clip==（border-box、content-box）进行修改

### 溢出处理

==overflow==(auto|hidden|scroll|……)，控制内容溢出边框盒后的处理方式
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-14.png)
### 断词规则

==word-break==，会影响文字在什么位置被截断换行

- normal：普通。CJK字符（文字位置截断），非CJK字符（单词位置截断）
- break-all：截断所有。所有字符都在文字处截断
- keep-all：保持所有。所有文字都在单词之间截断

### 空白处理

white-space: nowrap，遇到空白不换行，可能导致溢出
white-space: pre，遇到空格不折叠
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-15.png)

```css
    li {
      border-bottom: 1px dashed #ccc;
      line-height:2;
      border-left:3px solid #008c8c;
      margin:1em 0;
      width: 200px;
      padding-left:10px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow:ellipsis;
      /* 文本溢出显示圆点 */
    }
```
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250626-16.png)
## 9.行盒的盒模型
常见的行盒：包含具体内容的元素

span、strong、em、i、img、video、audio

### 显著特点

1. 盒子沿着内容沿伸
2. 行盒不能设置宽高
	调整行盒的宽高，应该使用字体大小、行高、字体类型，间接调整。

3. 内边距（填充区）
	水平方向有效，垂直方向(可以看到效果)不会实际占据空间。
	![](/img/user/01_HTML+CSS/attachments/Paste-image-20250627.png)
4. 边框
	水平方向有效，垂直方向(可以看到效果)不会实际占据空间。

5. 外边距
	水平方向有效，垂直方向不会实际占据空间，完全无效。
	![](/img/user/01_HTML+CSS/attachments/Paste-image-20250627-1.png)

> [!info]
> 虽然设置 `line-height` 是在块级元素（如 `<p>`、`<div>`）上常见，但实际是影响其**内部行盒**的排列方式。也就是说，块盒只是**传播或继承**了 `line-height` 的值，具体效果还是体现在行盒上。

### 行块盒
>对应以前的行内块级元素

display：inline-block 的盒子
既有块盒的特点又有行盒的特点：
1. 不独占一行
2. 盒模型中所有尺寸都有效

```css
    a {
      background-color: red;
      color: #fff;
      display: inline-block;
      width: 100px;
      text-align: center;
      margin:50px;
    }
```
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250627-2.png)
删掉`display: inline-block;`:a元素变为行盒
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250627-3.png)

### 行快盒实现分页标签
[scroll]

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    body {
      background-color: #ccc;
    }
    a {
      background-color: #fff;
      color: #3951b3;
      text-decoration: none;
      display: inline-block;
      width:36px;
      height: 36px;
      text-align: center;
      line-height: 36px;
      border-radius: 4px;
      margin:0 2px;
    }
    div a:hover{
      color:#fff;
      background-color: #4e6ef2;
    }
    div a.selected{
      color:#fff;
      background-color: #4e6ef2;
    }
  </style>
</head>
<body>
  <div>
    <a href="">1</a>
    <a href="">2</a>
    <a href="" class="selected">3</a>
    <a href="">4</a>
    <a href="">5</a>
    <a href="">6</a>
    <a href="">7</a>
    <a href="">8</a>
    <a href="">9</a>
    <a href="">10</a>
  </div>
</body>
</html>
```

![](/img/user/01_HTML+CSS/attachments/Paste-image-20250627-4.png)
#### 空白折叠

空白折叠，发生在行盒（行块盒）内部 或 行盒（行块盒）之间
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250627-5.png)
这些源码中的空白会被折叠为一个空格
### 可替换元素 和 非可替换元素

+ 大部分元素，页面上显示的结果，取决于==元素内容==，称为**非可替换元素**

+ 少部分元素，页面上显示的结果，取决于==元素属性==，称为**可替换元素**

可替换元素：img、video、audio、input、button等

绝大部分可替换元素==均为行盒，但类似于行块盒，盒模型中所有尺寸都有效。==
比如一个img元素，display属性默认值为inline，行盒元素，但是可以设置width、height

object-fit：contain|fill|cover
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250627-6.png)
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250627-7.png)
![](/img/user/01_HTML+CSS/attachments/Paste-image-20250627-8.png)
## 10.常规流

- 盒模型：规定单个盒子的规则

- 视觉格式化模型（布局规则）：页面中的多个盒子排列规则
	- 视觉格式化模型，大体上将页面中盒子的排列分为三种方式：
	1. 常规流
	2. 浮动
	3. 定位

### 常规流布局

常规流、文档流、普通文档流、常规文档流

所有元素，默认情况下，都属于常规流布局

总体规则：块盒独占一行，行盒水平依次排列

包含块（containing block）：每个盒子都有它的包含块，包含块决定了盒子的排列区域。

绝大部分情况下：盒子的包含块，为其父元素的内容盒

**块盒**

1. 每个块盒的总宽度，必须刚好等于包含块的宽度

宽度的默认值是auto

margin的取值也可以是auto，默认值0

auto：将剩余空间吸收掉

width吸收能力强于margin

若宽度、边框、内边距、外边距计算后，仍然有剩余空间，该剩余空间被margin-right全部吸收

在常规流中，块盒在其包含快中居中，可以定宽、然后左右margin设置为auto。

2. 每个块盒垂直方向上的auto值

height:auto， 适应内容的高度

margin:auto， 表示0

3. 百分比取值

padding、宽、margin可以取值为百分比

以上的所有百分比相对于包含块的宽度。

高度的百分比：

1）. 包含块的高度是否取决于子元素的高度，设置百分比无效
2）. 包含块的高度不取决于子元素的高度，百分比相对于父元素高度

4. 上下外边距的合并

两个常规流块盒，上下外边距相邻，会进行合并。

两个外边距取最大值。
## 11.常规流练习

## 12.浮动
视觉格式化模型，大体上将页面中盒子的排列分为三种方式：

1. 常规流
2. 浮动
3. 定位

### 应用场景

1. 文字环绕
2. 横向排列

### 浮动的基本特点

修改float属性值为：

- left：左浮动，元素靠上靠左
- right：右浮动，元素靠上靠右

默认值为none

1. 当一个元素浮动后，元素必定为块盒(更改display属性为block)
2. 浮动元素的包含块，和常规流一样，为父元素的内容盒

### 盒子尺寸

1. 宽度为auto时，适应内容宽度
2. 高度为auto时，与常规流一致，适应内容的高度
3. margin为auto，为0.
4. 边框、内边距、百分比设置与常规流一样

### 盒子排列

1. 左浮动的盒子靠上靠左排列
2. 右浮动的盒子考上靠右排列
3. 浮动盒子在包含块中排列时，会避开常规流块盒
4. 常规流块盒在排列时，无视浮动盒子
5. 行盒在排列时，会避开浮动盒子
6. 外边距合并不会发生

> 如果文字没有在行盒中，浏览器会自动生成一个行盒包裹文字，该行盒叫做匿名行盒。

### 高度坍塌

高度坍塌的根源：常规流盒子的自动高度，在计算时，不会考虑浮动盒子

清除浮动，涉及css属性：clear

- 默认值：none
- left：清除左浮动，该元素必须出现在前面所有左浮动盒子的下方
- right：清除右浮动，该元素必须出现在前面所有右浮动盒子的下方
- both：清除左右浮动，该元素必须出现在前面所有浮动盒子的下方
## 13.浮动练习
## 14.定位
视觉格式化模型，大体上将页面中盒子的排列分为三种方式：

1. 常规流
2. 浮动：float
3. 定位：position

定位：手动控制元素在包含块中的精准位置

涉及的CSS属性：position

### position属性

- 默认值：static，静态定位（不定位）
- relative：相对定位
- absolute：绝对定位
- fixed：固定定位

一个元素，只要position的取值不是static，认为该元素是一个定位元素。

定位元素会脱离文档流（相对定位除外）

一个脱离了文档流的元素：

1. 文档流中的元素摆放时，会忽略脱离了文档流的元素
2. 文档流中元素计算自动高度时，会忽略脱离了文档流的元素

### 相对定位

不会导致元素脱离文档流，只是让元素在原来位置上进行偏移。

可以通过四个CSS属性对设置其位置：

- left
- right
- top
- bottom

盒子的偏移不会对其他盒子造成任何影响。

### 绝对定位

1. 宽高为auto，适应内容
2. 包含块变化：找祖先中第一个定位元素，该元素的填充盒为其包含块。若找不到，则它的包含块为整个网页（初始化包含块）

### 固定定位

其他情况和绝对定位完全一样。

包含块不同：固定为视口（浏览器的可视窗口）


### 定位下的居中

某个方向居中：

1. 定宽（高）
2. 将左右（上下）距离设置为0
3. 将左右（上下）margin设置为auto

绝对定位和固定定位中，margin为auto时，会自动吸收剩余空间

### 多个定位元素重叠时

堆叠上下文

设置z-index，通常情况下，该值越大，越靠近用户

只有定位元素设置z-index有效

z-index可以是负数，如果是负数，则遇到常规流、浮动元素，则会被其覆盖

### 补充

- 绝对定位、固定定位元素一定是块盒
- 绝对定位、固定定位元素一定不是浮动
- 没有外边距合并
## 15.定位练习
## 16.更多的选择器
### 更多伪类选择器

1. first-child

选择第一个子元素

first-of-type，选中子元素中第一个指定类型的元素

2. last-child


3. nth-child

选中指定的第几个子元素

even：关键字，等同于2n
odd: 关键字，等同于2n+1

4. nth-of-type

选中指定的子元素中第几个某类型的元素

### 更多的伪元素选择器

1. first-letter

选中元素中的第一个字母

2. first-line

选中元素中第一行的文字

3. selection

选中被用户框选的文字
## 17.更多的样式
### 透明度

1. opacity，它设置的是整个元素的透明，它的取值是0 ~ 1
2. 在颜色位置设置alpha通道(rgba )

### 鼠标

使用cursor设置

### 盒子隐藏

1. display:none，不生成盒子
2. visibility:hidden，生成盒子，只是从视觉上移除盒子，盒子仍然占据空间。

### 背景图

#### 和img元素的区别

img元素是属于HTML的概念

背景图属于css的概念

1. 当图片属于网页内容时，必须使用img元素
2. 当图片仅用于美化页面时，必须使用背景图

#### 涉及的css属性

1. background-image

2. background-repeat

默认情况下，背景图会在横坐标和纵坐标中进行重复

3. background-size

预设值：contain、cover，类似于object-fit
数值或百分比

4. background-position

设置背景图的位置。

预设值：left、bottom、right、top、center

数值或百分比

雪碧图（精灵图）（spirit）

5. background-attachment

通常用它控制背景图是否固定。

6. 背景图和背景颜色混用

7. 速写（简写）background
## 18.背景图练习
# CSS进阶
## 1.@规则
at-rule: @规则、@语句、CSS语句、CSS指令

1. import
    

@import "路径";

导入另外一个css文件

2. charset
    

@charset "utf-8";

告诉浏览器该CSS文件，使用的字符编码集是utf-8，必须写到第一行
## 2.web字体和图标
### web字体

用户电脑上没有安装相应字体，强制让用户下载该字体

使用@font-face指令制作一个新字体

### 字体图标

iconfont.cn
## 3.块级格式化上下文
## 4.布局
### 多栏布局

两栏布局

三栏布局

### 等高

1. CSS3的弹性盒
2. JS控制
3. 伪等高

### 元素书写顺序

### 后台页面的布局
## 5.\[扩展]浮动的细节规则
## 6.\[扩展]行高的取值
line-height

1. px, 像素值
    
2. 无单位的数字
    
3. em单位
    
4. 百分比
## 7.\[扩展]body背景
**画布 canvas**

一块区域

特点：

1. 最小宽度为视口宽度
2. 最小高度为视口高度

**HTML元素的背景**

覆盖画布

**BODY元素的背景**

如果HTML元素有背景，BODY元素正常（背景覆盖边框盒）

如果HTML元素没有背景，BODY元素的背景覆盖画布

**关于画布背景图**

1. 背景图的宽度百分比，相对于视口
2. 背景图的高度百分比，相对于网页高度
3. 背景图的横向位置百分比、预设值，相对于视口
4. 背景图的纵向位置百分比、预设值，相对于网页高度
## 8.行盒的垂直对齐
### 多个行盒垂直方向上的对齐

给没有对齐元素设置vertical-align

预设值

数值

### 图片的底部白边

图片的父元素是一个块盒，块盒高度自动，图片底部和父元素底边之间往往会出现空白。

1. 设置父元素的字体大小为0
2. 将图片设置为块盒

## 9.\[扩展]参考线-深入理解字体
font-size、line-height、vertical-align、font-family

### 文字

文字是通过一些文字制作软件制作的，比如fontforge

制作文字时，会有几根参考线，不同的文字类型，参考线不一样。同一种文字类型，参考线一致。

### font-size

字体大小，设置的是文字的相对大小

文字的相对大小：1000、2048、1024

文字顶线到底线的距离，是文字的实际大小（content-area，内容区）

行盒的背景，覆盖content-area

### 行高

顶线向上延申的空间，和底线向下延申的空间，两个空间相等，该空间叫做gap（空隙）

gap默认情况下，是字体设计者决定

top到botoom（看ppt图），叫做virtual-area（虚拟区）

行高，就是virtual-area

line-height:normal，默认值，使用文字默认的gap

> 文字一定出现一行的最中间——错误
> content-area一定出现在virtual-area的中间

### vertical-align

决定参考线：font-size、font-family、line-height

一个元素如果子元素出现行盒，该元素内部也会产生参考线

baseline：该元素的基线与父元素的基线对齐

super: 该元素的基线与父元素的上基线对齐

sub：该元素的基线与父元素的下基线对齐

text-top: 该元素的virtual-area的顶边，对齐父元素的text-top

text-bottom: 该元素的virtual-area的底边，对齐父元素的text-bottom

top：该元素的virtual-area的定边，对齐line-box的顶边

bottom：该元素的virtual-area的底边，对齐line-box的底边

middle: 该元素的中线（content-area的一半），与父元素的X字母高度一半的位置对齐

行盒组合起来，可以形成多行，每一行的区域叫做line-box，line-box的顶边是该行内所有行盒最高顶边，底边是该行行盒的最低底边。

实际，一个元素的实际占用高度（高度自动），高度的计算通过line-box计算。

行盒：inline-box
行框：line-box

数值：相对于基线的偏移量，向上为正数，向下为负数。

百分比：相对于基线的偏移量，百分比是相对于自身virtual-area的高度

line-box是承载文字内容的必要条件，以下情况不生成行框：

1. 某元素内部没有任何行盒
2. 某元素字体大小为0

### 可替换元素和行块盒的基线

图片：基线位置位于图片的下外边距。

表单元素：基线位置在内容底边

行块盒：

1. 行块盒最后一行有line-box，用最后一行的基线作为整个行块盒的基线。
2. 如果行块盒内部没有行盒，则使用下外边距作为基线
## 10.\[扩展]堆叠上下文
堆叠上下文（stack context），它是一块区域，这块区域由某个元素创建，它规定了该区域中的内容在Z轴上排列的先后顺序。

### 创建堆叠上下文的元素

1. html元素（根元素）
2. 设置了z-index（非auto）数值的定位元素

### 同一个堆叠上下文中元素在Z轴上的排列

从后到前的排列顺序：

1. 创建堆叠上下文的元素的背景和边框
2. 堆叠级别(z-index, stack level)为负值的堆叠上下文
3. 常规流非定位的块盒
4. 非定位的浮动盒子
5. 常规流非定位行盒
6. 任何 z-index 是 auto 的定位子元素，以及 z-index 是 0 的堆叠上下文
7. 堆叠级别为正值的堆叠上下文

每个堆叠上下文，独立于其他堆叠上下文，它们之间不能相互穿插。
## 11.\[扩展]svg
# svg

svg: scalable vector graphics，可缩放的矢量图

1. 该图片使用代码书写而成
2. 缩放不会失真
3. 内容轻量

### 怎么使用

svg可以嵌入浏览器，也可以单独成为一个文件

xml语言，svg使用该语言定义

### 书写svg代码

#### 矩形:rect

#### 圆形：circle

#### 椭圆：ellipse

#### 线条：line

#### 折线：polyline

#### 多边形：polygon

#### 路径：path

M = moveto
L = lineto
H = horizontal lineto
V = vertical lineto
C = curveto
S = smooth curveto
Q = quadratic Belzier curve
T = smooth quadratic Belzier curveto
A = elliptical Arc

A
半径1    
半径2     
顺时针旋转角度    
小弧（0）或大弧（1）   
顺时针（1）逆时针（0）

Z = closepath


#### 例子

画太极图
## 12.\[扩展]数据链接
data url

### 如何书写

数据链接：将目标文件的数据直接书写到路径位置

语法：data:MIME,数据

### 意义

优点：

1. 减少了浏览器中的请求

请求

响应

减少了请求中浪费的时间

2. 有利于动态生成数据

缺点：

1. 增加了资源的体积

导致了传输内容增加，从而增加了单个资源的传输时间

2. 不利于浏览器的缓存

浏览器通常会缓存图片文件、css文件、js文件。

3. 会增加原资源的体积到原来的4/3

应用场景：

1. 但请求单个图片体积较小，并且该图片因为各种原因，不适合制作雪碧图，可以使用数据链接。

2. 图片由其他代码动态生成，并且图片较小，可以使用数据链接。

### base64

一种编码方式

通常用于将一些二进制数据，用一个可书写的字符串表示。
## 13.浏览器兼容性
### 问题产生原因

- 市场竞争
- 标准版本的变化

### 厂商前缀

> 比如：box-sizing， 谷歌旧版本浏览器中使用-webkit-box-sizing:border-box

- 市场竞争，标准没有发布
- 标准仍在讨论中（草案），浏览器厂商希望先支持

IE： -ms-
Chrome，safari:  -webkit-
opera： -o-
firefox: -moz-

> 浏览器在处理样式或元素时，使用如下的方式：
> 当遇到无法识别的代码时，直接略过。


1. 谷歌浏览器的滚动条样式

实际上，在开发中使用自定义的滚动条，往往是使用div+css+JS实现的

2. 多个背景图中选一个作为背景

### css hack

根据不同的浏览器（主要针对IE），设置不同的样式和元素

1. 样式

IE中，CSS的特殊符号

- *属性，兼容IE5、IE6、IE7
- _属性，兼容IE5~IE6
- 属性值\9，兼容IE5~IE11
- 属性值\0，兼容IE8~IE11
- 属性值\9\0，兼容IE9~IE10

> IE5、6、7的外边距bug，浮动元素的左外边距翻倍

2. 条件判断

### 渐近增强 和 优雅降级

两种解决兼容性问题的思路，会影响代码的书写风格

- 渐近增强：先适应大部分浏览器，然后针对新版本浏览器加入新的样式

书写代码时，先尽量避免书写有兼容性问题的代码，完成之后，再逐步加入新标准中的代码。

- 优雅降级：先制作完整的功能，然后针对低版本浏览器进行特殊处理

书写代码时，先不用特别在意兼容性，完成整个功能之后，再针对低版本浏览器处理样式。

### caniuse

查找css兼容性

[caniuse.com](https://caniuse.com/)
## 14.居中总结
居中：盒子在其包含块中居中

### 行盒（行块盒）水平居中

直接设置行盒（行块盒）父元素```text-align:center```

### 常规流块盒水平居中

定宽，设置左右margin为auto

### 绝对定位元素的水平居中

定宽，设置左右的坐标为0（left:0, right:0），将左右margin设置为auto

> 实际上，固定定位（fixed）是绝对定位（absolute）的特殊情况

### 单行文本的垂直居中

设置文本所在元素的行高，为整个区域的高度

### 行块盒或块盒内多行文本的垂直居中

没有完美方案

设置盒子上下内边距相同，达到类似的效果。

### 绝对定位的垂直居中

定高，设置上下的坐标为0（top:0, bottom:0），将上下margin设置为auto
## 15.样式补充
### display:list-item

设置为该属性值的盒子，本质上仍然是一个块盒，但同时该盒子会附带另一个盒子

元素本身生成的盒子叫做主盒子，附带的盒子称为次盒子，次盒子和主盒子水平排列

涉及的css：

1. ```list-style-type```

设置次盒子中内容的类型

2. ```list-style-position```

设置次盒子相对于主盒子的位置

3. 速写属性```list-style```

**清空次盒子**

list-style:none

### 图片失效时的宽高问题

如果img元素的图片链接无效，img元素的特性和普通行盒一样，无法设置宽高

### 行盒中包含行块盒或可替换元素

行盒的高度与它内部的行块盒或可替换元素的高度无关

### text-align:justify

text-align:

- left: 左对齐
- right：右对齐
- center：居中
- justify：除最后一行外，分散对齐

### 制作一个三角形

### direction 和 writing-mode

开始 start -> 结束 end
左 left -> 右 end

开始和结束是相对的，不同国家有不同的习惯

左右是绝对的

direction设置的是开始到结束的方向

writing-mode：设置文字书写方向

### utf-8字符