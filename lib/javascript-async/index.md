# 异步处理

标签（空格分隔）： 理解

---

## 回调

通过回调函数处理异步任务

### 错误处理

error-first回调

```javascript
loadScript('/my/script.js', (error, script) => {
  if (error) {
    // handle error
  } else {
    // script loaded successfully
  }
});
```

### 串行

在回调中执行下一个异步，导致回调地狱

```javascript
loadScript('/my/script1.js', script1 => {
  loadScript('/my/script2.js', script2 => {
    // ...
  })
});
```

### 并行

使用循环并行执行

```javascript
for (let i = 0; i < 10; i++) {
  loadScript(`/my/script${i}`, script => {
    afterLoadComplete(i, script)
  })
}
```

### 单元测试

使用done函数指明何时完成异步任务

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
promises.reduce((promise, item) => {
    return promise.then(() => item)
}, Promise.resolve())
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

### Promise测试

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
