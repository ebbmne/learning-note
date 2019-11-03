### 回调函数

#### 定义

回调函数：特定的事件或条件发生时由另外的一方调用的，用于对该事件或条件进行响应

#### 同步回调函数

理解：立即执行，完全执行了才结束，不会放入回调队列中

例子：forEach中的回调函数，Promise的excutor函数

#### 异步回调函数

理解：不会立即执行，会放入回调队列中将来执行

例子：定时器的回调，ajax回调，Promise的成功/失败的回调

--------------------------------------------------

### Promise定义

#### 抽象表达
Promise是JS中进行异步编程的解决方案

> JS中进行异步编程的解决方案有四种：纯回调，Promise，generator，async/await

#### 具体来说

从语法上来说：Promise是一个构造函数
从功能上来说：Promise对象用来封装一个异步操作并可以获取其结果

-----------------------------------------------------

### 为什么需要Promise

| 使用纯回调                           | 使用Promise                                            |
| ------------------------------------ | ------------------------------------------------------ |
| 回调地狱，代码难以阅读，异常难以处理 | 链式调用，代码易于阅读，异常易于捕获和处理             |
| 回调函数在异步操作执行前必须先定义好 | 回调函数定义的时间更加灵活，可以在异步操作结束后再定义 |

-----------------------------------------------------

### Promise状态

#### Promise有三种状态

| 状态     | 说明             |
| -------- | ---------------- |
| pending  | 异步操作执行中   |
| resolved | 异步操作执行成功 |
| rejected | 异步操作执行失败 |

#### Promise状态改变

状态改变只有两种，且一个Promise只能改变一次

* pending -> resolved

* pending -> rejected

------------------------------------------------------

### Promise结果

异步操作无论成功还是失败，Promise都会有一个结果

成功的结果记为value，失败的结果记为reason

-------------------------------

### Promise API

#### 构造函数

##### 参数：执行器函数

执行器函数的结构如下

```js
(resolve, reject) => { 
  // 执行异步操作
  if (异步操作成功) {
    resolve(成功结果);
  } else if (异步操作失败) {
    reject(失败结果);
  }
}
```

执行器函数中执行异步操作，定义时立即执行

`resolve`用于改变Promise对象状态为`resolved`，同时保存成功结果到Promise对象中

`reject`用于改变Promise对象状态为`rejected`，同时保存失败结果到Promise对象中

##### 返回值：一个Promise对象

#### Promise.prototype.then

##### 参数：成功的回调函数和失败的回调函数

```js
const p = new Promise();
p.then(value => {}, reason => {});
```

##### 返回值：一个新的Promise对象

#### Promise.prototype.catch

##### 参数：失败的回调函数

```js
const p = new Promise();
p.catch(reason => {});
```

##### 返回值：一个新的Promise对象

##### 本质：then的语法糖

```js
p.then(undefined, reason => {});
```

#### Promise.resolve

##### 参数：成功的结果

##### 返回值：一个新的Promise对象，其状态为resolved，结果为传入的参数

##### 本质：语法糖

```js
const p = Promise.resolve(value);
// 等价于
const p = new Promise((resolve, reject) => {
  resolve(value);
});
```

#### Promise.reject

##### 参数：失败的结果

##### 返回值：一个新的Promise对象，其状态为resolved，结果为传入的参数

##### 本质：语法糖

```js
const p = Promise.reject(reason);
// 等价于
const p = new Promise((resolve, reject) => {
  reject(reason);
});
```

#### Promise.all

##### 参数：一个装有Promise对象的数组

##### 返回值：返回一个新的Promise

* 该Promise的结果为一个数组，该数组内容为每个Promise对象的结果

* 该Promise的状态是当全部Promise执行成功时，才成功，否则失败

```js
const p1 = Promise.resolve(1);
const p2 = Promise.resolve(2);
const p3 = Promise.resolve(3);

Promise.all([p1, p2, p3]).then(value => {
  console.log(value); // [1,2,3]
})
```

#### Promise.race

##### 参数：一个装有Promise对象的数组

##### 返回值：返回一个新的Promise

* 该Promise的状态以第一个执行成功的Promise的状态为准

* 该Promise的结果为第一个执行完毕的Promise的结果

```js
const p1 = Promise.reject(1);
const p2 = Promise.resolve(2);
const p3 = Promise.resolve(3);

Promise.all([p1, p2, p3]).then(value => {
  console.log(value); // [1,2,3]
})
```

#### Promise.all和Promise.race的缺点

不适合带逻辑的异步操作，比如 p1 有两种返回结果，需要根据不同的返回结果要执行不同的函数，则 Promise.all 很难实现，不如直接使用回调函数

#### 使用例子

```js
// 1. 创建一个Promise对象
const p = new Promise((resolve, reject) => { // 执行器函数 execute
  // 2. 执行异步操作任务
  setTimeout(() => {
    const time = Date.now();
      if (time % 2 === 0) {
        // 3.1 如果成功了，调用resolve(value)
        resolve("成功的数据: " + time);
      } else {
        // 3.2 如果失败了，调用reject(reason)
        reject("失败的数据: " + time);
      }
    }, 1000);
});

p.then(
  value => { // 接收得到成功的value数据
    console.log(value);
  },
  reason => { // 
    console.log(reason);
  }
);
```

--------------------------------------

### Promise核心问题

#### 改变Promise状态的方法？

> 一共有三种改变Promise状态的方法

* resolve(value): 如果当前是pending就会变为resolved

* reject(reason): 如果当前是pending就会变为rejected

* 抛出异常: 如果当前是pending就会变为rejected

#### 一个Promise指定了多个成功/失败的回调函数，都会调用吗？

> 可以指定多个成功/失败的回调函数，都会进行调用

```js
const p = new Promise((resolve, rejecet) => {
  resolve("Promise resolved result");
});

p.then(value=>{
  console.log("1 > ", value);
});
p.then(value=>{
  console.log("2 > ", value);
});
p.then(value=>{
  console.log("3 > ", value);
});

// 输出结果
// 1 > Promise resolved result
// 2 > Promise resolved result
// 3 > Promise resolved result
```
#### 改变Promise状态和指定回调函数谁先谁后？

> 都有可能，这两种情况都允许发生
>
> 正常情况下是先指定回调函数再改变状态，但也可以先改变状态再执行回调函数

 * 如果先指定回调函数，则Promise会保存回调函数，当状态发生改变时，回调函数就会调用，得到数据
 * 如果先改变状态，则当指定回调时，回调函数就会调用，得到数据

#### then返回一个新Promise，该新Promise的状态是什么？
##### 简单表达

> 由then()中回调函数执行的结果决定

##### 详细表达

* 回调函数执行如果抛出异常，新Promise状态为rejected，结果为抛出的异常
* 回调函数执行如果返回的是非Promise的任意值（包括undefined），新Promise状态为resolved，结果为返回的值
* 如果返回的是一个Promise，则此Promise的状态和结果就是新Promise的状态和结果

#### Promise如何串连多个连续的任务？
>  Promise的then会返回一个新的Promise，可以形成链式调用

#### Promise链式调用过程中异常如何捕获？
* 当使用Promise的then链式调用时，可以在最后指定失败的回调

* 前面任何操作出现了异常，都会传递到最后失败的回调中进行处理

#### 如何中断Promise链式调用？
> 在回调函数中返回一个pending状态的Promise

```js
p.then(value => {
  return new Promise(() => {});  
})
```

