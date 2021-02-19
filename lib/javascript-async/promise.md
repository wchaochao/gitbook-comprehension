# Promise

标签（空格分隔）： 理解

---

## 原理

表示一个unknown value

* 初始状态为pending undefined
* 通过resolve、reject操作改变状态，确定settled值

### 状态

状态发生改变后就不能更改

* pending -> fulfilled
* pending -> rejected

![Promise实例化](https://javascript.info/article/promise-basics/promise-resolve-reject.svg)

### resolve(value)

第一次有效

* value为非thenable时，fulfill
* value为Promise时
 * 该Promise为原Promise时，reject
 * 该Promise不为原Promise时，等该Promise settled后再fulfill或reject
* value为其他thenable时，尝试调用then方法
  * then方法抛出Error时，reject
  * then方法调用传入的resolve时，对resolve值继续进行判断
  * then方法调用传入的reject时，reject

### fulfill(value)

第一次有效

* 状态变为fulfilled value
* 异步执行所有成功回调
 * 回调不为函数，回调所属promise resolve
 * 回调为函数，尝试执行回调
  * 回调报错时，回调所属promise reject
  * 回调返回值时，回调所属promise resolve返回值

### reject(error)

第一次有效

* 状态变为rejected value
* 异步执行所有失败回调
 * 回调不为函数，回调所属promise reject
 * 回调为函数，尝试执行回调
  * 回调报错时，回调所属promise reject
  * 回调返回值时，回调所属promise resolve返回值

## 实例化

返回新Promise，尝试执行executor

* 报错时，reject
* executor调用传入的resolve时，resolve
* executor调用传入的reject时，reject

```javascript
const promise = new Promise((resolve, reject) => {
  // 异步处理完成时resolve(value) or reject(error)
})
```

## 实例方法

### Promise.prototype.then(onFulfilled, onRejected)

返回新Promise

* 参数为成功回调和失败回调，加入相应的回调堆栈中
* 原Promise unknown时，等待Promise settled，再异步执行回调
* 原Promise settled时，直接异步执行回调

```javascript
promise.then(onFulfilled, onRejected)
```

### Promise.prototype.catch(onRejected)

捕获错误，相当于then(undefined, onRejected)

* 可以捕获之前所有promise的错误
* ES3中需要使用promise['catch']

### Promise.prototype.finally(onFinally)

最终处理，相当于then(onFinallyWrapper, onFinallyWrapper)，onFinallyWrapper执行如下

* onFinally不是函数时，相当于then(onFinally, onFinally)
* onFinally是函数时
  * 执行onFinally，无参数
  * 返回值使用Promise.resolve转换为Promise，成功的时候返回原promise的值

## 静态方法

### Promise.resolve(value)

将值转换为Promise

* value为Promise时，直接返回
* value为其他值时，进行resolve值判断

```javascript
Promise.resolve(1)
```

### Promise.reject(error)

创建rejected promise

```javascript
Promise.reject(new Error('bar))
```

### Promise.all(iterable)

并行执行所有异步任务

* 通过Promise.resolve将iterable的元素转换为Promise
* 返回一个新Promise，所有的Promise成功时resolve，有一个失败时reject

```javascript
Promise.all('123').then(arr => console.log(arr))
```

### Promise.race(iterable)

竞争执行所有异步任务

* 通过Promise.resolve将iterable的元素转换为Promise
* 返回一个新Promise，有一个Promise成功时resolve，有一个失败时reject
* 可通过Promise.race实现超时机制

```javascript
function delay (ms) {
  return new Promise(resolve => {
    setTimeout(resolve, ms)
  })
}

const timeoutPromise = delay(1000).then(() => {
  const error = new Error('timeout')
  error.customeType = 'timeout'
  return Promise.reject(error)
})
Promise.race(promise, timeoutPromise).then(() => {
  // 操作成功
}).catch(e => {
  if (e.customeType === 'timeout') {
    // 超时
  }
})
```

## Promise库

* [ypromise](https://github.com/YahooArchive/ypromise/blob/master/promise.js)：YUI实现的Promise Polyfill
* [native-promise-only](https://github.com/getify/native-promise-only/blob/master/lib/npo.src.js)：以作为ES6 Promises的polyfill为目的的类库
* [es6-promise](https://github.com/stefanpenner/es6-promise)：兼容 ES6 Promises的Polyfill类库
* [prfun](https://github.com/cscott/prfun)：Promise帮助函数
* [q.js](https://github.com/kriskowal/q/blob/master/q.js)：Promise扩展类库，实现了 Promises 和 Deferreds 等规范
* [Bluebird](https://github.com/petkaantonov/bluebird)：Promise扩展类库，扩展了取消promise对象的运行，取得promise的运行进度，以及错误处理的扩展检测等非常丰富的功能

## 推荐资料

* [Promise/A+](https://promisesaplus.com/)
* [Promise迷你书](http://liubin.org/promises-book/)
* [Promise反模式](http://taoofcode.net/promise-anti-patterns/)
