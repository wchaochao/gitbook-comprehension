# 渲染机制

标签（空格分隔）： 理解

---

## 引擎

### 渲染引擎

* 将HTML解析为DOM树
* 将CSS解析为CSSOM树
* DOM树和CSSOM树结合为渲染树
* 渲染树变化时进行重排和重绘

### JavaScript引擎

* 将JavaScript解析为ESTree
* 将ESTree翻译为字节码
* 解释执行字节码，除可执行JavaScript API外还可执行DOM API、CSSOM API、Web API

### 互斥

JavaScript引擎线程和渲染线程互斥

* 渲染时会阻塞JavaScript执行
* JavaScript执行时会阻塞页面渲染

## JavaScript执行

### 同步任务

顺序执行

* 执行全局代码时全局上下文入栈
* 执行函数时将函数上下文入栈
* 执行完函数时函数上下午出栈

### 异步任务

通过事件循环执行

* 执行setTimeout、setInterval，将定时器下发到定时器线程，计数结束时将定时器回调加入到任务队列中
* 执行http请求，将http请求下发到http线程，请求状态发生变更时将相应的回调加入任务队列中
* 执行Promise，promise状态发生变更时将相应的回调加入到任务队列中
* 执行MutationObserver，节点发生变更时将相应的回调加入到任务队列中

## 事件循环

### 任务队列

* 宏任务：script、setTimeout、setInterval、http请求、DOM事件
* 微任务：Promise、MutationObserver

### 执行顺序

* 执行一个宏任务
* 执行所有微任务
* 渲染页面
* 执行Web worker
