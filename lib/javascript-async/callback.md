# 回调

标签（空格分隔）： 理解

---

## 理解

* 异步任务最终都是通过回调来处理的
* 回调的本质是转移回操作权

## 异步处理

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

## 推荐资料

* [异步处理](http://codingdict.com/article/22485)
