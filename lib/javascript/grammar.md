# ES6语法

标签（空格分隔）： 理解

---

## ...

### 剩余参数

将剩余参数收集到一个数组中

```javascript
function sum1 (...args) {}

function sum2 (a, ...args) {}
```

### 展开

* ...obj：展开对象
* ...arr：展开数组
* ...iterable：将iterable转换为数组再展开

```javascript
Math.max(...arr)
let merged = [...arr, ...str]
let objCopy = {...objCopy}
```

## 箭头函数

* 箭头函数中的this对象为外部的this
* 箭头函数的arguments对象为外部的arguments

```javascript
const fn = (a, b) => a + b
```

## 参考资料

* [JavaScript.info](https://javascript.info/)
