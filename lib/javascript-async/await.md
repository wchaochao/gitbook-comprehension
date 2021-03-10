# Async/Await

标签（空格分隔）： 理解

---

## 理解

自动执行的Generator

* async表示当前操作为异步操作
* await表示等待值执行完毕

## async

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

## 参考资料

* [异步处理](http://codingdict.com/article/22485)
