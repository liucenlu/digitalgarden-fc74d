---
{"dg-publish":true,"permalink":"/05_Angular18/Angular/","created":"2025-07-29T16:13:55.673+08:00","updated":"2025-10-09T19:17:28.590+08:00"}
---

## 学习资源
1. Angular18官网文档：[什么是 Angular？ • Angular](https://v18.angular.cn/overview)
2. 视频教程
	1. YouTube
		1. https://www.youtube.com/watch?v=JWhRMyyF7nc 4小时，简短，基础，V18，配套齐全
		2. https://www.youtube.com/watch?v=3qBXWUpoPHo 17小时，fcc提供，V12，从Typescript 的基础知识讲起，印度英语，字幕识别和翻译不太准确
		3. https://www.youtube.com/watch?v=oUmVFHlwZsI 90分钟速成，配套资源齐全，版本正好是V18
	2. B站
		1. [【2022版】angular零基础教程合集 | 这么完整的前端教学一定要看看 -零基础到实战精通 Angular/实战/服务/框架 T0001_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1TY4y157Y5?spm_id_from=333.788.videopod.episodes&vd_source=87ad7f6fa4bfe76b6604c6fe42cb55fc) 30p\*15min，V11 
3. 知识储备前提：HTML、CSS 和 TypeScript
	- JAvaScript类
	- TypeScript基础
	- TypeScript装饰器

## Angular-in-90ish
通过完成一个包含Todo-List组件的Angular项目来学习以下Angular核心概念
![](/img/user/05_Angular18/attachments/Paste-image-20250805.png)
1. 拉代码到本地
	1. `git clone https://github.com/AhsanAyaz/angular-in-90ish.git`
2. 运行幻灯片
	1. `pnpm install`
	2. `npm run dev`
3. 运行教程应用
	1. `cd first-ng-app`
	2. `pnpm install`
	3. `pnpm start`
	4. 打开`localhost:4200`

### 创建Angular应用
1. 安装脚手架
	`npm install -g @angular/cli`
2. check cli版本
	`ng --version`
3. 创建Angular应用
	`ng new first-ng-app`
	`ng new first-ng-app --dry-run`
	- `--dry-run`：表示“试运行”，不会真正创建文件或更改磁盘内容，只会在终端显示将要创建哪些文件和目录。
	`ng new first-ng-app --inline-style --inline-template`
	- `--inline-styles`：组件的样式会直接写在组件的 TypeScript 文件里（即 `styles` 属性），不会生成单独的 `.css` 或 `.scss` 文件。
	- `--inline-template`：组件的模板会直接写在组件的 TypeScript 文件里（即 template 属性），不会生成单独的 `.html` 文件。
4. 运行
	1. `npm start`
### 代码结构
![](/img/user/05_Angular18/attachments/Paste-image-20250801-2.png)
1. index.html
	![](/img/user/05_Angular18/attachments/Paste-image-20250801.png)
	Angular 应用的主入口 HTML 文件，是 Angular 应用的外壳，实际页面内容由 Angular 组件动态生成并插入 `<app-root>` 标签中。
2. main.ts
	![](/img/user/05_Angular18/attachments/Paste-image-20250801-1.png)
	 Angular 应用的主入口 TypeScript 文件，负责启动 Angular 应用，是整个项目的入口点。
	 - bootstrapApplication(AppComponent, appConfig)
    使用 bootstrapApplication方法启动 Angular 应用，把 AppComponent 作为根组件，并应用 appConfig 配置。
	- `.catch((err) => console.error(err));`  
    如果启动过程中出错，会在控制台输出错误信息。
3. style.scss
	Angular 应用的全局样式文件（styles.scss）
### 组件
![](/img/user/05_Angular18/attachments/Paste-image-20250801-3.png)
**Angular 组件**是 Angular 应用的基本构建块。每个组件由三部分组成：
1. **模板（template）**：定义组件的视图（HTML结构）。
2. **类（class）**：包含数据和逻辑（TypeScript代码）。
3. **样式（styles）**：定义该组件的专属样式（CSS/SCSS）。

组件通过装饰器 `@Component` 进行声明，并通过 selector 指定在页面中的标签名。

**重要性：**

- **模块化开发**：每个组件负责一块独立的功能，便于开发、维护和复用。
- **视图与逻辑分离**：模板负责展示，类负责数据和行为，结构清晰。
- **组合应用**：整个 Angular 应用就是由组件树组合而成的，根组件（如 `<app-root>`) 是入口，其他组件嵌套其中。
- **便于测试**：每个组件可以单独测试，提高代码质量。

#### 1. app.component.ts
这是 Angular 应用的根组件文件，定义了 Angular 应用的根组件，负责显示欢迎信息，并作为路由内容的容器。
![](/img/user/05_Angular18/attachments/Paste-image-20250801-4.png)
- `@Component({...})`  
	组件的装饰器，定义了组件的元数据：
- selector: 'app-root'：该组件在 HTML 中用 `<app-root></app-root>` 标签表示。
- imports: \[RouterOutlet]：声明该组件模板中会用到的路由出口。
- template: ...：组件的内联模板，显示欢迎语和 `<router-outlet />`，用于路由内容的占位。
- \[styles: []]：组件的样式，这里为空数组，表示没有单独样式。
- export class AppComponent  
	组件的类定义，包含一个 title 属性，值为 `'myfirst-ng-app'`，用于模板绑定。

> [!样式泄露的避免]
> 
> ![](/img/user/05_Angular18/attachments/Paste-image-20250801-6.png)
> Angular会自动为组件的 DOM 元素添加独特的属性选择器，实现样式作用域隔离。这样组件样式只作用于本组件，不会影响其他组件。

#### 2. 创建组件
1. `ng generate component header`
	1. 简写：`ng g c header`
	2. 生成一个名为 `header` 的组件，文件会在 `src/app/header/` 目录下。
2. `ng g c component/header`
	- 生成一个名为 `header` 的组件，并放在 `src/app/component/header/` 目录下。
创建结果：
![](/img/user/05_Angular18/attachments/Paste-image-20250801-7.png)

---
1. header.component.ts
	```ts
	import { Component } from '@angular/core';
	
	@Component({
	  selector: 'app-header',
	  imports: [],
	  templateUrl: './header.component.html',
	  styleUrl: './header.component.scss'
	})
	export class HeaderComponent {
	
	}
	
	```
	- 与前面的主组件内容不同的是templateUrl和styleUrl指向了单独的html和css文件
---
3. `ng g c home`
#### 3. 导入组件
![](/img/user/05_Angular18/attachments/Paste-image-20250801-8.png)

#### 模板语法
Angular支持四种主要的数据绑定方式：
##### 1. 插值绑定（Interpolation）- `{{}}`

用于在模板中显示组件属性的值：

`<p>Hello {{userName}}!</p>`

##### 2. 属性绑定（Property Binding）- `[]`

将组件属性值绑定到DOM元素的属性：

```html
<img [src]="imageUrl" /> 
<button [disabled]="isDisabled">Click me</button>
```

##### 3. 事件绑定（Event Binding）- `()`

将DOM事件绑定到组件的方法：
```html
<button (click)="handleClick()">Click me</button> 
<input (input)="onInputChange($event)" />
```

##### 4. 双向绑定（Two-way Binding）- `[()]`

结合了属性绑定和事件绑定，实现数据的双向同步：
`<input [(ngModel)]="userName" />`

##### 数据流方向

- **单向下行绑定**：组件到模板（Interpolation、Property Binding）
- **单向上行绑定**：模板到组件（Event Binding）
- **双向绑定**：组件与模板间双向数据流（Two-way Binding）
#### 4.数据绑定Data-binding|Signal
Angular的数据绑定（Data Binding）是Angular框架的核心特性之一，它允许在组件的 TypeScript 类和模板之间建立连接，实现数据的自动同步。
1. 基于Signal的数据绑定
	[信号 • 概览 • Angular](https://v18.angular.cn/guide/signals#)
	**signal** 是一个值的包装器，当该值变化时通知订阅的消费者。信号可以包含任何值，从原始类型到复杂数据结构。使用时通过函数调用的方式。
	信号可以是 _可写的_ 或 _只读的_。可以通过==set==或==update==方法更新值。
	1. **自动响应式**：当 signal 值变化时，模板会自动更新
	2. **细粒度控制**：只更新依赖该 signal 的部分
	3. **类型安全**：TypeScript 提供完整的类型检查支持
	4. **性能优化**：相比传统变更检测，signal 提供更好的性能 ![](/img/user/05_Angular18/attachments/Paste-image-20250804.png)
2. 数据绑定的传统方式（Angular16或以下）
	1. 使用时不需要通过函数调用的方式。
	2. ![](/img/user/05_Angular18/attachments/attachments/Pasted image 20250804152701.png)
#### 5. 增加更多组件
![](/img/user/05_Angular18/attachments/Paste-image-20250804-1.png)
`ng g c components/greeting`
#### 6. 数据传递
通过inputs将数据从父组件传递到子组件
目前的组件结构如下：
![](/img/user/05_Angular18/attachments/Paste-image-20250804-2.png)
尝试将message从组件app-home传递到app-greeting
1. 在子组件中创建组件接受输入属性（input）
	>输入属性类似于其它框架中的 _props_。
	
	
	1. `input()` 函数（对应 Signal）
		1. `message = input<string>('hello');`
	2. `@Input()` 装饰器（传统方式）
		1. `@Input() message: string = 'hello';`

`input()` 是 `@Input()` 的现代化、响应式版本，它们解决的是同一个问题（组件间数据传递），但 `input()` 提供了更好的类型安全、更清晰的必需性声明和内置的响应式能力。两者在功能上是等价的，但 `input()` 代表了 Angular 的发展方向。
2. 在父组件中传递值
	1. ![](/img/user/05_Angular18/attachments/Paste-image-20250804-3.png)

#### 7. 事件监听器

[事件绑定 • Angular](https://v18.angular.cn/guide/templates/event-binding)

![](/img/user/05_Angular18/attachments/Paste-image-20250804-4.png)
ts类中定义事件处理方法
```ts
export class HomeComponent {
  homeMessage = signal('Hello from home');
   keyUpHandler() {
    console.log('user typed something in the input');
  }
}
```
html模板中绑定
![](/img/user/05_Angular18/attachments/Paste-image-20250804-5.png)

带参数的事件绑定
![](/img/user/05_Angular18/attachments/Paste-image-20250804-6.png)

#### 8.实现一个计数器
创建一个计数器组件`ng g c component/counter`
```ts
//counter.component.html.ts
export class CounterComponent {
  counterValue = signal(0);

  increase() {
    this.counterValue.update(value => value + 1);
  }
  decrease() {
    this.counterValue.update(value => value - 1);
  }
  reset() {
    this.counterValue.set(0);
  }
}
```
```html
//counter.component.html
<p>Counter Value:{{counterValue()}}</p>
<div>
  <button (click)="increase()">Increase</button>
  <button (click)="decrease()">Decrease</button>
  <button (click)="reset()">Reset</button>
</div>
```

#### 9. 路由
Angular 是一个 **单页面应用程序（Single Page Application，简称 SPA）**，特点是整个应用只加载一个 HTML 页面，之后通过 JavaScript 动态地更新视图，不需要每次跳转都向服务器请求一个新的页面。

虽然是“单页面”，但 Angular 通过 **路由（Routing）** 功能，允许你为不同的路径定义不同的组件视图。用户访问不同的路径时，Angular 会根据路径加载对应的组件内容。

Angular 支持 **按需加载（Lazy Loading）**，即用户访问某个页面时，浏览器只会加载该页面所需的代码资源，而不是一次性加载全部内容。  
这样可以：减少初次加载的时间、提高整体性能、提升用户体验
![](/img/user/05_Angular18/attachments/Paste-image-20250805-1.png)
创建一个todos页面
1. `ng g c todos`
2. 通过RouterOutlet来切换显示不同的组件内容（home/todos）
	定义路由
	```ts
	//app.routes.ts
	import { Routes } from '@angular/router';
	
	export const routes: Routes = [{
	  path: '',
	  pathMatch: 'full',//路径匹配策略，完全匹配
	  loadComponent: () => {//动态导入组件
	    return import('./home/home.component').then((m) => m.HomeComponent);
	  }
	}];
	```
	这样就可以通过\<router-outlet/>动态加载home组件了
	![](/img/user/05_Angular18/attachments/Paste-image-20250805-2.png)
3. 创建一个todo-item组件，将每一个todo事项作为一个组件在todos页面中
	1. `ng g c component/todo-item`
	2. 同样，在app.routes.ts中配置todos组件的路由信息
		![](/img/user/05_Angular18/attachments/Paste-image-20250805-3.png)
		此时可以通过路径`http://localhost:4200/todos`访问到todos组件的页面
	3. 通过RouterLink实现路由跳转
	```html
	//header.component.html
	<header>
	  <nav>
	    <span routerLink="/">{{title()}}</span>
	    <ul>
	      <li routerLink="/todos">Todos</li>
	    </ul>
	  </nav>
	</header>
	```
#### 10.依赖注入&&Angular Service
[依赖注入 • 概览 • Angular](https://v18.angular.cn/guide/di)
>我的理解：Angular Service用于封装数据、进行http调用获取执行一些跟数据渲染没有直接关系的任务。

> [!Angular Service]-
> Angular Service 是 Angular 应用程序中用于封装特定功能或业务逻辑的可重用组件。
>
>**什么是服务**
  服务是可重用的代码片段，可以被注入
>类似于定义组件，服务由以下内容组成：
>
>- 一个 **TypeScript 装饰器**，通过 `@Injectable` 声明该类为 Angular 服务，并允许你通过 `providedIn` 属性（通常为 `'root'`）定义应用程序中哪些部分可以访问该服务，从而允许服务在应用程序中的任何地方被访问。
>- 一个 **TypeScript 类**，定义当服务被注入时将可访问的代码
>
>**如何使用服务**
>
>- 导入服务
>- 声明一个类字段，服务被注入到其中。将类字段赋值为调用内置函数 `inject` 创建服务的结果
> ------
> **常见用途**
> 
> 1. **HTTP 数据获取**：
> 	```ts
> 	@Injectable({
> 	  providedIn: 'root'
> 	})
> 	export class UserService {
> 	  constructor(private http: HttpClient) {}
> 	
> 	  getUsers() {
> 	    return this.http.get<User[]>('/api/users');
> 	  }
> 	}
> 	```
> 2. **状态管理**：
> 	```ts
> 	@Injectable({
> 	  providedIn: 'root'
> 	})
> 	export class StateService {
> 	  private dataSubject = new BehaviorSubject\<any>(null);
> 	  public data$ = this.dataSubject.asObservable();
> 	
> 	  updateData(data: any) {
> 	    this.dataSubject.next(data);
> 	  }
> 	}
> 	```
> 3. **工具函数封装**：
> 	```ts
> 	@Injectable({
> 	  providedIn: 'root'
> 	})
> 	export class UtilityService {
> 	  formatDate(date: Date): string {
> 	    return date.toLocaleDateString();
> 	  }
> 	}
> 	```
> Service 是 Angular 架构中的核心概念之一，有助于实现关注点分离和代码重用。

1. 创建一个服务
	`ng g service services/todos`
	结果：
	![](/img/user/05_Angular18/attachments/Paste-image-20250805-4.png)
	以上配置在全局组件都可以使用此服务
	如果只需要在组件级别使用此服务，则需：
	1. 移除`providedIn: 'root'`
	2. 在组件装饰器配置：`providers:[TodosService]`
2. 定义一个todo类型
	```ts
	export type todo = {
	  userId: number;
	  id: number;
	  title:string;
	  completed: boolean;
	}
	```
3. 在todos组件中注入服务|==inject()==
	```ts
	export class TodosComponent {
	  todoService = inject(TodosService)
	}
	```
4. 在todos组件中使用服务
```ts
//todos.component.ts
export class TodosComponent implements OnInit {//OnInit是Angular的生命周期接口之一
  todoService = inject(TodosService);
  todoItems = signal<Array<todo>>([]);

  ngOnInit(): void {
    console.log(this.todoService.todoItems);  
    this.todoItems.set(this.todoService.todoItems);
  }
}
```
```html
//todos.component.html
<p>{{todoItems()[0].title}}</p>

//使用for循环渲染每一项
@for (todo of todoItems(); track todo.id){
  <p>{{ todo.title }}</p>
}
```
#### 11.控制流块
Angular 模板语法支持 _控制流块_，可以有条件地显示、隐藏和重复元素。
[控制流 • Angular](https://v18.angular.cn/guide/templates/control-flow#repeat-content-with-the-for-block)
@if
@for
@else
@switch

```html
// `@if` 和 `@else`
@if (isLogin) {
<p>欢迎回来！</p>
} @else {
<p>请先登录。</p>
}
```

```html
// `@for`
@for (item of items; track item.id) {
<li>{{ item.name }}</li>
}
```

```html
//`@switch`（替代 `ngSwitch`）
@switch (status) {
@case ('success') {
<p>操作成功！</p>
}
@case ('error') {
<p>发生错误。</p>
}
@default {
<p>未知状态。</p>
}
}
```

#### 12.HTTP 与后端服务通信
[发起请求 • Angular](https://v18.angular.cn/guide/http/making-requests)

1. 在app.config.ts中通过==providHttpClient()==提供http module/providers
	![](/img/user/05_Angular18/attachments/Paste-image-20250805-5.png)
2. 注入==HttpClient==服务
	```ts
	//todos.service.ts
	export class TodosService {
	  http = inject(HttpClient);
	  ...
	  }
	```
3. 使用==http==方法
	在todo服务中定义通过api获取todoItem的函数
```ts
export class TodosService {
http = inject(HttpClient);
getTodosFromApi(){
	const url = 'https://jsonplaceholder.typicode.com/todos';
	return this.http.get<Array<todo>>(url);
	}
}
```
在todo组件中订阅Observable
	`HttpClient` 具有与用于发出请求的不同 HTTP 动词相对应的方法，这些方法既可以加载数据，也可以在服务器上应用变更。每个方法都返回一个 [RxJS `Observable`](https://rxjs.dev/guide/observable)，当订阅时，会发送请求并在服务器响应时发出结果。
```ts
	export class TodosComponent implements OnInit {//OnInit是Angular的生命周期接口之一
	  todoService = inject(TodosService);
	  todoItems = signal<Array<todo>>([]);
	
	  ngOnInit(): void {
	    this.todoService.getTodosFromApi()
	    .pipe(catchError((err)=>{
	      console.log(err);
	      throw err;
	    }))
	    .subscribe((todos)=>{
	      this.todoItems.set(todos);
	    })
	  }
	}
```
现在已经可以通过todos页面展示所以通过api获得的todoItems了，只需要再修改一些todos页面的html以及样式即可获得更好的页面效果

#### 13.指令
[指令 • 概览 • Angular](https://v18.angular.cn/guide/directives)
Angular 指令是 Angular 应用中用于修改 DOM 元素行为或外观的类，是 Angular 模板系统的核心组成部分。

| 指令类型                                                                            | 详情                        | 举例                                          |
| :------------------------------------------------------------------------------ | :------------------------ | ------------------------------------------- |
| [组件](https://v18.angular.cn/guide/components)                                   | 用于模板。这种类型的指令是最常见的指令类型。    | 自定义组件                                       |
| [属性型指令](https://v18.angular.cn/guide/directives#built-in-attribute-directives)  | 更改元素、组件或其他指令的外观或行为。       | `[ngClass]`, `[ngStyle]`，`[(ngModel)]`自定义指令 |
| [结构型指令](https://v18.angular.cn/guide/directives#built-in-structural-directives) | 通过添加和删除 DOM 元素来更改 DOM 布局。 | *ngIf, *ngFor, *ngSwitch                    |
```html
//todos.component.ts
<h3>Todos List</h3>

//结构型指令*ngif
<!-- <p *ngIf="!todoItems().length">Loading...</p> -->
@if(!todoItems().length){
  <p>Loading...</p>
}

<ul class="todos">
...
</ul>
```
1. 给已完成的todoItems创建一个指令
	`ng g directive directives/highlight-completed-todo`
2. 自定义指令
	```ts
	export class HighlightCompletedTodoDirective {
	  isCompleted = input(false);
	  el = inject(ElementRef);//ElementRef 提供对指令所附加的 DOM 元素的直接访问
	  
	  stylesEffect = effect(()=>{//使用 effect 创建一个副作用函数，当依赖的信号变化时自动执行
	    if(this.isCompleted()){
	      this.el.nativeElement.style.textDecoration = 'line-through';
	      this.el.nativeElement.style.color = '#6c757d';
	      this.el.nativeElement.style.backgroundColor = '#d3f9d8';
	    }else{
	      this.el.nativeElement.style.textDecoration = 'none';
	      this.el.nativeElement.style.color = '#000';
	      this.el.nativeElement.style.backgroundColor = '#fff';
	    }
	  })
	}
	
	```
	- 当 isCompeleted 输入值改变时，自动更新元素样式
	- 根据完成状态应用不同的样式：
	    - 完成时：添加删除线、灰色文字、浅绿色背景
	    - 未完成时：无装饰、黑色文字、白色背景
3. 将指令应用到元素上
	```html
	//todo-item.component.html
	  <li appHighlightCompletedTodo [isCompleted]="todo().completed" class="todos__item">
	    <input id="todo-{{todo().id}}" type="checkbox" [checked]="todo().completed" />
	    <label for="todo-{{todo().id}}">{{todo().title}}</label>
	  </li>
	```


>子组件向父组件传递数据|emit

子组件todo-item发生变化后传递更新completed值给父组件todos，父组件更新todoItems数组，子组件重新渲染
1. 在子组件中定义输出属性
	```ts
	export class TodoItemComponent {
	  todo = input.required<todo>();
	  todoToggled = output<todo>();
	
	  todoClicked(){
	    this.todoToggled.emit(this.todo());
	  }
	}
	```
	1. `todoToggled = output<todo>();` 是Angular中定义组件输出属性的语法，用于子组件向父组件传递数据。todoToggled 是输出属性的名称，父组件可以通过这个名称监听子组件的事件。
	2. 子组件发生变化后触发todoClicked()
		```html
		<input id="todo-{{todo().id}}" type="checkbox" [checked]="todo().completed" (change)="this.todoClicked()" />
		```
2. 父组件中
	```html
	  <app-todo-item (todoToggled)="updateTodoItem($event)" [todo]="todo"/>
	```
	- `(todoToggled)="updateTodoItem($event)"` - 监听子组件触发的 `todoToggled` 事件
	- 当子组件调用 `this.todoToggled.emit(this.todo());` 时，会触发父组件的 `updateTodoItem()` 方法
	- `$event` 包含子组件传递出来的 todo 对象
#### 14.管道
`Pipe`（管道）是一种用于转换模板中数据显示格式的特殊类，它可以在不改变原始数据的情况下，对视图中的数据进行格式化、过滤或转换。

**管道的基本特点**

- 用于模板中，通过 `|` 符号（管道符）使用
- 可以链式使用多个管道
- 分为内置管道和自定义管道两种类型

**内置管道**
将todoItem的title以大写格式显示
1. 导入UpperCasePipe
2. 应用UpperCasePipe
	![](/img/user/05_Angular18/attachments/Paste-image-20250806.png)
	这里的样式是通过JS修改的而不是CSS

**自定义一个管道**
过滤显示已完成的item
1. `ng g pipe pipes/filter-todos`创建一个管道
2. 定义过滤管道
	```ts
	import { Pipe, PipeTransform, signal } from '@angular/core';
	import { todo } from '../model/todo.type';
	
	@Pipe({
	  name: 'filterTodos'
	})
	export class FilterTodosPipe implements PipeTransform {
	
	  transform(todos: todo[], searchTerm: string): todo[] {
	    if(!searchTerm){
	      return todos;
	    }
	    return todos.filter(todo=>{
	      return todo.title.toLowerCase().includes(searchTerm.toLowerCase());
	    })
	  }
	}
	```
	**类结构和属性**：	
	1. **implements PipeTransform** - 实现Angular的管道转换接口		
		**transform方法**：	
		这是管道的核心方法，负责实际的数据转换：	
		1. **参数**：	    
		    - `todos: todo[]` - 输入的待办事项数组
		    - `searchTerm: string` - 搜索关键词
		2. **逻辑**：    
		    - 如果没有搜索词（`!searchTerm`），直接返回原数组
		    - 否则使用 `filter` 方法过滤数组，只保留标题包含搜索词的待办事项
		    - 过滤时使用不区分大小写的匹配（通过 `toLowerCase()` 实现）
3. 导入并使用管道
	1. ![](/img/user/05_Angular18/attachments/Paste-image-20250806-3.png)
	 - 管道操作符左侧的值（这里是 `todoItems()`）会自动作为 transform 方法的第一个参数传入
	- 冒号（`:`）后面的是额外的参数，对应 transform 方法的第二个参数及后续参数
4. `[(ngModel)]="searchTerm"`
	1. 语法含义	
		- **[ngModel]** - 属性绑定：将组件中的 searchTerm 值绑定到input元素
		- **(ngModel)** - 事件绑定：监听input元素值的变化事件
		- **[(ngModel)]** - 双向绑定：同时实现属性绑定和事件绑定
	
	2. 工作原理
		1. **从组件到视图**：当组件中的 searchTerm 值改变时，input框会自动更新显示
		2. **从视图到组件**：当用户在input框中输入内容时，searchTerm 的值会自动更新

### 补充：Angular的生命周期钩子

Angular 的生命周期钩子（Lifecycle Hooks）是组件或指令在其生命周期中某些特定时间点会自动调用的方法。你可以在这些时间点插入自定义逻辑，比如初始化数据、清理资源、检测变化等。

| **阶段**           | **方法**                                                                       | **总结**                                                                                                                            |
| ---------------- | ---------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| 创建               | `constructor`                                                                | [标准 JavaScript 类构造函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor) 。在 Angular 实例化组件时运行。 |
| Change<br><br>检测 | [ngOnInit](https://v18.angular.cn/guide/components/lifecycle#ngoninit)       | 在 Angular 初始化所有组件输入后运行一次。                                                                                                         |
|                  | [ngOnChanges](https://v18.angular.cn/guide/components/lifecycle#ngonchanges) | 每次组件输入发生变化时运行。                                                                                                                    |
|                  | `ngDoCheck`                                                                  | 每次检查此组件是否有变化时运行。                                                                                                                  |
|                  | `ngAfterViewInit`                                                            | 在组件的 _视图_ 初始化后运行一次。                                                                                                               |
|                  | `ngAfterContentInit`                                                         | 在组件的 _内容_ 初始化后运行一次。                                                                                                               |
|                  | `ngAfterViewChecked`                                                         | 每次检查组件视图是否有变化时运行。                                                                                                                 |
|                  | `ngAfterContentChecked`                                                      | 每次检查此组件内容是否有变化时运行。                                                                                                                |
| 渲染               | `afterNextRender`                                                            | 当**所有**组件都已渲染到 DOM 时运行一次。                                                                                                         |
|                  | `afterRender`                                                                | 每次**所有**组件都渲染到 DOM 时运行。                                                                                                           |
| 销毁               | [ngOnDestroy](https://v18.angular.cn/guide/components/lifecycle#ngondestroy) | 在组件被销毁前运行一次。                                                                                                                      |
>`afterRender` 和 `afterNextRender` **不是 Angular 的标准生命周期钩子**，它们并不属于 Angular 框架定义的生命周期接口。

#### 执行顺序
初始化期间
![](/img/user/05_Angular18/attachments/Paste-image-20250806-1.png)
后续更新
![](/img/user/05_Angular18/attachments/Paste-image-20250806-2.png)
### 浏览器插件Angular Dev Tools
![](/img/user/05_Angular18/attachments/Paste-image-20250801-5.png)**Angular DevTools** 是一款官方推出的浏览器开发者工具插件，主要用于调试和分析 Angular 应用。常见特性如下：

- **组件树查看**：可直观地查看应用的组件结构，了解各组件的嵌套关系。
- **属性和状态检查**：可以实时查看和修改组件的输入属性（@Input）、输出事件（@Output）以及内部状态。
- **依赖注入树**：可查看服务的注入关系，帮助理解依赖注入的层级。
- **性能分析**：可以分析变更检测（Change Detection）性能，定位性能瓶颈。
- **路由信息**：可查看当前路由状态和路由参数。
