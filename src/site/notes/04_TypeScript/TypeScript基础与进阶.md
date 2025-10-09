---
{"dg-publish":true,"permalink":"/04_TypeScript/TypeScript基础与进阶/","created":"2025-07-29T19:45:18.750+08:00","updated":"2025-10-09T19:02:00.640+08:00"}
---

# 1.TypeScript概述

## 为什么要学习TypeScript

- 获得更好的开发体验
- 解决JS中一些难以处理问题

## JS开发中的问题

- 使用了不存在的变量、函数或成员
- 把一个不确定的类型当作一个确定的类型处理
- 在使用null或undefined的成员

js的原罪

- js语言本身的特性，决定了该语言无法适应大型的复杂的项目
- 弱类型：某个变量，可以随时更换类型。
	- ![](/img/user/04_TypeScript/attachments/Paste-image-20250730-1.png)
- 解释性：错误发生的时间，是在运行时（而非编译时）

前端开发中，大部分的时间都是在排错

例子：
![](/img/user/04_TypeScript/attachments/Paste-image-20250730.png)
1. 变量名拼写错误、使用不存在的成员
2. getUserName返回值的类型不确定
## TypeScript

简称TS

TypeScript是JS的**超集**，是一个可选的、静态的**类型系统**

- 超集
	理解超集：整数、正整数， 整数是正整数的超集
![](/img/user/04_TypeScript/attachments/Paste-image-20250730-10.png)

- 类型系统
	对代码中所有的标识符（变量、函数、参数、返回值）进行类型检查

- 可选的
	类型检查可用可不用
	学习曲线非常平滑。

- 静态的(在运行之前)

无论是浏览器环境，还是node环境，无法直接识别ts代码

> babel: es6 -> es5

> tsc: ts -> es

tsc: ts编译器

静态：类型检查发生的时间，在编译的时候，而非运行时

TS不参与任何运行时的类型检查。

**TS的常识**

- 2012年微软发布 （ES6，ES2015）
- Anders Hejlsberg 负责开发TS项目
- 开源、拥抱ES标准
- 版本3.4
- 官网：[TypeScript: Documentation - 为 JavaScript 程序员准备的 TypeScript](https://www.typescriptlang.org/zh/docs/handbook/typescript-in-5-minutes.html)

> 中文网：https://www.tslang.cn/  个人翻译
> [基础类型 · TypeScript中文网 · TypeScript——JavaScript的超集](http://tslang.cn/docs/handbook/basic-types.html)


**额外的惊喜**

有了类型检查，增强了面向对象的开发

js中也有类和对象，js支持面向对象开发。没有类型检查，很多面向对象的场景实现起来有诸多问题。

使用TS后，可以编写出完善的面向对象代码。

# 2.在node中搭建TS开发环境

## 安装TypeScript

默认情况下，TS会做出下面几种假设：

1. 假设当前的执行环境是dom
2. 如果代码中没有使用模块化语句（import、export），便认为该代码是全局执行
3. 编译的目标代码是ES3

有两种方式更改以上假设：

1. 使用tsc命令行的时候，加上选项参数
2. 使用ts配置文件，更改编译选项
	1. 直接新建文件tsconfig.json
	2. 命令行输入`tsc --init`，自动生成配置文件

## TS的配置文件

使用了配置文件后，使用tsc进行编译时，不能跟上文件名，如果跟上文件名，会忽略配置文件。

@types/node，对node的js代码的类型描述
安装命令：`npm i -D @types/node`

@types是一个ts官方的类型库，其中包含了很多对js代码的类型描述。

> JQuery：用js写的，没有类型检查
> 安装@types/jquery，为jquery库添加类型定义
![](/img/user/04_TypeScript/attachments/Paste-image-20250730-2.png)
## 使用第三方库简化流程

ts-node: 将ts代码在内存中完成编译，同时完成运行
- 安装：`npm i -g ts-node`
- 使用：`ts-node src/index.ts`
- 在开发阶段非常好用
- 但不能检测代码发生变化，需要手动运行

nodemon: 用于检测文件的变化
- 安装：`npm i -g nodemon`
- 使用：`nodemon --exec ts-node src/index.ts`，在检测到代码变化时执行XX命令
- 将命令写到脚本里：
	![](/img/user/04_TypeScript/attachments/Paste-image-20250730-3.png)
	启动：`npm run dev`
	![](/img/user/04_TypeScript/attachments/Paste-image-20250730-4.png)
- `nodemon -e ts --exec ts-node src/index.ts`：只监测ts文件
- `nodemon --watch src -e ts --exec ts-node src/index.ts`：只监测src文件夹中的ts文件
- 开发完成后，`tsc`命令输出编译后的文件
# 3.基本类型约束
[基础类型 · TypeScript中文网 · TypeScript——JavaScript的超集](http://tslang.cn/docs/handbook/basic-types.html)
> TS是一个可选的静态的类型系统

## 如何进行类型约束

仅需要在 变量、函数的参数、函数的返回值位置加上==```:类型```==
![](/img/user/04_TypeScript/attachments/Paste-image-20250730-5.png)
```ts
function sum(a: number, b: number, c: number):number {
    return a + b + (c || 0);
}

//sum(3, 4);

sum(3, 4, 5);
```

ts在很多场景中可以完成类型推导，上面的代码中只需要对函数的参数进行类型定义，返回值会自动推导。

any: 表示任意类型，对该类型，ts不进行类型检查，需要手动进行类型约束
![](/img/user/04_TypeScript/attachments/Paste-image-20250730-6.png)
> 小技巧，如何区分数字字符串和数字，关键看怎么读？
> 如果按照数字的方式朗读，则为数字；否则，为字符串。

## 源代码和编译结果的差异

编译结果中没有类型约束信息
![](/img/user/04_TypeScript/attachments/Paste-image-20250730-7.png)
## 基本类型

>注意是小写不是大写
- number：数字
- string：字符串
- boolean：布尔
- 数组
	- number[ ]：number类型的数组
	- Array\<number>：同上，实际是语法糖
- object: 对象
- null 和 undefined

null和undefined是所有其他类型的子类型，它们可以赋值给其他类型

通过在配置文件添加```strictNullChecks:true```，可以获得更严格的空类型检查，null和undefined只能赋值给自身。

## 其他常用类型

- 联合类型：多种类型任选其一
	
	配合类型保护进行判断
	
	类型保护：当对某个变量进行类型判断之后，在判断的语句块中便可以确定它的确切类型，typeof可以触发类型保护。
```ts
let name: string | undefined;
if(typeof name === 'string'){
	//类型保护
}
```
- void类型：通常用于约束函数的返回值，表示该函数没有任何返回
  
- never类型：通常用于约束函数的返回值，表示该函数永远不可能结束
```ts
function throwError(msg: string): never {
    throw new Error(msg);
}

function alwaysDoSomething(): never {
    while (true) {
        //...
    }
}
```
- 字面量类型：使用一个值进行约束
```ts
let a:'A';

let gender: "男" | "女";

gender = "女";

gender = "男";

let arr: []; //arr永远只能取值为一个空数组

let user: {
    name:string
    age:number
}//约束user为一个对象且必须是一个string类型的name属性和一个number类型的age属性

user = {
    name:"34",
    age:33
}
```
- 元祖类型（Tuple）: 一个固定长度的数组，并且数组中每一项的类型确定
```ts
let tu: [string, number];
tu = ["3", 4];
```
- any类型: any类型可以绕过类型检查，因此，any类型的数据可以赋值给任意类型
```ts
let data:any = "sfdsdf";

let num:number = data;
```
## 类型别名

对已知的一些类型定义名称

```
type 类型名 = ...
```

```ts
type Gender = "男" | "女"
type User = {
    name:string
    age:number
    gender:Gender
}
let u:User
u = {
    name:"sdfd",
    gender:"男",
    age:34
}

function getUsers(g:Gender):User[] {
    return [];
}
```
## 函数的相关约束

函数重载：在函数实现之前，对函数调用的多种情况进行声明
```ts
/**
 * 得到a*b的结果
 * @param a 
 * @param b 
 */
function combine(a:number, b:number):number;
/**
 * 得到a和b拼接的结果
 * @param a 
 * @param b 
 */
function combine(a:string, b:string):string;
function combine(a: number | string, b: number | string): number | string {
    if (typeof a === "number" && typeof b === "number") {
        return a * b;
    }
    else if (typeof a === "string" && typeof b === "string") {
        return a + b;
    }
    throw new Error("a和b必须是相同的类型");
}

const result = combine("a","b")
```
可选参数：可以在某些参数名后加上问号，表示该参数可以不用传递。可选参数必须在参数列表的末尾。
```ts
function sum(a: number, b: number, c?: number):number {
    return a + b + (c || 0);
}

sum(3, 4);

sum(3, 4, 5);
```
# 4.扩展类型-枚举

> 扩展类型：类型别名、枚举、接口、类

枚举通常用于约束某个变量的取值范围。

字面量和联合类型配合使用，也可以达到同样的目标。

## 字面量类型的问题

- 在类型约束位置，会产生重复代码。可以使用类型别名解决该问题。
- 逻辑含义和真实的值产生了混淆，会导致当修改真实值的时候，产生大量的修改。
- 字面量类型不会进入到编译结果。

## 枚举

如何定义一个枚举：

```
enum 枚举名{
    枚举字段1 = 值1,
    枚举字段2 = 值2,
    ...
}
```
使用：
```ts
enum Gender{
	male='男',
	female='女'
}
let gender:Gender = Gender.female;

console.log(gender);  //女
```
枚举会出现在编译结果中，编译结果中表现为对象。
![](/img/user/04_TypeScript/attachments/Paste-image-20250730-8.png)

枚举的规则：

- 枚举的字段值可以是字符串或数字
- 数字枚举的值会自动自增
- 被数字枚举约束的变量，可以直接赋值为数字
- 数字枚举的编译结果 和 字符串枚举有差异
![](/img/user/04_TypeScript/attachments/Paste-image-20250730-9.png)

最佳实践：
- 尽量不要在一个枚举中既出现字符串字段，又出现数字字段
- 使用枚举时，尽量使用枚举字段的名称，而不使用真实的值

# 5.模块化

相关配置：

|       配置名称       |        含义        |
| :--------------: | :--------------: |
|      module      | 设置编译结果中使用的模块化标准  |
| moduleResolution |    设置解析模块的模式     |
|  removeComments  |     编译结果移除注释     |
|  noEmitOnError   |    错误时不生成编译结果    |
| esModuleInterop  | 启用es模块化交互非es模块导出 |


> 前端领域中的模块化标准：ES6、commonjs、amd、umd、system、esnext

> TS中如何书写模块化语句
> 编译结果??

## TS中如何书写模块化语句

TS中，导入和导出模块，统一使用ES6的模块化标准

1. 命名导出
	命名导出允许从一个模块中导出多个值，每个导出项都有自己的名称，导入时必须使用对应的名称接收，且需要`{}`包裹。
	![](/img/user/04_TypeScript/attachments/Paste-image-20250731.png)
2. 默认导出
	一个模块只能有一个默认导出，导出时无需指定名称，导入时可以自定义名称，不需要`{}`包裹。
	![](/img/user/04_TypeScript/attachments/Paste-image-20250731-1.png)
## 编译结果中的模块化

可配置：
```ts
"module": "commonjs", //配置编译目标使用的模块化标准
```

TS中的模块化在编译结果中：

- 如果编译结果的模块化标准是ES6： 没有区别
- 如果编译结果的模块化标准是commonjs：导出的声明会变成exports的属性，默认的导出会变成exports的default属性；
![](/img/user/04_TypeScript/attachments/Paste-image-20250731-2.png)
## 如何在TS中书写commonjs模块化代码
(不推荐在TS中使用commonjs标准)

导出：export = xxx

导入：import xxx = require("xxx")

## 模块解析

模块解析：应该从什么位置寻找模块

TS中，有两种模块解析策略
- classic（过时）：经典
- node（更常用）：就是node解析策略（唯一的变化，是将js替换为ts）
  - 相对路径```require("./xxx")```
  - 非相对模块```require("xxx")```，在node_modules文件夹寻找模块

> [!NOTE]
> 小技巧
> ```json
>     "scripts": {
>         "dev": "nodemon --watch src -e ts --exec ts-node src/index.ts",
>         "build": "rd /s /q dist & tsc"
>     },  
> ```
> build命令在编译时先删除历史dist文件夹再生成最新编译文件到dist中

# 6.接口和类型兼容性

## 扩展类型-接口

接口：inteface

> 扩展类型：类型别名、枚举、接口、类

TypeScript的接口：用于约束类、对象、函数的契约（标准）

契约（标准）的形式：

- API文档，弱标准
    
- 代码约束，强标准
    
>不约束类的时候，接口类型和类型别名区别不大

和类型别名一样，接口定义，不出现在编译结果中

1. 接口约束对象
	```ts
interface User {
	name: string
	age: number
	sayHello(): void
	//sayHello: () => void
}

let u: User = {
	name: "sdfds",
	age: 33,
	sayHello() {
		console.log("asfadasfaf");
	}
}
	```
2. 接口约束函数
	```ts
interface Condition {
	(n: number): boolean
}

function sum(numbers: number[], callBack: Condition) {
	let s = 0;
	numbers.forEach(n => {
		if (callBack(n)) {
			s += n;
		}
	})
	return s;
}

const result = sum([3, 4, 5, 7, 11], n => n % 2 !== 0);
console.log(result);
	```
    

**接口可以继承**

可以通过接口之间的继承，实现多种接口的组合
```ts
interface A {
    T1: string
}

interface B {
    T2: number
}

interface C extends A, B {
    T3: boolean
}
```
使用类型别名可以实现类似的组合效果，需要通过`&`，它叫做交叉类型
```ts
type A = {
    T1: string
}

type B = {
    T2: number
}

type C = {
    T1: number//会导致T1的类型变成number&string的奇怪状态
    T3: boolean
} & A & B
```
它们的区别：

- 子接口不能覆盖父接口的成员
    
- 交叉类型会把相同成员的类型进行交叉
    

**readonly**关键字

只读修饰符，修饰的目标是只读

只读修饰符不在编译结果中
```ts
type User = {
    readonly id: string
    name: string
    age: number,
    readonly arr: readonly string[]
}

let u: User = {
    id: "123",
    name: "Asdf",
    age: 33,
    arr:["Sdf", "dfgdfg"]
}

const arr1: readonly number[] = [3, 4, 6];

const arr2: ReadonlyArray<number> = [3, 4, 6];
```
## 类型兼容性

B->A，如果能完成赋值，则B和A类型兼容

>鸭子辨型法（子结构辨型法）：目标类型需要某一些特征，赋值的类型只要能满足该特征即可

- 基本类型：完全匹配
    
- 对象类型：鸭子辨型法
    

> [!NOTE]
> 类型断言
> ```ts
> sound: "嘎嘎嘎" as "嘎嘎嘎",
> ```
> 如果没做类型断言类型推断会认为sound是string类型，但开发者希望sound就是"嘎嘎嘎"字面量类型。

```ts
interface Duck {
    sound: "嘎嘎嘎"
    swin(): void
}

let person = {
    name: "伪装成鸭子的人",
    age: 11,
    sound: "嘎嘎嘎" as "嘎嘎嘎",
    swin() {
        console.log(this.name + "正在游泳，并发出了" + this.sound + "的声音");
    }
}
let duck: Duck = person;//，类型兼容，可以成功赋值
```

*当直接使用对象字面量赋值的时候，会进行更加严格的判断*

- 函数类型
	一切无比自然
	
	**参数**：传递给目标函数的参数可以少，但不可以多
	
	**返回值**：要求返回必须返回；不要求返回，你随意；

# 7.TS中的类

> 面向对象思想

基础部分，学习类的时候，仅讨论新增的语法部分。

**属性**
不能动态增加属性
使用属性列表来描述类中的属性
![](/img/user/04_TypeScript/attachments/Paste-image-20250731-3.png)

**属性的初始化检查**

配置项：`strictPropertyInitialization:true`

属性的初始化位置：

1. 构造函数中
    
2. 属性默认值
	`gender: "男" | "女" = "男"`


**属性可以修饰为可选的**
`pid?: string`

**属性可以修饰为只读的**
`readonly id: number`

**使用访问修饰符**

访问修饰符可以控制类中的某个成员的访问权限

- public：默认的访问修饰符，公开的，所有的代码均可访问
    
- private：私有的，只有在类中可以访问
    
- protected：暂时不讲
    

>JS中使用Symble实现

**属性简写**

如果某个属性，通过构造函数的参数传递，并且不做任何处理的赋值给该属性。可以进行简写

**访问器**
set、get
语法糖
作用：用于控制属性的读取和赋值
```ts
set age(value: number) {
	if (value < 0) {
		this._age = 0;
	}
	else if (value > 200) {
		this._age = 200;
	}
	else {
		this._age = value;
	}
}

get age() {
	return Math.floor(this._age);
}
```
完整代码：
```ts
class User {
    readonly id: number //不能改变
    gender: "男" | "女" = "男"
    pid?: string
    private _publishNumber: number = 3; //每天一共可以发布多少篇文章
    private _curNumber: number = 0; //当前可以发布的文章数量

    constructor(public name: string, private _age: number) {
        this.id = Math.random();
    }

    set age(value: number) {
        if (value < 0) {
            this._age = 0;
        }
        else if (value > 200) {
            this._age = 200;
        }
        else {
            this._age = value;
        }
    }

    get age() {
        return Math.floor(this._age);
    }

    publish(title: string) {
        if (this._curNumber < this._publishNumber) {
            console.log("发布一篇文章：" + title);
            this._curNumber++;
        }
        else {
            console.log("你今日发布的文章数量已达到上限");
        }
    }
}

const u = new User("aa", 22);
//c#
u.age = 1.5;
console.log(u.age);


u.publish("文章1")
u.publish("文章2")
u.publish("文章3")
u.publish("文章4")
u.publish("文章5")
u.publish("文章6")
```
# 8.泛型

有时，书写某个函数时，会丢失一些类型信息（多个位置的类型应该保持一致或有关联的信息）

泛型：是指附属于函数、类、接口、类型别名之上的类型

泛型相当于是一个类型变量，在定义时，无法预先知道具体的类型，可以用该变量来代替，只有到调用时，才能确定它的类型
![](/img/user/04_TypeScript/attachments/Paste-image-20250731-4.png)
很多时候，TS会智能的根据传递的参数，推导出泛型的具体类型

如果无法完成推导，并且又没有传递具体的类型，默认为空对象

泛型可以设置默认值

## 在函数中使用泛型

在函数名之后写上`<泛型名称>`
![](/img/user/04_TypeScript/attachments/Paste-image-20250731-5.png)
## 如何在类型别名、接口、类中使用泛型

直接在名称后写上`<泛型名称>`

## 泛型约束

泛型约束，用于现实泛型的取值
![](/img/user/04_TypeScript/attachments/Paste-image-20250731-6.png)
将泛型T约束为一个有name属性的对象，如果不进行约束，T不一定是对象，就无法使用obj.name.
## 多泛型
```ts
//将两个数组进行混合
//[1,3,4] + ["a","b","c"] = [1, "a", 3, "b", 4, "c"]
function mixinArray<T, K>(arr1: T[], arr2: K[]): (T | K)[] {
    if (arr1.length != arr2.length) {
        throw new Error("两个数组长度不等");
    }
    let result: (T | K)[] = [];
    for (let i = 0; i < arr1.length; i++) {
        result.push(arr1[i]);
        result.push(arr2[i]);
    }
    return result;
}

const result = mixinArray([1, 3, 4], ["a", "b", "c"]);

result.forEach(r => console.log(r));
```

# 9.深入理解类和接口

## 面向对象概述

### 为什么要讲面向对象

1. TS为前端面向对象开发带来了契机
    JS语言没有类型检查，如果使用面向对象的方式开发，会产生大量的接口，而大量的接口会导致调用复杂度剧增，这种复杂度必须通过严格的类型检查来避免错误，尽管可以使用注释或文档或记忆力，但是它们没有强约束力。
	TS带来了完整的类型系统，因此开发复杂程序时，无论接口数量有多少，都可以获得完整的类型检查，并且这种检查是据有强约束力的。

2. 面向对象中有许多非常成熟的模式，能处理复杂问题
    在过去的很多年中，在大型应用或复杂领域，面向对象已经积累了非常多的经验。

### 什么是面向对象

面向对象：Oriented（基于） Object（事物），简称OO。

是一种编程思想，它提出一切以类对切入点思考问题。

其他编程思想：面向过程、函数式编程

> 学开发最重要最难的是什么？思维

面向过程：以功能流程为思考切入点，不太适合大型应用

函数式编程：以数学运算为思考切入点

面向对象：以划分类为思考切入点。类是最小的功能单元

类：可以产生对象的模板。

### 如何学习

1. TS中的OOP （面向对象编程，Oriented Object Programing）
    
2. 小游戏练习
    

理解 -> 想法 -> 实践 -> 理解 -> ....

## 类的继承

### 继承的作用

继承可以描述类与类之间的关系

> 坦克、玩家坦克、敌方坦克 玩家坦克是坦克，敌方坦克是坦克

如果A和B都是类，并且可以描述为A是B，则A和B形成继承关系：

- B是父类，A是子类
    
- B派生A，A继承自B
    
- B是A的基类，A是B的派生类
    

如果A继承自B，则A中自动拥有B中的所有成员

 @startuml  
 ​  
 Tank <|-- PlayerTank  
 Tank <|-- EnemyTank  
 EnemyTank <|-- BossTank  
 ​  
 @enduml

### 成员的重写

重写(override)：子类中覆盖父类的成员

子类成员不能改变父类成员的类型

无论是属性还是方法，子类都可以对父类的相应成员进行重写，但是重写时，需要保证类型的匹配。

注意this关键字：在继承关系中，this的指向是动态——调用方法时，根据具体的调用者确定this指向

super关键字：在子类的方法中，可以使用super关键字读取父类成员

### 类型匹配

鸭子辨型法

子类的对象，始终可以赋值给父类

面向对象中，这种现象，叫做里氏替换原则

如果需要判断一个数据的具体子类类型，可以使用instanceof

### protected修饰符

readonly：只读修饰符

访问权限修饰符：private public protected

protected: 受保护的成员，只能在自身和子类中访问

## 单根性和传递性

单根性：每个类最多只能拥有一个父类

传递性：如果A是B的父类，并且B是C的父类，则，可以认为A也是C的父类

## 抽象类

### 为什么需要抽象类

 @startuml  
 ​  
 棋子 <|-- 马  
 棋子 <|-- 兵  
 棋子 <|-- 炮  
 ​  
 @enduml

有时，某个类只表示一个抽象概念，主要用于提取子类共有的成员，而不能直接创建它的对象。该类可以作为抽象类。

给类前面加上`abstract`，表示该类是一个抽象类，不可以创建一个抽象类的对象。

### 抽象成员

父类中，可能知道有些成员是必须存在的，但是不知道该成员的值或实现是什么，因此，需要有一种强约束，让继承该类的子类，必须要实现该成员。

**抽象类中**，可以有抽象成员，这些抽象成员必须在子类中实现

### 设计模式 - 模板模式

设计模式：面对一些常见的功能场景，有一些固定的、经过多年实践的成熟方法，这些方法称之为设计模式。

模板模式：有些方法，所有的子类实现的流程完全一致，只是流程中的某个步骤的具体实现不一致，可以将该方法提取到父类，在父类中完成整个流程的实现，遇到实现不一致的方法时，将该方法做成抽象方法。

## 静态成员

### 什么是静态成员

静态成员是指，附着在类上的成员（属于某个构造函数的成员）

使用static修饰的成员，是静态成员

实例成员：对象成员，属于某个类的对象

静态成员：非实例成员，属于某个类

### 静态方法中的this

实例方法中的this指向的是**当前对象**

而静态方法中的this指向的是**当前类**

### 设计模式 - 单例模式

单例模式：某些类的对象，在系统中最多只能有一个，为了避免开发者造成随意创建多个类对象的错误，可以使用单例模式进行强约束。

## 再谈接口

接口用于约束类、对象、函数，是一个类型契约。

> 有一个马戏团，马戏团中有很多动物，包括：狮子、老虎、猴子、狗，这些动物都具有共同的特征：名字、年龄、种类名称，还包含一个共同的方法：打招呼，它们各自有各自的技能，技能是可以通过训练改变的。狮子和老虎能进行火圈表演，猴子能进行平衡表演，狗能进行智慧表演

> 马戏团中有以下常见的技能：

> - 火圈表演：单火圈、双火圈
>     
> - 平衡表演：独木桥、走钢丝
>     
> - 智慧表演：算术题、跳舞
>     

不适用接口实现时：

- 对能力（成员函数）没有强约束力
    
- 容易将类型和能力耦合在一起
    

系统中缺少对能力的定义 —— 接口

面向对象领域中的接口的语义：表达了某个类是否拥有某种能力

某个类具有某种能力，其实，就是实现了某种接口

类型保护函数：通过调用该函数，会触发TS的类型保护，该函数必须返回boolean

接口和类型别名的最大区别：接口可以被类实现，而类型别名不可以

> 接口可以继承类，表示该类的所有成员都在接口中。

## 索引器

`对象[值]`，使用成员表达式

在TS中，默认情况下，不对索引器（成员表达式）做严格的类型检查

使用配置`noImplicitAny`开启对隐式any的检查。

隐式any：TS根据实际情况推导出的any类型

在索引器中，键的类型可以是字符串，也可以是数字

在类中，索引器书写的位置应该是所有成员之前

TS中索引器的作用

- 在严格的检查下，可以实现为类动态增加成员
    
- 可以实现动态的操作类成员
    

在JS中，所有的成员名本质上，都是字符串，如果使用数字作为成员名，会自动转换为字符串。

在TS中，如果某个类中使用了两种类型的索引器，要求两种索引器的值类型必须匹配

## this指向约束

[https://yehudakatz.com/2011/08/10/understanding-javascript-function-invocation-and-this/](https://yehudakatz.com/2011/08/10/understanding-javascript-function-invocation-and-this/)

### 在JS中this指向的几种情况

明确：大部分时候，this的指向取决于函数的调用方式

- 如果直接调用函数（全局调用），this指向全局对象或undefined (启用严格模式)
    
- 如果使用`对象.方法`调用，this指向对象本身
    
- 如果是dom事件的处理函数，this指向事件处理对象
    

特殊情况：

- 箭头函数，this在函数声明时确定指向，指向函数位置的this
    
- 使用bind、apply、call手动绑定this对象
    

### TS中的this

配置noImplicitThis为true，表示不允许this隐式的指向any

在TS中，允许在书写函数时，手动声明该函数中this的指向，将this作为函数的第一个参数，该参数只用于约束this，并不是真正的参数，也不会出现在编译结果中。

# 10俄罗斯方块游戏

俄罗斯方块游戏 {ignore=true}概述工程搭建游戏开发开发小方块类小方块的显示类开发方块的组合类俄罗斯方块的生产者俄罗斯方块的规则类开发旋转功能开发游戏类触底处理积分完成游戏界面总结

## 概述

使用技术：webpack + jquery + typescript + 面向对象开发

项目目的：

1. 学习TS如何结合webpack做开发
    
2. 巩固TS的知识
    
3. 锻炼逻辑思维能力
    
4. 体验面向对象编程的思想
    

学习方法：

1. 调整心态，不要浮躁
    
2. 理解->思考->实践->理解->.....
    

## 工程搭建

环境：浏览器 + 模块化

webpack：构建工具，根据入口文件找寻依赖，打包

1. 安装webpack
    
2. 安装html-webpack-plugin
    
3. 安装clean-webpack-plugin
    
4. 安装webpack-dev-server
    
5. 安装ts的相应loader
    

ts-loader，awesome-typescript-loader

它们依赖typescript

## 游戏开发

单一职能原则：每个类只做跟它相关的一件事 开闭原则：系统中的类，应该对扩展开放，对修改关闭

基于以上两个原则，系统中使用如下模式： 数据-界面分离模式

传统面向对象语言，书写类的属性时，往往会进行如下操作：

1. 所有的属性全部私有化
    
2. 使用公开的方法提供对属性的访问
    

### 开发小方块类

小方块类：它能处理自己的数据，知道什么时候需要显示，但不知道怎么显示

> react、react-dom / react-native

### 小方块的显示类

作用：用于显示一个小方块到页面上

### 开发方块的组合类

组合类中的属性：

- 小方块的数组
    

思考：该数组的组成能不能发生变化。

回答：不能发生变化，是只读数组

思考：该数组的每一项从何而来

一个方块的组合，取决于组合的形状（一组相对坐标的组合，该组合中有一个特殊坐标，表示形状的中心）

如果知道：形状、中心点坐标、颜色，就可以设置小方块的数组

- 形状
    

### 俄罗斯方块的生产者

### 俄罗斯方块的规则类

### 开发旋转功能

旋转的本质：根据当前形状 -> 新的形状

- 有些方块是不旋转的，有些方块旋转时只有两种状态
    

rotate方法有一种通用的实现方式，但是，不同的情况下，会有不同的具体实现

将SquareGroup作为父类，其他的方块都是它的子类，子类可以重写父类的方法

- 旋转不能超出边界
    

### 开发游戏类

Game类清楚什么时候进行显示的切换，但不知道如何显示

### 触底处理

触底：当前方块到达最底部

什么时候可能发生触底？（什么时候调用函数）

1. 自动下落
    
2. 玩家控制下落
    

触底之后做什么？（函数如何编写的问题）

- 切换方块
    
- 保存已落下的方块
    
- 消除方块的处理
    

消除时做哪些事？ 从界面上移除、从exists数组中移除，改变y坐标

- 游戏是否结束
    

### 积分

### 完成游戏界面

## 总结

为什么要讲面向对象？

1. 面向对象带来了新的开发方式
    

面向对象开发已经非常成熟，特别善于解决复杂问题

2. TypeScript的某些语法是专门为面向对象准备
    
3. 学习一些设计模式
    

为什么选择做游戏？

1. 游戏特别容易使用面向对象的思维
    
2. 目前这门课的受众有一定的开发经验
    

开发：高内聚、低耦合

# 11.装饰器

## 概述

> 面向对象的概念（java：注解，c#：特征），decorator 
> angular大量使用，react中也会用到 
> 目前JS支持装饰器，目前处于建议征集的第二阶段

### 解决的问题

装饰器，能够带来额外的信息量，可以达到分离关注点的目的。

- 信息书写位置的问题
    
- 重复代码的问题
    

上述两个问题产生的根源：某些信息，在定义时，能够附加的信息量有限。

装饰器的作用：为某些属性、类、参数、方法提供元数据信息(metadata)

元数据：描述数据的数据
![](/img/user/04_TypeScript/attachments/Paste-image-20250731-7.png)
### 装饰器的本质

在JS中，装饰器是一个函数。（装饰器是要参与运行的）

装饰器可以修饰：

- 类
    
- 成员（属性+方法）
    
- 参数
    

## 类装饰器

类装饰器的本质是一个函数，该函数接收一个参数，表示类本身（构造函数本身）

使用装饰器`@得到一个函数`

在TS中，如何约束一个变量为类

- Function
    
- `new (参数)=>object`
    

在TS中要使用装饰器，需要开启`experimentalDecorators`

装饰器函数的运行时间：在类定义后直接运行

类装饰器可以具有的返回值：

- void：仅运行函数
    
- 返回一个新的类：会将新的类替换掉装饰目标
    

多个装饰器的情况：会按照后加入先调用的顺序进行调用。

## 成员装饰器

- 属性
    

属性装饰器也是一个函数，该函数需要两个参数：

1. 如果是静态属性，则为类本身；如果是实例属性，则为类的原型；
    
2. 固定为一个字符串，表示属性名
    

- 方法
    

方法装饰器也是一个函数，该函数需要三个参数：

1. 如果是静态方法，则为类本身；如果是实例方法，则为类的原型；
    
2. 固定为一个字符串，表示方法名
    
3. 属性描述对象
    

可以有多个装饰器修饰

## 练习：类和属性的描述装饰器

## reflect-metadata库

该库的作用：保存元数据

## class-validator 和 class-transformer 库

## 补充

- 参数装饰器
    

依赖注入、依赖倒置

要求函数有三个参数：

1. 如果方法是静态的，则为类本身；如果方法是实例方法，则为类的原型
    
2. 方法名称
    
3. 在参数列表中的索引
    

- 关于TS自动注入的元数据
    

如果安装了`reflect-metadata`，并且导入了该库，并且在某个成员上添加了元数据，并且启用了`emitDecoratorMetadata`。

则TS在编译结果中，会将约束的类型，作为元数据加入到相应位置

这样一来，TS的类型检查（约束）将有机会在运行时进行。

- AOP(aspect oriented programming)
    

编程方式，属于面向对象开发。

将一些在业务中共同出现的功能块，横向切分，已达到分离关注点的目的。

# 12.类型演算

> 根据已知的信息，计算出新的类型

## 三个关键字

- typeof
    

TS中的typeof，书写的位置在类型约束的位置上。

表示：获取某个数据的类型

当typeof作用于类的时候，得到的类型，是该类的构造函数

- keyof
    

作用于类、接口、类型别名，用于获取其他类型中的所有成员名组成的联合类型

- in
    

该关键字往往和keyof联用，限制某个索引类型的取值范围。

## TS中预设的类型演算

```ts
Partial<T>  // 将类型T中的成员变为可选  
Required<T>  // 将类型T中的成员变为必填  
​Readonly<T> // 将类型T中的成员变为只读  
Exclude<T, U> // 从T中剔除可以赋值给U的类型。  
Extract<T, U> // 提取T中可以赋值给U的类型。  
NonNullable<T> // 从T中剔除null和undefined。  
ReturnType<T> // 获取函数返回值类型。  
InstanceType<T> // 获取构造函数类型的实例类型。  
```
 
 ​
# 13.声明文件

> 概述、编写、发布

## 概述

1. 什么是声明文件？
    

以`.d.ts`结尾的文件

2. 声明文件有什么作用？
    

为JS代码提供类型声明

3. 声明文件的位置
    

- 放置到tsconfig.json配置中包含的目录中
    
- 放置到node_modules/@types文件夹中
    
- 手动配置
    
- 与JS代码所在目录相同，并且文件名也相同的文件。用ts代码书写的工程发布之后的格式。
    

## 编写

> 手动编写 自动生成

- 自动生成
    

工程是使用ts开发的，发布（编译）之后，是js文件，发布的是js文件。

如果发布的文件，需要其他开发者使用，可以使用声明文件，来描述发布结果中的类型。

配置`tsconfig.json`中的`declaration:true`即可

- 手动编写
    

1. 对已有库，它是使用js书写而成，并且更改该库的代码为ts成本较高，可以手动编写声明文件
    
2. 对一些第三方库，它们使用js书写而成，并且这些第三方库没有提供声明文件，可以手动编写声明文件。
    

**全局声明**

声明一些全局的对象、属性、变量

> namespace: 表示命名空间，可以将其认为是一个对象，命名空间中的内容，必须通过`命名空间.成员名`访问

**模块声明**

**三斜线指令**

在一个声明文件中，包含另一个声明文件

## 发布

1. 当前工程使用ts开发
    

编译完成后，将编译结果所在文件夹直接发布到npm上即可

2. 为其他第三方库开发的声明文件
    

发布到@types/**中。

1） 进入github的开源项目：[https://github.com/DefinitelyTyped/DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)

2） fork到自己的开源库中

3） 从自己的开源库中克隆到本地

4） 本地新建分支（例如：mylodash4.3），在新分支中进行声明文件的开发

 在types目录中新建文件夹，在新的文件夹中开发声明文件

5） push分支到你的开源库

6） 到官方的开源库中，提交pull request

7） 等待官方管理员审核（1天）

审核通过之后，会将你的分支代码合并到主分支，然后发布到npm。

之后，就可以通过命令`npm install @types/你发布的库名`