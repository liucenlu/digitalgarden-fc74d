---
{"dg-publish":true,"permalink":"/03_Vue/vue学习-基础/Vue3学习（基础）/","created":"2025-09-11T03:08:04.000+08:00","updated":"2025-10-09T18:51:05.926+08:00"}
---

# Vue3学习（基础）

# **一. Vue.js 是什么？**

Vue.js 是一个用于构建用户界面的 JavaScript 框架。它可以帮助你轻松地将数据和页面绑定在一起，当数据变化时，页面会自动更新。

---

# **二. 示例代码的结构**

Vue.js 的代码通常分为三部分：

1. **模板（Template）**：HTML 部分，用来定义页面的结构。
2. **脚本（Script）**：JavaScript 部分，用来定义数据和逻辑。
3. **样式（Style）**：CSS 部分，用来定义页面的样式。

---

# 三.Vue互动教程

[教程 | Vue.js](https://cn.vuejs.org/tutorial/#step-2)

![image.png](/img/user/03_Vue/vue学习-基础/image.png)

## 1. 声明式渲染

- vue单文件组件（Single-File Component，SFC），它将从属于同一个组件的 HTML、CSS 和 JavaScript 封装在使用 `.vue` 后缀的文件中。
- 声明式渲染是vue的核心功能，通过扩展于标准 HTML 的模板语法，我们可以根据 JavaScript 的状态来描述 HTML 应该是什么样子的。当状态改变时，HTML 会自动更新。
- ref()和reactive()
    - [响应式基础 | Vue.js](https://cn.vuejs.org/guide/essentials/reactivity-fundamentals)
- 在组件的 `<script setup>` 块中声明的响应式状态，可以直接在模板中使用。下面展示了双花括号语法（mustache 语法）的使用，根据 `counter` 对象和 `message` ref 的值渲染动态文本：
    
    ```html
    <h1>{{ message }}</h1>
    <p>Count is: {{ counter.count }}</p>
    ```
    
    注意我们在模板中访问的 `message` ref 时不需要使用 `.value`：它会被自动解包，让使用更简单。
    
    在双花括号中的内容并不只限于标识符或路径——我们可以使用任何有效的 JavaScript 表达式。
    
    ```html
    <h1>{{ message.split('').reverse().join('') }}</h1>
    ```
    

![image.png](/img/user/03_Vue/vue学习-基础/image 1.png)

## 2. Attribute绑定

- [模板语法 | Vue.js](https://cn.vuejs.org/guide/essentials/template-syntax)
- 在 Vue 中，mustache 语法 (即双大括号) 只能用于文本插值。为了给属性attribute 绑定一个动态值，需要使用 `v-bind` 指令：

```html
<div v-bind:id="dynamicId"></div>
```

        冒号后面的部分 (`:id`) 是指令的“参数”。此处，元素的 `id` attribute 将与组件状态里的 `dynamicId` 属性保持同步。

        由于 `v-bind` 使用地非常频繁，它有一个专门的简写语法：

```html
<div :id="dynamicId"></div>
```

- **指令**是由 `v-` 开头的一种特殊 attribute。它们是 Vue 模板语法的一部分。和文本插值类似，指令的值是可以访问组件状态的 JavaScript 表达式。

![image.png](/img/user/03_Vue/vue学习-基础/image 2.png)

## 3.事件监听

- [事件处理 | Vue.js](https://cn.vuejs.org/guide/essentials/event-handling)
- 我们可以使用 `v-on` 指令监听 DOM 事件：

```html
<button v-on:click="increment">{{ count }}</button>
```

        因为其经常使用，`v-on` 也有一个简写语法：

```html

<button @click="increment">{{ count }}</button>
```

此处，`increment` 引用了一个在 `<script setup>` 中声明的函数

- 事件处理函数也可以使用内置表达式，并且可以使用修饰符简化常见任务。这些细节包含在[**指南 - 事件处理**](https://cn.vuejs.org/guide/essentials/event-handling.html)。
- 事件处理器 (handler) 的值可以是：
1. **内联事件处理器**：事件被触发时执行的内联 JavaScript 语句 (与 `onclick` 类似)。
2. **方法事件处理器**：一个指向组件上定义的方法的属性名或是路径。

![事件监听.gif](/img/user/03_Vue/vue学习-基础/事件监听.gif)

### **事件修饰符[​](https://cn.vuejs.org/guide/essentials/event-handling#event-modifiers)**

在处理事件时调用 `event.preventDefault()` 或 `event.stopPropagation()` 是很常见的。尽管我们可以直接在方法内调用，但如果方法能更专注于数据逻辑而不用去处理 DOM 事件的细节会更好。

为解决这一问题，Vue 为 `v-on` 提供了**事件修饰符**。修饰符是用 `.` 表示的指令后缀，包含以下这些：

- `.stop`
- `.prevent`
- `.self`
- `.capture`
- `.once`
- `.passive`

```html
<!-- 单击事件将停止传递 -->
<a @click.stop="doThis"></a><!-- 提交事件将不再重新加载页面 -->
<form @submit.prevent="onSubmit"></form><!-- 修饰语可以使用链式书写 -->
<a @click.stop.prevent="doThat"></a><!-- 也可以只有修饰符 -->
<form @submit.prevent></form><!-- 仅当 event.target 是元素本身时才会触发事件处理器 -->
<!-- 例如：事件处理器不来自子元素 -->
<div @click.self="doThat">...</div>
```

**TIP
使用修饰符时需要注意调用顺序，因为相关代码是以相同的顺序生成的。因此使用 `@click.prevent.self` 会阻止元素及其子元素的所有点击事件的默认行为，而 `@click.self.prevent` 则只会阻止对元素本身的点击事件的默认行为。**

`.capture`、`.once` 和 `.passive` 修饰符与[**原生 `addEventListener` 事件**](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener#options)相对应：

```html
<!-- 添加事件监听器时，使用 `capture` 捕获模式 -->
<!-- 例如：指向内部元素的事件，在被内部元素处理前，先被外部处理 -->
<div @click.capture="doThis">...</div><!-- 点击事件最多被触发一次 -->
<a @click.once="doThis"></a>
<!-- 滚动事件的默认行为 (scrolling) 将立即发生而非等待 `onScroll` 完成 -->
<!-- 以防其中包含 `event.preventDefault()` -->
<div @scroll.passive="onScroll">...</div>
```

`.passive` 修饰符一般用于触摸事件的监听器，可以用来[**改善移动端设备的滚屏性能**](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener#%E4%BD%BF%E7%94%A8_passive_%E6%94%B9%E5%96%84%E6%BB%9A%E5%B1%8F%E6%80%A7%E8%83%BD)。

**TIP
请勿同时使用 `.passive` 和 `.prevent`，因为 `.passive` 已经向浏览器表明了你*不想*阻止事件的默认行为。如果你这么做了，则 `.prevent` 会被忽略，并且浏览器会抛出警告。**

### **按键修饰符[​](https://cn.vuejs.org/guide/essentials/event-handling#key-modifiers)**

在监听键盘事件时，我们经常需要检查特定的按键。Vue 允许在 `v-on` 或 `@` 监听按键事件时添加按键修饰符。

```html
<!-- 仅在 `key` 为 `Enter` 时调用 `submit` -->
<input @keyup.enter="submit" />
```

你可以直接使用 [**`KeyboardEvent.key`**](https://developer.mozilla.org/zh-CN/docs/Web/API/UI_Events/Keyboard_event_key_values) 暴露的按键名称作为修饰符，但需要转为 kebab-case 形式。

```html
<input @keyup.page-down="onPageDown" />
```

在上面的例子中，仅会在 `$event.key` 为 `'PageDown'` 时调用事件处理。

### **按键别名[​](https://cn.vuejs.org/guide/essentials/event-handling#key-aliases)**

Vue 为一些常用的按键提供了别名：

- `.enter`
- `.tab`
- `.delete` (捕获“Delete”和“Backspace”两个按键)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

### **系统按键修饰符[​](https://cn.vuejs.org/guide/essentials/event-handling#system-modifier-keys)**

你可以使用以下系统按键修饰符来触发鼠标或键盘事件监听器，只有当按键被按下时才会触发。

- `.ctrl`
- `.alt`
- `.shift`
- `.meta`

**注意
在 Mac 键盘上，meta 是 Command 键 (⌘)。在 Windows 键盘上，meta 键是 Windows 键 (⊞)。在 Sun 微机系统键盘上，meta 是钻石键 (◆)。在某些键盘上，特别是 MIT 和 Lisp 机器的键盘及其后代版本的键盘，如 Knight 键盘，space-cadet 键盘，meta 都被标记为“META”。在 Symbolics 键盘上，meta 也被标识为“META”或“Meta”。**

举例来说：

```html
<!-- Alt + Enter -->
<input @keyup.alt.enter="clear" />
<!-- Ctrl + 点击 -->
<div @click.ctrl="doSomething">Do something</div>
```

**TIP
请注意，系统按键修饰符和常规按键不同。与 `keyup` 事件一起使用时，该按键必须在事件发出时处于按下状态。换句话说，`keyup.ctrl` 只会在你仍然按住 `ctrl` 但松开了另一个键时被触发。若你单独松开 `ctrl` 键将不会触发。**

### **`.exact` 修饰符[​](https://cn.vuejs.org/guide/essentials/event-handling#exact-modifier)**

`.exact` 修饰符允许精确控制触发事件所需的系统修饰符的组合。

```html
<!-- 当按下 Ctrl 时，即使同时按下 Alt 或 Shift 也会触发 -->
<button @click.ctrl="onClick">A</button>
<!-- 仅当按下 Ctrl 且未按任何其他键时才会触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>
<!-- 仅当没有按下任何系统按键时触发 -->
<button @click.exact="onClick">A</button>
```

### **鼠标按键修饰符[​](https://cn.vuejs.org/guide/essentials/event-handling#mouse-button-modifiers)**

- `.left`
- `.right`
- `.middle`

这些修饰符将处理程序限定为由特定鼠标按键触发的事件。

但请注意，`.left`，`.right` 和 `.middle` 这些修饰符名称是基于常见的右手用鼠标布局设定的，但实际上它们分别指代设备事件触发器的“主”、”次“，“辅助”，而非实际的物理按键。因此，对于左手用鼠标布局而言，“主”按键在物理上可能是右边的按键，但却会触发 `.left` 修饰符对应的处理程序。又或者，触控板可能通过单指点击触发 `.left` 处理程序，通过双指点击触发 `.right` 处理程序，通过三指点击触发 `.middle` 处理程序。同样，产生“鼠标”事件的其他设备和事件源，也可能具有与“左”，“右”完全无关的触发模式。

## 4. 表单绑定

- 我们可以同时使用 `v-bind` 和 `v-on` 来在表单的输入元素上创建双向绑定：

```html
<input :value="text" @input="onInput">
```

```jsx
function onInput(e) {  // v-on 处理函数会接收原生 DOM 事件  // 作为其参数。  text.value = e.target.value}
```

试着在文本框里输入——你会看到 `<p>` 里的文本也随着你的输入更新了。

- 为了简化双向绑定，Vue 提供了一个 `v-model` 指令，它实际上是上述操作的语法糖：

```jsx
<input v-model="text">
```

`v-model` 会将被绑定的值与 `<input>` 的值自动同步，这样我们就不必再使用事件处理函数了。

`v-model` 不仅支持文本输入框，也支持诸如**多选框、单选框、下拉框**之类的输入类型。我们在[**指南 - 表单绑定**](https://cn.vuejs.org/guide/essentials/forms.html)中讨论了更多的细节。

![表单绑定.gif](/img/user/03_Vue/vue学习-基础/表单绑定.gif)

## 5. 条件渲染

- 我们可以使用 `v-if` 指令来有条件地渲染元素：

```html
<h1 v-if="awesome">Vue is awesome!</h1>
```

这个 `<h1>` 标签只会在 `awesome` 的值为[**真值 (Truthy)**](https://developer.mozilla.org/zh-CN/docs/Glossary/Truthy) 时渲染。若 `awesome` 更改为[**假值 (Falsy)**](https://developer.mozilla.org/zh-CN/docs/Glossary/Falsy)，它将被从 DOM 中移除。

我们也可以使用 `v-else` 和 `v-else-if` 来表示其他的条件分支：

```html
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```

- 更多细节请查阅 `v-if`：[**指南 - 条件渲染**](https://cn.vuejs.org/guide/essentials/conditional.html)

![动画.gif](/img/user/03_Vue/vue学习-基础/动画.gif)

## 6. 列表渲染

- 我们可以使用 `v-for` 指令来渲染一个基于源数组的列表：
    
    ```html
    <ul>  <li v-for="todo in todos" :key="todo.id">    {{ todo.text }}  </li></ul>
    ```
    
    这里的 `todo` 是一个局部变量，表示当前正在迭代的数组元素。它只能在 `v-for` 所绑定的元素上或是其内部访问，就像函数的作用域一样。
    
    注意，我们还给每个 todo 对象设置了唯一的 `id`，并且将它作为[**特殊的 `key` attribute**](https://cn.vuejs.org/api/built-in-special-attributes.html#key) 绑定到每个 `<li>`。`key` 使得 Vue 能够精确地移动每个 `<li>`，以匹配对应的对象在数组中的位置。
    
- 更新列表有两种方式：
    1. 在源数组上调用[**变更方法**](https://stackoverflow.com/questions/9009879/which-javascript-array-functions-are-mutating)：
        
        ```jsx
        todos.value.push(newTodo)
        ```
        
    2. 使用新的数组替代原数组：
        
        ```jsx
        todos.value = todos.value.filter(/* ... */)
        ```
        

这里是一个简单的 todo 列表

![列表渲染.gif](/img/user/03_Vue/vue学习-基础/列表渲染.gif)

## 7. 计算属性

- 介绍一个新 API：[**`computed()`**](https://cn.vuejs.org/guide/essentials/computed.html)。它可以让我们创建一个计算属性 ref，这个 ref 会动态地根据其他响应式数据源来计算其 `.value`：

```jsx
import { ref, computed } from 'vue'
const hideCompleted = ref(false)
const todos = ref([  /* ... */])
const filteredTodos = computed(() => {  
// 根据 `todos.value` & `hideCompleted.value`  // 返回过滤后的 todo 项目
})
```

```diff
- <li v-for="todo in todos">
+ <li v-for="todo in filteredTodos">
```

计算属性会自动跟踪其计算中所使用的到的其他响应式状态，并将它们收集为自己的依赖。计算结果会被缓存，并只有在其依赖发生改变时才会被自动更新。

![计算属性.gif](/img/user/03_Vue/vue学习-基础/计算属性.gif)

## 8. 生命周期和模板引用

- 有时我们也会不可避免地需要手动操作 DOM。
    
    这时我们需要使用**模板引用**——也就是指向模板中一个 DOM 元素的 ref。我们需要通过[**这个特殊的 `ref` attribute**](https://cn.vuejs.org/api/built-in-special-attributes.html#ref) 来实现模板引用：
    
    ```html
    <p ref="pElementRef">hello</p>
    ```
    
    要访问该引用，我们需要声明一个同名的 ref：
    
    ```jsx
    const pElementRef = ref(null)
    ```
    
    注意这个 ref 使用 `null` 值来初始化。这是因为当 `<script setup>` 执行时，DOM 元素还不存在。模板引用 ref 只能在组件**挂载**后访问。
    
- 要在挂载之后执行代码，我们可以使用 `onMounted()` 函数：
    
    ```jsx
    import { onMounted } from 'vue'onMounted(() => {  // 此时组件已经挂载。})
    ```
    
    这被称为**生命周期钩子**——它允许我们注册一个在组件的特定生命周期调用的回调函数。还有一些其他的钩子如 `onUpdated` 和 `onUnmounted`。更多细节请查阅[**生命周期图示**](https://cn.vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram)。
    
    ![生命周期和模板引用.gif](/img/user/03_Vue/vue学习-基础/生命周期和模板引用.gif)
    

## 9. 侦听器

- 有时我们需要响应性地执行一些“副作用”——例如，当一个数字改变时将其输出到控制台。我们可以通过侦听器来实现它：
    
    ```jsx
    import { ref, watch } from 'vue'const count = ref(0)watch(count, (newCount) => {  // 没错，console.log() 是一个副作用  console.log(`new count is: ${newCount}`)})
    ```
    
    `watch()` 可以直接侦听一个 ref，并且只要 `count` 的值改变就会触发回调。`watch()` 也可以侦听其他类型的数据源——更多详情请参阅[**指南 - 侦听器**](https://cn.vuejs.org/guide/essentials/watchers.html)。
    
    一个比在控制台输出更加实际的例子是当 ID 改变时抓取新的数据。在右边的例子中就是这样一个组件。该组件被挂载时，会从模拟 API 中抓取 todo 数据，同时还有一个按钮可以改变要抓取的 todo 的 ID。现在，尝试实现一个侦听器，使得组件能够在按钮被点击时抓取新的 todo 项目。
    
    ![侦听器.gif](/img/user/03_Vue/vue学习-基础/侦听器.gif)
    

## 10. 组件

- 目前为止，我们只使用了单个组件。真正的 Vue 应用往往是由嵌套组件创建的。
    
    父组件可以在模板中渲染另一个组件作为子组件。要使用子组件，我们需要先导入它：
    
    ```jsx
    import ChildComp from './ChildComp.vue'
    ```
    
    然后我们就可以在模板中使用组件，就像这样：
    
    ```html
    <ChildComp />
    ```
    
- 现在——导入子组件并在模板中渲染它。
    
    ![组件.gif](/img/user/03_Vue/vue学习-基础/组件.gif)
    

## 11. Props

- 子组件可以通过 **props** 从父组件接受动态数据。首先，需要声明它所接受的 props：
    
    ```jsx
    <!-- ChildComp.vue -->
    <script setup>
    const props = defineProps({  msg: String})
    </script>
    ```
    

注意 `defineProps()` 是一个编译时宏，并不需要导入。一旦声明，`msg` prop 就可以在子组件的模板中使用。它也可以通过 `defineProps()` 所返回的对象在 JavaScript 中访问。

父组件可以像声明 HTML attributes 一样传递 props。若要传递动态值，也可以使用 `v-bind` 语法：

```jsx
<ChildComp :msg="greeting" />
```

![image.png](/img/user/03_Vue/vue学习-基础/image 3.png)

## 12. Emits

- 除了接收 props，子组件还可以向父组件触发事件：
    
    ```html
    <script setup>
    // 声明触发的事件
    const emit = defineEmits(['response'])
    // 带参数触发
    emit('response', 'hello from child')
    </script>
    ```
    
    `emit()` 的第一个参数是事件的名称。其他所有参数都将传递给事件监听器。
    
    父组件可以使用 `v-on` 监听子组件触发的事件——这里的处理函数接收了子组件触发事件时的额外参数并将它赋值给了本地状态：
    
    ```html
    <ChildComp @response="(msg) => childMsg = msg" />
    ```
    
    - `<ChildComp>`：子组件的标签。
    - `@response`：监听子组件触发的名为 `response` 的自定义事件。
    - `(msg) => childMsg = msg`：事件处理函数，当子组件触发 `response` 事件时：
        - `msg`：子组件传递的事件参数。
        - 将 `msg` 赋值给父组件的响应式变量 `childMsg`。
    
    ![image.png](/img/user/03_Vue/vue学习-基础/image 4.png)
    
    在子组件使用 `defineEmits` 定义事件类型（可选类型检查）
    
    在子组件的方法中调用 `emit('response', payload)` 发送事件
    
    • **`@click="$emit('close')"`**：当按钮被点击时，触发 `close` 事件，通知父组件关闭模态框。
    
    ![image.png](/img/user/03_Vue/vue学习-基础/image 5.png)
    

## 13. 插槽

- 除了通过 props 传递数据外，父组件还可以通过**插槽** (slots) 将模板片段传递给子组件：

```html
<ChildComp>  This is some slot content!</ChildComp>
```

在子组件中，可以使用 `<slot>` 元素作为插槽出口 (slot outlet) 渲染父组件中的插槽内容 (slot content)：

```html
<!-- 在子组件的模板中 -->
<slot/>
```

`<slot>` 插口中的内容将被当作“默认”内容：它会在父组件没有传递任何插槽内容时显示：

```html
<slot>Fallback content</slot>
```

现在我们没有给 `<ChildComp>` 传递任何插槽内容，所以你将看到默认内容。让我们利用父组件的 `msg` 状态为子组件提供一些插槽内容吧。

![插槽slot.gif](/img/user/03_Vue/vue学习-基础/插槽slot.gif)

### v-slot

总结来说，回答需要涵盖v-slot的定义、用途、不同用法（默认、具名、作用域）、示例代码以及版本差异，同时用简单易懂的语言解释，避免过于技术化的术语，帮助用户快速掌握这一概念。

`v-slot` 是 Vue.js 中用于定义**组件插槽**的指令，它允许你在父组件中向子组件插入自定义内容，实现组件的灵活复用和内容分发。以下是它的核心概念和用法：

---

### 1. **默认插槽 (Default Slot)**

通过 `v-slot` 定义默认插槽内容：

```html
<!-- 子组件 ChildComponent.vue -->
<template>
  <div class="child">
    <slot>默认内容</slot> <!-- 默认显示的内容 -->
  </div>
</template>

<!-- 父组件 ParentComponent.vue -->
<template>
  <ChildComponent>
    <p>这是自定义的插槽内容！</p> <!-- 会覆盖默认内容 -->
  </ChildComponent>
</template>

```

---

### 2. **具名插槽 (Named Slots)**

为插槽命名，实现多个独立插槽：

```html
<!-- 子组件 ChildComponent.vue -->
<template>
  <div>
    <header slot="header">头部内容</header>
    <main slot="main">主体内容</main>
    <footer slot="footer">底部内容</footer>
  </div>
</template>

<!-- 父组件 ParentComponent.vue -->
<template>
  <ChildComponent>
    <template #header>
      <h1>自定义标题</h1>
    </template>

    <template #main>
      <p>这里是主体区域</p>
    </template>
  </ChildComponent>
</template>

```

---

### 3. **作用域插槽 (Scoped Slots)**

子组件向父组件传递数据，父组件通过插槽接收并渲染：

```html
<!-- 子组件 ChildComponent.vue -->
<template>
  <ul>
    <li v-for="item in items" :key="item.id">
      <slot :item="item" name="itemSlot">{{ item.text }}</slot>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return { items: [{ id: 1, text: '苹果' }, { id: 2, text: '香蕉' }] };
  }
};
</script>

<!-- 父组件 ParentComponent.vue -->
<template>
  <ChildComponent>
    <template #itemSlot="{ item }">
      <strong>{{ item.text }}</strong>（价格：¥{{ item.price }}）
    </template>
  </ChildComponent>
</template>

```

---

### 关键语法

| 语法 | 作用 |
| --- | --- |
| `v-slot:default` | 定义默认插槽（可简写为 `v-slot`） |
| `v-slot:name` | 定义具名插槽 |
| `v-slot:default="slotProps"` | 获取作用域插槽的数据 |

---

### 注意事项

1. **版本差异**：
• Vue 2 中使用 `slot` 和 `slot-scope`，Vue 3 统一使用 `v-slot`。
2. **必须直接包裹内容**：插槽内容需直接写在子组件标签内，不能有其他元素嵌套。
3. **向子组件传递数据**：通过 `v-bind` 或简写 `:` 将数据绑定到插槽参数。

---

### 实际场景

- **UI 组件库**：如按钮、模态框等允许用户自定义内部内容的组件。
• **列表渲染**：复用列表项模板，动态传递数据。
• **表单构建**：生成动态表单字段，通过插槽插入自定义输入组件。

掌握 `v-slot` 能显著提升组件的灵活性和可维护性！如果有具体场景，可以进一步探讨用法~

| computed | 计算属性 |  |
| --- | --- | --- |
| onMounted | 生命周期钩子 | [生命周期钩子 | Vue.js](https://cn.vuejs.org/guide/essentials/lifecycle#registering-lifecycle-hooks) |
| watch | 侦听器 |  |

# 四、实践教程

https://cn.vuejs.org/examples/#handling-input