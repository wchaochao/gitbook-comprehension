# 浏览器

标签（空格分隔）： 理解

---

## 组成

### 渲染线程

* HTML被HTML引擎解析为DOM树
* CSS被CSS引擎解析为CSSOM树
* DOM树和CSSOM树结合为渲染树
* 渲染树变化时进行重排和重绘

### JavaScript引擎线程

* JavaScript被解析器解析为ESTree
* ESTree被翻译器翻译为字节码
* 字节码被放入任务队列中，根据事件循环执行

### 单线程

JavaScript引擎线程和渲染线程互斥

* 渲染时会阻塞JavaScript执行
* JavaScript执行时会阻塞页面渲染

### 定时器触发线程

* JavaScript执行时遇到定时器setTimeout、setInterval时，会将定时器交给定时器触发线程维护
* 定时器计数完毕时，事件触发线程会将定时器回调加入到任务队列中

### http请求线程

* JavaScript发送http请求时，会将请求交给http请求线程
* 请求状态发生变更时，事件触发线程会将相应的回调加入任务队列中

### 事件触发线程

* 将准备好的事件回调加入到任务队列中

## 事件循环

### 任务队列

* 宏任务：script、setTimeout、setInterval、http请求、DOM事件
* 微任务：Promise、MutationObserver

### 执行顺序

* 执行一个宏任务
* 执行所有微任务
* 渲染
* 执行Web worker
