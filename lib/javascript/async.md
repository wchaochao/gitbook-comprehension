# 异步编程

标签（空格分隔）： 理解

---

## 回调

通过回调函数处理异步任务

### 异步处理

* 错误处理：error-first回调
* 串行：在回调中执行下一个异步，导致回调地狱
* 并行：使用循环并行执行

```javascript
// error-first回调
loadScript('/my/script.js', function(error, script) {
  if (error) {
    // handle error
  } else {
    // script loaded successfully
  }
});
```

### 回调测试

```javascript
describe('Callback', () => {
  it('user `done`', done => {
    asyncTask(() => {
      // assert
      done()
    })
  })
})
```

## Promise

通过Promise的链式调用处理异步任务

### 实例化

```javascript
const promise = new Promise((resolve, reject) => {
  // 异步处理完成时resolve(value) or reject(error)
})
```

#### 状态

* pending -> fulfilled
* pending -> rejected

![Promise实例化](https://javascript.info/article/promise-basics/promise-resolve-reject.svg)

#### resolve(value)

第一次有效

* value为普通值，直接resolve
* value为Promise，等Promise settled时再resolve或reject
 * 该Promise是原Promise时reject
* value为thenable，尝试调用then方法
  * then方法抛出Error时，reject
  * then方法resolve时，继续对resolve值进行判断
  * then方法reject时，reject

#### reject(error)

第一次有效

* 不管error为何值，直接reject
* 抛出错误相当于reject

### 实例方法

#### Promise#then

* 参数为成功回调和失败回调
 * promise resolve时执行成功回调，参数为resolve value
 * promise reject时执行失败回调，参数为reject error
* 返回值为新Promise，状态由回调执行情况决定
 * 回调不是函数时，原Promise的状态传递给新Promise
 * 回调抛出Error时，新Promise reject该错误
 * 回调返回值时，新Promise对该值进行resolve值判断

```javascript
promise.then(onFulfilled, onRejected)
```

#### Promise#catch

捕获错误，相当于then(undefined, onRejected)

* 可以捕获之前所有promise的错误
* ES3中需要使用promise['catch']

```javascript
promise.catch(onRejected)
```

#### Promise#finally

最终处理，相当于then(onFinallyWrapper, onFinallyWrapper)，onFinallyWrapper执行如下

* 执行onFinally，无参数
* onFinally返回一个非Promise值时，onFinallyWrapper返回原Promise的值
* onFinally返回一个Promise时，该Promise resolve时传递原Promise状态，reject时传递该Promise状态，onFinallyWrapper返回该Promise

```javascript
promise.finally(onFinally)
```

### 静态方法

#### Promise.resolve

将值转换为Promise

* value为Promise时，直接返回
* value为其他值时，进行resolve值判断

```javascript
Promise.resolve(1)
```

#### Promise.reject

创建rejected promise

```javascript
Promise.reject('error')
```

#### Promise.all

并行

* 数组中的元素通过Promise.resolve转换为Promise
* 创建一个Promise，所有的Promise成功时resolve，有一个失败时reject

```javascript
Promise.all([1, 2, 3]).then(arr => console.log(arr))
```

#### Promise.race

竞争

* 数组中的元素通过Promise.resolve转换为Promise
* 创建一个Promise，有一个Promise成功时resolve，有一个失败时reject

```javascript
Promise.race([1, 2, 3]).then(val => console.log(val))
```

### 异步处理

* 错误处理：最后catch
* 串行：链式调用
* 并行：循环、all、race

### Promise测试

```javascript
describe('Promise', () => {
  it('return promise', () => {
    return promise.then(() => {
      // assert
    })
  })
})
```

### Promise库

* [ypromise](https://github.com/YahooArchive/ypromise/blob/master/promise.js)：YUI实现的Promise Polyfill
* [native-promise-only](Promise Polyfill)：以作为ES6 Promises的polyfill为目的的类库
* [es6-promise](https://github.com/stefanpenner/es6-promise)：兼容 ES6 Promises的Polyfill类库
* [JSDeferred](https://github.com/cho45/jsdeferred/blob/master/jsdeferred.js)：deferred类库
* [q.js](https://github.com/kriskowal/q/blob/master/q.js)：Promise扩展类库，实现了 Promises 和 Deferreds 等规范
* [Bluebird](https://github.com/petkaantonov/bluebird)：Promise扩展类库，扩展了取消promise对象的运行，取得promise的运行进度，以及错误处理的扩展检测等非常丰富的功能

## Generator

使用Generator的yield/next处理异步任务

### 创建

```javascript
function* generateSequence () {
  // yield value
}

const g = generateSequence()
```

* 也是Iterable对象，可以for...of、Array.from、展开
* 也是Iterator对象，可以调用next方法

### 嵌套

通过yield*嵌套另一个Generator

```javascript
function* generateSequence(start, end) {
  for (let i = start; i <= end; i++) yield i;
}

function* generatePasswordCodes() {

  // 0..9
  yield* generateSequence(48, 57);

  // A..Z
  yield* generateSequence(65, 90);

  // a..z
  yield* generateSequence(97, 122);

}
```

### Generator#next

执行至下一个yield处

* 将参数传递进Generator函数，作为上一个yield的返回值
* 执行代码至下一个yield处或函数结束
* 返回{value: any, done: boolean}到函数外
 * value为下一个yield或return的值
 * done为函数是否执行完成

### Generator#throw

在yield返回处抛出错误

```javascript
function* gen() {
  try {
    let result = yield "2 + 2 = ?"; // (1)

    alert("The execution does not reach here, because the exception is thrown above");
  } catch(e) {
    alert(e); // shows the error
  }
}

let generator = gen();

let question = generator.next().value;

generator.throw(new Error("The answer is not found in my database")); // (2)
```

### 异步原理

通过yield/next交换值

* yield时返回Promise对象或Thunk函数
* next时在value的回调中继续next，参数为回调值

### 异步处理

* 错误处理：throw、try/catch
* 串行：连续yield/next

### Generator库

* [thunkify](https://github.com/tj/node-thunkify)：处理nodejs的回调
* [co](https://github.com/tj/co)：自动化Generator
* [koa](https://github.com/koajs/koa)：http框架

## async/await

Generator的语法糖

### async

返回Promise

* 成功时resolve
* 出错时reject

```javascript
async function f1 () {
  return 1;
}

f1().then(alert); // 1

async function f2 () {
  return Promise.resolve(1);
}

f2().then(alert); // 1

async function f () {
  let response = await fetch('http://no-such-url');
}

// f() becomes a rejected promise
f().catch(alert); // TypeError: failed to fetch // (*)
```

### await

* 只能在async函数中
* 遇到promise/thenable时暂停函数执行直到promise/thenable完成
 * promise/thenable成功时返回result
 * promise/thenable失败时抛出错误

```javascript
async function f () {
 let value = await promise
}
```

### 异步处理

* 错误处理：try/catch
* 串行：连续await

## 异步任务调度器

* 支持并发限制
* 支持优先级
* 支持重试

## 参考资料

* [异步处理](http://codingdict.com/article/22485)
* [Promise/A+](https://promisesaplus.com/)
* [Promise迷你书](http://liubin.org/promises-book/)
* [JavaScript.info](https://javascript.info/)
