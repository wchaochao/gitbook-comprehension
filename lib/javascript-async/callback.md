# Promise

标签（空格分隔）： 理解

---

## 理解

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

* value为非thenable时，直接fulfill
* value为Promise时
 * 该Promise为原Promise时，reject
 * 该Promise不为原Promise时，等该Promise settled后再fulfill或reject
* value为其他thenable时，尝试调用then方法
  * then方法抛出Error时，reject
  * then方法调用传入的resolve时，继续resolve
  * then方法调用传入的reject时，reject

### fulfill(value)

第一次有效

* 状态变为fulfilled value
* 异步执行所有成功回调

### reject(error)

第一次有效

* 状态变为rejected value
* 异步执行所有失败回调

### trigger(handlers, argument)

异步执行所有回调

* 回调不为函数时
 * 成功回调默认为返回参数的回调
 * 失败回调默认为抛出错误的回调
* 尝试执行回调
  * 回调报错时，回调所属promise reject
  * 回调返回值时，回调所属promise resolve返回值

## 实例化

返回新Promise，尝试执行executor

* 报错时，reject
* executor调用传入的resolve时，resolve
* executor调用传入的reject时，reject

```javascript
function preloadImage (path) {
  return new Promise((resolve, reject) => {
    const image = new Image()
    image.onload = resolve
    image.reject = reject
    image.src = path
  })
}
```

## 实例方法

### Promise.prototype.then(onFulfilled, onRejected)

返回新Promise

* 参数为成功回调和失败回调，加入相应的回调堆栈中
* 原Promise unknown时，等待Promise settled，再异步执行回调
* 原Promise settled时，直接异步执行回调

```javascript
const promise = new Promise(function(resolve, reject){
  resolve('传递给then的值')
})
promise.then(function (value) {
  console.log(value)
}, function (error) {
  console.error(error)
})
```

### Promise.prototype.catch(onRejected)

捕获错误，相当于then(undefined, onRejected)

* 可以捕获之前所有promise回调中的错误
* ES3中需要使用promise['catch']

```javascript
const promise = new Promise(function(resolve, reject){
  reject(new Error('传递给catch的err'))
})
promise.then(function (value) {
  console.log(value)
}).catch(function (error) {
  console.error(error)
})
```

### Promise.prototype.finally(onFinally)

最终处理，相当于then(onFinallyWrapper, onFinallyWrapper)，onFinallyWrapper执行如下

* onFinally不是函数时，相当于then(onFinally, onFinally)
* onFinally是函数时
  * 执行onFinally，无参数
  * 返回值使用Promise.resolve转换为Promise，成功的时候返回原promise的值

```javascript
let loading = true
getData().finally(() => {
  loading = false
})
```

## 静态方法

### Promise.resolve(value)

将值转换为Promise

* value为Promise时，直接返回
* value为其他值时，进行resolve值判断

```javascript
Promise.resolve(value)
Promise.resolve(promise)
Promise.resolve(thenable)
```

### Promise.reject(error)

创建rejected promise

```javascript
Promise.reject(new Error('bar))
```

### Promise.all(iterable)

等待所有任务执行成功

* 通过Promise.resolve将iterable的元素转换为Promise
* 返回一个新Promise，所有的Promise成功时resolve，有一个失败时reject

```javascript
Promise.all('123').then(arr => console.log(arr))
```

### Promise.race(iterable)

等待某一任务执行完成

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
  const error = new TimeoutError('timeout')
  return Promise.reject(error)
})
Promise.race(promise, timeoutPromise).then(() => {
  // 操作成功
}).catch(e => {
  if (e instanceof TimeoutError) {
    // 超时
  }
})
```

### Promise.allSettled(iterable)

等待所有任务执行完成

* 通过Promise.resolve将iterable的元素转换为Promise
* 返回一个新Promise，所有的Promise执行完成时resovle
 * 任务成功时对应值{status: 'fulfilled', value: value}
 * 任务失败时对应值{status: 'rejected', reason: reason}

```javascript
Promise.allSettled([Promise.resolve(1), Promise.reject(-1)]).then(results => console.log(results)) // [{status: 'fulfilled', value: 1}, {status: 'rejected', reason: -1}]
```

### Promise.any(iterable)

等待任一任务执行成功

* 通过Promise.resolve将iterable的元素转换为Promise
* 返回一个新Promise，有一个Promise成功时resolve，所有Promise失败时reject，值为AggregatorError

```javascript
Promise.any([Promise.reject(-1), Promise.reject(-2)]).catch(results => console.log(results)) // [-1, -2]
```

## 异步处理

通过链式调用处理异步任务

### 错误处理

在链式调用的最后catch错误

```javascript
promise.then(function1)
  .then(function2)
  .catch(errorHandler)
```

catch无法捕获在回调中异步抛出的错误

```javascript
promise.then(() => {
  setTimeout(() => {
    throw new Error('async error')
  })
}).catch(e => {
  // 捕获不到async error
})
```

### 串行

链式调用

```javascript
promise.then(function1)
  .then(function2)
  .then(function3)
```

使用reduce

```javascript
promises.reduce((result, item) => {
    return Promise.resolve(result).then(val => {
      return handler(val, item)
    })
}, undefined)
```

### 并行

使用循环

```javascript
for (let i = 0; i < 10; i++) {
  promise[i].then(handler)
}
```

使用Promise.all

```javascript
Promise.all(promises).then(handler)
```

### 单元测试

返回promise

```javascript
describe('Promise', () => {
  it('return promise', () => {
    return promise.then(() => {
      // assert
    })
  })
})
```

## Promise库

* [ypromise](https://github.com/YahooArchive/ypromise/blob/master/promise.js)：YUI实现的Promise Polyfill
* [native-promise-only](https://github.com/getify/native-promise-only/blob/master/lib/npo.src.js)：以作为ES6 Promises的polyfill为目的的类库
* [es6-promise](https://github.com/stefanpenner/es6-promise)：兼容 ES6 Promises的Polyfill类库
* [prfun](https://github.com/cscott/prfun)：Promise帮助函数
* [q.js](https://github.com/kriskowal/q/blob/master/q.js)：Promise扩展类库，实现了 Promises 和 Deferreds 等规范
* [Bluebird](https://github.com/petkaantonov/bluebird)：Promise扩展类库，扩展了取消promise对象的运行，取得promise的运行进度，以及错误处理的扩展检测等非常丰富的功能

## 参考资料

* [Promise/A+](https://promisesaplus.com/)
* [Promise迷你书](http://liubin.org/promises-book/)
* [Promise反模式](http://taoofcode.net/promise-anti-patterns/)
* [w3c promise guide](https://www.w3.org/2001/tag/doc/promises-guide)
* [ES6入门-Promise对象](https://es6.ruanyifeng.com/#docs/promise)
* [ECMAScript Promise](https://tc39.es/ecma262/#sec-promise-objects)
