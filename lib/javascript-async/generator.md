# Generator

标签（空格分隔）： 理解

---

## 理解

分段回调函数

* next表示将值传递进Generator，执行下一段函数
* yield表示当前段函数执行完毕，返回yield值

## 创建

* 使用`function*`表示Generator生成器
* 使用`yield`返回当前段函数生成的值
* 使用`yield*`返回另一个Generator的生成值

```javascript
function* makeGenerator () {
  // yield value
  // yield* anotherGenerator
}

const g = makeGenerator()
```

## 实例属性

### Generator.prototype.next(value)

执行下一段函数

* 将value传递回Generator函数
 * 第一次调用时，从Generator函数开头开始
 * 非第一次调用时，作为上一次yield的返回值
* 执行代码至下一个yield处或函数结束处
* 返回{value: any, done: boolean}到函数外
 * value为下一个yield或return的值
 * done为函数是否执行完成

### Generator.prototype.throw(error)

执行下一段函数，传入错误

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

## 异步处理

自动执行Generator的所有分段函数，返回最终结果

* 对yield的值进行Promise封装
* Promise成功时通过next返回值
* Promise失败时通过throw返回值

### 错误处理

在Generator中try/catch

### 串行

不断yield

## Generator库

* [thunkify](https://github.com/tj/node-thunkify)：处理nodejs的回调
* [co](https://github.com/tj/co)：自动化Generator
* [koa](https://github.com/koajs/koa)：http框架
