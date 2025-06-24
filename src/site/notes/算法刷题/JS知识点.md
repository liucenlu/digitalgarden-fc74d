---
{"dg-publish":true,"permalink":"/算法刷题/JS知识点/","created":"2025-06-22T16:48:37.034+08:00","updated":"2025-06-24T13:33:49.731+08:00"}
---


## 1.JavaScript 字符串转数组方式总结

### 1. `str.split('')`
```js
const str = 'hello';
const arr = str.split('');
console.log(arr); // ['h', 'e', 'l', 'l', 'o']
```

- ✅ **优点**：  
    - 简洁、直观      
    - 表达“按字符拆分”的语义明确    
- ⚠️ **注意**：
    - 在旧环境中对 Unicode（如 emoji、中文字符）可能存在拆分错误（现代浏览器已兼容）
        

### 2. `Array.from(str)`

```js
const str = 'hello';
const arr = Array.from(str);
console.log(arr); // ['h', 'e', 'l', 'l', 'o']
```

- ✅ **优点**： 
    - 支持 Unicode 正确拆分（包括 emoji）    
    - 支持第二个参数用于字符映射（类似 `map`）
        
```js
Array.from('abc', c => c.toUpperCase()); // ['A', 'B', 'C']
```

- ⚠️ **注意**：
    - 语法略复杂，兼容 ES6+      


### 3. 扩展运算符 `[...]str`

```js
const str = 'hello';
const arr = [...str];
console.log(arr); // ['h', 'e', 'l', 'l', 'o']
```

- ✅ **优点**：
    
    - 简洁现代，支持 Unicode
        
- ⚠️ **注意**：
    
    - 和 `Array.from()` 底层行为相同
        
    - 也需要 ES6 支持
        

### 4. `Object.assign([], str)`

```js
const str = 'hello';
const arr = Object.assign([], str);
console.log(arr); // ['h', 'e', 'l', 'l', 'o']
```

- ✅ **特点**：
    - 冷门技巧，效果类似    
- ⚠️ **缺点**： 
    - 可读性差，语义不清晰，不推荐日常使用
        
## 2.哈希表
哈希表（Hash Table），也称为哈希映射（Hash Map），是一种将键（Key）映射到值（Value）的数据结构。它利用哈希函数将键映射到一个数组中的一个位置（或桶），从而可以快速地查找对应的值。

在 JavaScript 中，哈希表可以使用对象（Object）或者 `Map` 类来实现。下面是两种实现方式的简单介绍：

### 使用对象（Object）

JavaScript 对象通常用作哈希表，因为它们可以将键与值关联起来。以下是一个简单的例子：

[scrollX]

```js
// 创建一个空对象
let hashTable = {}; 
// 添加键值对 
hashTable['name'] = 'Alice'; 
hashTable['age'] = 30; 
hashTable['city'] = 'New York'; 
// 访问值console.log(hashTable['name']); // 输出: Aliceconsole.log(hashTable['age']); // 输出: 30// 删除键值对delete hashTable['city']; 
console.log(hashTable['city']); // 输出: undefined
```

### 使用 `Map`

`Map` 对象是 JavaScript 内置的数据结构，提供了一种更为强大的方式来创建哈希表。与对象不同，`Map` 可以使用任何值（包括对象和函数）作为键。

```js
// 创建一个新的 
Maplet hashTable = newMap(); 
// 添加键值对 
hashTable.set('name', 'Alice'); hashTable.set('age', 30); hashTable.set('city', 'New York'); 
// 访问值console.log(hashTable.get('name')); // 输出: Aliceconsole.log(hashTable.get('age')); // 输出: 30// 删除键值对 
hashTable.delete('city'); console.log(hashTable.get('city')); // 输出: undefined// 检查是否存在某个键console.log(hashTable.has('name')); // 输出: true// 获取 Map 的大小console.log(hashTable.size); // 输出: 2
```

## parseInt和toString
`parseInt`和`toString`是 JavaScript 中用于处理数字和字符串转换的两个重要函数，下面来详细介绍。

### parseInt

`parseInt`是一个全局函数，其主要功能是将字符串转换为整数。它的语法结构为`parseInt(string, radix)`，这里的`radix`代表进制，其取值范围在 2 到 36 之间。

下面是`parseInt`的一些关键特性：

- 该函数会忽略字符串开头的空白字符。
- 一旦遇到无法解析的字符，就会停止解析。
- 要是没有提供`radix`参数，它会依据字符串的前缀来判断进制。例如，以`0x`开头的字符串会被当作十六进制数。不过需要注意的是，如果字符串没有明显的前缀，JavaScript 在 ES5 之前可能会默认按八进制解析，但在 ES5 及之后则会默认按十进制解析。
- 如果字符串无法被解析成数字，函数会返回`NaN`。

下面来看一些具体的示例：

```javascript
parseInt("10");        // 返回 10（默认按十进制解析）
parseInt("10", 10);    // 返回 10（明确指定十进制）
parseInt("10", 2);     // 返回 2（按二进制解析）
parseInt("0xF", 16);   // 返回 15（按十六进制解析）
parseInt("5 years");   // 返回 5（遇到非数字字符停止解析）
parseInt("years 5");   // 返回 NaN（因为第一个字符就不是数字）
parseInt("08");        // 返回 8（在ES5及之后按十进制解析，而不是八进制）
```

 
### toString

`toString`是 JavaScript 中大多数对象都拥有的方法，在处理数字时，它可以把数字转换为指定进制的字符串。其语法为`num.toString(radix)`，这里的`radix`同样表示进制，范围是 2 到 36，默认值为 10。

 
`toString`的主要特点如下：

- 能够将数字转换为不同进制的字符串形式。
- 对于整数和浮点数都适用。
- 如果数字是`NaN`或者`Infinity`，则会直接返回对应的字符串。 

以下是一些示例：

```javascript
(10).toString();       // 返回 "10"（默认按十进制转换）
(10).toString(2);      // 返回 "1010"（转换为二进制）
(10).toString(16);     // 返回 "a"（转换为十六进制）
(0xFF).toString(10);   // 返回 "255"（从十六进制转换为十进制字符串）
(10.5).toString();     // 返回 "10.5"
(NaN).toString();      // 返回 "NaN"
(Infinity).toString(); // 返回 "Infinity"
```

### 总结

`parseInt`和`toString`的作用刚好相反：

- `parseInt`的核心是将字符串转换为整数，并且可以指定进制。
- `toString`则是把数字转换为字符串，同样能够指定进制。

在实际使用时，还需要注意以下几点：

- 使用`parseInt`时，一定要明确指定`radix`，这样可以避免因默认行为不同而产生的问题。
- 对于`toString`，要留意它是对象的方法，所以在使用字面量数字调用时，可能需要添加额外的括号或者点。例如`(10).toString()`或者`10..toString()`。

## 哈希表和哈希集合

[list2tab]

+ 概念
	+ 哈希表
		+ > 哈希表是一种 **通过“键”快速查找对应“值”** 的数据结构
		+ 底层原理是：将键通过 **哈希函数** 映射到数组索引，实现高效访问，平均时间复杂度为 **O(1)**。
	+ 哈希集合
		+ > 哈希集合是一种 **只存“唯一值”** 的集合结构，常用于去重或存在性判断。
		+ 也是通过哈希函数快速判断某个值是否存在。
+ 实现方式
	+ 哈希表
		+ Object：键只能是字符串或 Symbol，适合简单映射
		+ Map：键可以是任意类型（对象、函数等），功能更强大
	+ 哈希集合
		+ Set：内置类，用于存储唯一值，不允许重复
+ 示例
	+ 哈希表		  
	    ```js
		const map = new Map();
		map.set('name', 'Alice');
		map.set('age', 20);
			
		console.log(map.get('name')); // 'Alice'
	    ```
	- 哈希集合
		```js
		const set = new Set();
		set.add(1);
		set.add(2);
		set.add(1); // 重复添加无效
		console.log(set.has(1)); // true
		console.log(set.size);   // 2 
		```

## ES6新特性
### 箭头函数
[[前端八股/Javascript/前端面试 JavaScript篇_w3cschool#4. 箭头函数与普通函数的区别\|箭头函数与普通函数的区别]]
[[前端面试/项目+八股文#箭头函数与普通函数的区别 ？箭头区别面试\|箭头区别面试]]
### 模板语法
[[前端八股/Javascript/前端面试 JavaScript篇_w3cschool#11. ES6中模板语法与字符串处理\|ES6中模板语法与字符串处理]]
### 解构赋值
JavaScript 的解构赋值（Destructuring Assignment）是一种从数组或对象中提取数据并赋给变量或表达式的简洁语法，属于 ES6 引入的重要特性。它通过模式匹配（Pattern Matching）从数据结构中提取值，简化了代码逻辑，提高了可读性。

[list2tab]

+ 数组解构
	从数组中按顺序提取元素，变量名对应数组索引的位置：
	```js
	// 基础用法
	const arr = [1, 2, 3];
	const [a, b, c] = arr; // a=1, b=2, c=3
	
	// 剩余元素（...）
	const [x, y, ...rest] = arr; // rest = [3]
	
	// 默认值
	const [first, second = 'default'] = [1]; // second = 'default'
	
	// 嵌套数组
	const nestedArr = [[1, 2], [3, 4]];
	const [[a], [b]] = nestedArr; // a=1, b=3

	```
+ 对象解构
	从对象中按属性名提取值，变量名需与对象的键名一致：
	```js
	// 基础用法
	const obj = { name: 'Alice', age: 25 };
	const { name, age } = obj; // name='Alice', age=25
	
	// 可选链（嵌套对象）
	const user = { info: { name: 'Bob' } };
	const { info: { name } } = user; // name='Bob'
	
	// 默认值
	const { username = 'guest', role = 'user' } = {}; // username='guest'
	
	// 嵌套默认值
	const { profile: { avatar = 'default.jpg' } = {} } = {}; // avatar='default.jpg'
	
	// 忽略属性（使用逗号跳过）
	const { name, , role } = obj; // 中间变量被忽略
	
	```
+ 解构与其它语法结合
	+ (1) 函数参数解构
	```js
	function greet({ name, greeting = 'Hello' }) {
	  console.log(`${greeting}, ${name}!`);
	}
	greet({ name: 'Alice' }); // 输出 "Hello, Alice!"
	greet({ name: 'Bob', greeting: 'Hi' }); // 输出 "Hi, Bob!"
	
	```
	+ (2) 剩余参数与解构
	```js
	function sum([a, b, ...rest]) {
		return a + b + rest.reduce((sum, num) => sum + num, 0);
		}
		sum([1, 2, 3, 4]); // 输出 10
	```
	+ (3) 扩展运算符（...）
	```js
	// 数组合并
	const combined = [...arr1, ...arr2];
	// 对象合并（浅层合并）
	const mergedObj = { ...obj1, ...obj2 };
		
	```
+ 其它形式的解构
	+ (1) 字符串解构
	```js
	const str = 'hello';
	const [h, e, l, l, o] = str; // h='h', e='e', 等
	
	```
	+ (2) Set 和 Map 解构
	```js
	const mySet = new Set([1, 2, 3]);
	const { first, second } = mySet; // first=1, second=2（顺序不确定）
	
	const myMap = new Map([
	  ['name', 'Alice'],
	  ['age', 25]
	]);
	const { name, age } = myMap; // name='Alice', age=25
	
	```
