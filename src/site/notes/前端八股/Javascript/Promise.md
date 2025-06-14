---
{"dg-publish":true,"permalink":"/前端八股/Javascript/Promise/"}
---

## 对Promise的理解

> [!NOTE]
> Promise 对象是异步编程的一种解决方案，最早由社区提出。Promise 是一个构造函数，接收一个函数作为参数，返回一个 Promise 实例。一个 Promise 实例有三种状态，分别是pending、resolved 和 rejected，分别代表了进行中、已成功和已失败。实例的状态只能由 pending 转变 resolved 或者rejected 状态，并且状态一经改变，就凝固了，无法再被改变了。

Promise是异步编程的一种解决方案，它是一个对象，可以获取异步操作的消息，他的出现大大改善了异步编程的困境，避免了地狱回调，它比传统的解决方案回调函数和事件更合理和更强大。

所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

（1）Promise的实例有**三个状态**:  

- Pending（进行中）
- Resolved（已完成）
- Rejected（已拒绝）

当把一件事情交给promise时，它的状态就是Pending，任务完成了状态就变成了Resolved、没有完成失败了就变成了Rejected。  

（2）Promise的实例有**两个过程**：  

- pending -> fulfilled : Resolved（已完成）
- pending -> rejected：Rejected（已拒绝）

注意：一旦从进行状态变成为其他状态就永远不能更改状态了。  

## **Promise的特点：**  

- 对象的状态不受外界影响。promise对象代表一个异步操作，有三种状态，​`pending`​（进行中）、​`fulfilled`​（已成功）、​`rejected`​（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态，这也是promise这个名字的由来——“**承诺**”；
- 一旦状态改变就不会再变，任何时候都可以得到这个结果。promise对象的状态改变，只有两种可能：从 ​`pending`​变为 ​`fulfilled`​，从 ​`pending`​变为 ​`rejected`​。这时就称为 ​`resolved`​（已定型）。如果改变已经发生了，你再对promise对象添加回调函数，也会立即得到这个结果。这与事件（event）完全不同，事件的特点是：如果你错过了它，再去监听是得不到结果的。

**Promise的缺点：**  

- 无法取消Promise，一旦新建它就会立即执行，无法中途取消。
- 如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。
- 当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

状态的改变是通过 resolve() 和 reject() 函数来实现的，可以在异步操作结束后调用这两个函数改变 Promise 实例的状态，它的原型上定义了一个 then 方法，使用这个 then 方法可以为两个状态的改变注册回调函数。这个回调函数属于微任务，会在本轮事件循环的末尾执行。

**注意：**在构造 `Promise` 的时候，构造函数内部的代码是立即执行的  

#### promise和settimeout的相同点和不同

在面试中被问到 **Promise 和 setTimeout 的相同点与不同点**，可以从**用途、异步机制、执行时机、优先级**等方面来回答，体现你对 JavaScript 事件循环的理解。以下是一份高质量、条理清晰的口头回答模板：

---

### ✅ 面试口头回答模板：

> Promise 和 setTimeout 都是用来处理**异步任务**的机制，但它们的本质和执行时机不同。可以从以下几个方面来比较：

#### ✅ 相同点：

1. **都是异步执行**
    
    - 它们不会阻塞主线程，任务会被推迟到当前执行栈清空之后再执行。
        
2. **都可以通过回调来处理结果**
    
    - `setTimeout(fn, 0)` 用回调函数处理；
        
    - `Promise.then()` 则用链式写法处理异步结果。
        

---

#### ❌ 不同点：

1. **本质区别：**
    
    - `setTimeout` 是 **基于定时器的宏任务（macro task）**；
        
    - `Promise.then()` 是 **微任务（micro task）**，是 ES6 引入的更现代、更高效的异步方案。
        
2. **执行时机不同：**
    
    - 微任务（如 Promise）会在**当前宏任务结束后，立即执行**；
        
    - 宏任务（如 setTimeout）则会在所有微任务执行完之后才执行。
        
    - 所以：
        
        ```js
        Promise.resolve().then(() => console.log('promise'));
        setTimeout(() => console.log('timeout'), 0);
        // 输出顺序：'promise' -> 'timeout'
        ```
        
3. **控制粒度不同：**
    
    - `setTimeout` 只能通过时间控制异步逻辑，不适合链式复杂异步场景；
        
    - `Promise` 支持链式调用、错误捕获（`.catch()`），更适合组织多个异步任务。
        
4. **用途不同：**
    
    - `setTimeout` 更像是定时调度；
        
    - `Promise` 更适合处理**异步逻辑流程控制**，比如异步请求、文件操作等。
        

---

### 🎯 总结语句：

> 总的来说，`Promise` 是现代异步编程的核心，提供更强的语义和控制能力，而 `setTimeout` 更偏向基础的时间控制。它们都属于事件循环的一部分，但 Promise 属于微任务，优先级比 setTimeout 更高。

---

如果你还需要我补充一段**带输出顺序的示例代码 + 图示说明事件循环执行过程**，也可以告诉我。
### 4. Promise的基本用法

#### （1）创建Promise对象

Promise对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）。  

Promise构造函数接受一个函数作为参数，该函数的两个参数分别是 `resolve`和 `reject`。

``` js
const promise = new Promise(function(resolve, reject) {
  // ... some code
  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

**一般情况下都会使用** `new Promise()`**来创建promise对象，但是也可以使用** `promise.resolve`**和** `promise.reject`**这两个方法：**  

- Promise.resolve

`Promise.resolve(value)`的返回值也是一个promise对象，可以对返回值进行.then调用，代码如下：

``` js
Promise.resolve(11).then(function(value){
  console.log(value); // 打印出11
});
```

`resolve(11)`代码中，会让promise对象进入确定(`resolve`状态)，并将参数 `11`传递给后面的 `then`所指定的 `onFulfilled` 函数；  

创建promise对象可以使用 `new Promise`的形式创建对象，也可以使用 `Promise.resolve(value)`的形式创建promise对象；  

- Promise.reject

`Promise.reject` 也是 `new Promise`的快捷形式，也创建一个promise对象。代码如下：

``` js
Promise.reject(new Error(“我错了，请原谅俺！！”));
```

就是下面的代码new Promise的简单形式：

``` js
new Promise(function(resolve,reject){
   reject(new Error("我错了，请原谅俺！！"));
});
```

下面是使用resolve方法和reject方法：

``` js 
function testPromise(ready) {
  return new Promise(function(resolve,reject){
    if(ready) {
      resolve("hello world");
    }else {
      reject("No thanks");
    }
  });
};
// 方法调用
testPromise(true).then(function(msg){
  console.log(msg);
},function(error){
  console.log(error);
});
```

上面的代码的含义是给 `testPromise`方法传递一个参数，返回一个promise对象，如果为 `true`的话，那么调用promise对象中的 `resolve()`方法，并且把其中的参数传递给后面的 `then`第一个函数内，因此打印出 “`hello world`”, 如果为 `false`的话，会调用promise对象中的 `reject()`方法，则会进入 `then`的第二个函数内，会打印 `No thanks`；  

#### （2）Promise方法

Promise有五个常用的方法：then()、catch()、all()、race()、finally。下面就来看一下这些方法。  

- then()

当Promise执行的内容符合成功条件时，调用 `resolve`函数，失败就调用 `reject`函数。Promise创建完了，那该如何调用呢？

``` js
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```

`then`方法可以接受两个回调函数作为参数。第一个回调函数是Promise对象的状态变为 `resolved`时调用，第二个回调函数是Promise对象的状态变为 `rejected`时调用。其中第二个参数可以省略。  

`then`方法返回的是一个新的Promise实例（不是原来那个Promise实例）。因此可以采用链式写法，即 `then`方法后面再调用另一个then方法。  

当要写有顺序的异步事件时，需要串行时，可以这样写：

``` js
let promise = new Promise((resolve,reject)=>{
    ajax('first').success(function(res){
        resolve(res);
    })
})
promise.then(res=>{
    return new Promise((resovle,reject)=>{
        ajax('second').success(function(res){
            resolve(res)
        })
    })
}).then(res=>{
    return new Promise((resovle,reject)=>{
        ajax('second').success(function(res){
            resolve(res)
        })
    })
}).then(res=>{
  
})
```

那当要写的事件没有顺序或者关系时，还如何写呢？可以使用 `all` 方法来解决。  

- catch()

Promise对象除了有then方法，还有一个catch方法，该方法相当于 `then`方法的第二个参数，指向 `reject`的回调函数。不过 `catch`方法还有一个作用，就是在执行 `resolve`回调函数时，如果出现错误，抛出异常，不会停止运行，而是进入 `catch`方法中。

``` js
p.then((data) => {
     console.log('resolved',data);
},(err) => {
     console.log('rejected',err);
     }
); 
p.then((data) => {
    console.log('resolved',data);
}).catch((err) => {
    console.log('rejected',err);
});
```

- all()

`all`方法可以完成并行任务， 它接收一个数组，数组的每一项都是一个 `promise`对象。当数组中所有的 `promise`的状态都达到 `resolved`的时候，`all`方法的状态就会变成 `resolved`，如果有一个状态变成了 `rejected`，那么 `all`方法的状态就会变成 `rejected`。

``` js
javascript
let promise1 = new Promise((resolve,reject)=>{
    setTimeout(()=>{
       resolve(1);
    },2000)
});
let promise2 = new Promise((resolve,reject)=>{
    setTimeout(()=>{
       resolve(2);
    },1000)
});
let promise3 = new Promise((resolve,reject)=>{
    setTimeout(()=>{
       resolve(3);
    },3000)
});
Promise.all([promise1,promise2,promise3]).then(res=>{
    console.log(res);
    //结果为：[1,2,3] 
})
function all(promises){
  return new Promise((resolve,reject) => {
    let lens = promises.length;
    let count = 0;
    let res = [];
    for(let i = 0; i < lens; i++){
      promises[i].then(val => {
        count++;
        res.push(val);
        if(count === lens){
          resolve(res)
        }
      }).catch(error => {
        reject(error)
      })
    }
  })
}
```

调用 `all`方法时的结果成功的时候是回调函数的参数也是一个数组，这个数组按顺序保存着每一个promise对象 `resolve`执行时的值。  

- race()

`race`方法和 `all`一样，接受的参数是一个每项都是 `promise`的数组，但是与 `all`不同的是，当最先执行完的事件执行完之后，就直接返回该 `promise`对象的值。如果第一个 `promise`对象状态变成 `resolved`，那自身的状态变成了 `resolved`；反之第一个 `promise`变成 `rejected`，那自身状态就会变成 `rejected`。

``` js
let promise1 = new Promise((resolve,reject)=>{
    setTimeout(()=>{
       reject(1);
    },2000)
});
let promise2 = new Promise((resolve,reject)=>{
    setTimeout(()=>{
       resolve(2);
    },1000)
});
let promise3 = new Promise((resolve,reject)=>{
    setTimeout(()=>{
       resolve(3);
    },3000)
});
Promise.race([promise1,promise2,promise3]).then(res=>{
    console.log(res);
    //结果：2
},rej=>{
    console.log(rej)};
)
```

那么 `race`方法有什么实际作用呢？当要做一件事，超过多长时间就不做了，可以用这个方法来解决：

``` js
Promise.race([promise1,timeOutPromise(5000)]).then(res=>{})
```

- finally()

`finally`方法用于指定不管 Promise 对象最后状态如何，都会执行的操作。该方法是 ES2018 引入标准的。

``` js
promise
.then(result => {···})
.catch(error => {···})
.finally(() => {···});
```

上面代码中，不管 `promise`最后的状态，在执行完 `then`或 `catch`指定的回调函数以后，都会执行 `finally`方法指定的回调函数。  

下面是一个例子，服务器使用 Promise 处理请求，然后使用 `finally`方法关掉服务器。

``` js
server.listen(port)
  .then(function () {
    // ...
  })
  .finally(server.stop);
```

`finally`方法的回调函数不接受任何参数，这意味着没有办法知道，前面的 Promise 状态到底是 `fulfilled`还是 `rejected`。这表明，`finally`方法里面的操作，应该是与状态无关的，不依赖于 Promise 的执行结果。`finally`本质上是 `then`方法的特例：

``` js
promise
.finally(() => {
  // 语句
});
// 等同于
promise
.then(
  result => {
    // 语句
    return result;
  },
  error => {
    // 语句
    throw error;
  }
);
```

上面代码中，如果不使用 `finally`方法，同样的语句需要为成功和失败两种情况各写一次。有了 `finally`方法，则只需要写一次。  

### 5. Promise解决了什么问题

在工作中经常会碰到这样一个需求，比如我使用ajax发一个A请求后，成功后拿到数据，需要把数据传给B请求；那么需要如下编写代码：

``` js
let fs = require('fs')
fs.readFile('./a.txt','utf8',function(err,data){
  fs.readFile(data,'utf8',function(err,data){
    fs.readFile(data,'utf8',function(err,data){
      console.log(data)
    })
  })
})
```

上面的代码有如下缺点：  

- 后一个请求需要依赖于前一个请求成功后，将数据往下传递，会导致多个ajax请求嵌套的情况，代码不够直观。
- 如果前后两个请求不需要传递参数的情况下，那么后一个请求也需要前一个请求成功后再执行下一步操作，这种情况下，那么也需要如上编写代码，导致代码不够直观。

`Promise`出现之后，代码变成这样：

``` js
let fs = require('fs')
function read(url){
  return new Promise((resolve,reject)=>{
    fs.readFile(url,'utf8',function(error,data){
      error && reject(error)
      resolve(data)
    })
  })
}
read('./a.txt').then(data=>{
  return read(data) 
}).then(data=>{
  return read(data)  
}).then(data=>{
  console.log(data)
})
```

这样代码看起了就简洁了很多，解决了地狱回调的问题。  
