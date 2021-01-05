# 异步处理

标签（空格分隔）： 理解

---

## 回调

通过回调函数处理异步任务

### 缺点

* 回调地狱

## Promise

通过Promise的链式调用处理异步任务

### Promise规范

#### 状态

* pending -> fulfilled
* pending -> rejected

#### then方法

* 参数为成功回调和失败回调
* 返回值为新Promise，状态由回调决定

### Promise API

#### 实例化

```javascript
const promise = new Promise((resolve, reject) => {
  // resolve(value) or reject(reason)
})
```

### 链式调用

* promise.then(onFulfill, onReject)：链式处理
* promise.catch(onReject)：捕获错误，相当于promise.then(null, onReject)
* promise.finally(onFinally): 最终处理，相当于promise.finally(onFinally, onFinally)

### 静态创建

* Promise.resolve(value)：创建fulfilled的promise
* Promise.reject(reason)：创建rejected的promise

### 多个promise

* Promise.all(arr)：所有promise成功时执行onFulfill回调
* Promise.race(arr)：有一个promise成功时执行onFulfill回调

### Promise库

* [q.js](https://github.com/kriskowal/q/blob/master/q.js)：Promise实现
* [Bluebird](https://github.com/petkaantonov/bluebird)：Promise实现

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

### next方法

执行至下一个yield处

* 将参数传递进Generator函数，作为上一个yield的返回值
* 执行代码至下一个yield处或函数结束
* 返回{value: any, done: boolean}到函数外
 * value为下一个yield或return的值
 * done为函数是否执行完成

### throw方法

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

### 异步处理

通过yield/next交换值

* yield时返回Promise对象或Thunk函数
* next时在value的回调中继续next，参数为回调值

### Generator库

* [thunkify](https://github.com/tj/node-thunkify)：处理nodejs的回调
* [co](https://github.com/tj/co)：自动化Generator
* [koa](https://github.com/koajs/koa)：http框架

## async/await

Generator的语法糖

### async

* 返回Promise

```javascript
async function f1() {
  return 1;
}

f1().then(alert); // 1

async function f2() {
  return Promise.resolve(1);
}

f2().then(alert); // 1
```

### await

* 在async函数中
* 暂停函数执行直到promise/thenable完成
 * promise/thenable成功时返回result
 * promise/thenable失败时抛出TypeError

```javascript
let value = await promise
```

## 参考资料

* [JavaScript.info](https://javascript.info/)
* [异步处理](http://codingdict.com/article/22485)
