# NodeJS基础

标签（空格分隔）： 理解

---

* 异步I/0
* 事件驱动
* 单线程

## 模块机制

### 模块

module

* require：模块引用
* 模块标识：地址或字符串
* exports：模块引用

### 模块调用

* 文件模块：JavaScript模块调用C/C++扩展模块
* 文件模块调用核心模块
* 核心模块：JavaScript核心模块调用C/C++内建模块
* C/C++模块调用平台层libev
* libev调用各自的操作系统API

### 模块加载

#### 标识解析

* 地址解析为绝对地址
* 字符串不动

#### 缓存命中

* 根据绝对地址或字符串命中缓存
* 未命中生成模块

#### 路径分析

* 绝对地址不用分析
* 字符串对应核心模块时直接调用核心模块
 * 通过process.binding加载JavaScript核心模块，编译执行
 * JavaScript核心模块通过process.binding调用C/C++内建模块
* 字符串不为核心模块时生成模块路径数组，遍历所有父路径下的node_modules

#### 文件定位

* 作为文件
 * 有扩展名，直接定位文件
 * 无扩展名，依次尝试.js、.node、.json扩展名
* 作为目录
 * 获取package.json下的main文件，定位main文件
 * 获取不到package.json下的main文件，定位index文件，无扩展名尝试
* 非核心字符串标识不断往上遍历模块路径数组

#### 编译执行

* js文件：加载js文件，wrap成函数，传入参数执行
* node文件：使用dlopen加载node文件，执行后返回模块
* json文件：加载json文件，使用JSON.parse解析

### 其他模块

AMD

```javascript
define(id?, dependencies?, factory)

function factory (...deps) {}
```

CMD

```javascript
define(factory)

function factory (require, exports, module) {}
```

## 包

### 包结构

* bin
* lib
* doc
* test
* package.json

### package.json结构

* name
* version
* description
* keywords
* author
* license
* main
* bin
* script
* dependencies
* devDependencies

### 包管理器

* npm -v：版本号
* npm init：生成package.json
* npm i <package>：安装包
 * package可以是npm上的包名、url地址、本地包地址
 * 通过--registry设置镜像站
 * 通过-g全局安装
* npm i -D <package>：安装开发依赖
* npm uninstall <package>：移除包
* npm adduser：添加用户
* npm publish <folder>：发布包
* npm owner：设置包拥有者

### 安装包

* 当前目录下没有node_modules目录时创建node_modules目录
* 下载包并解压到node_modules目录
* 包有bin字段时创建软链接

### 包脚本

* 通过npm run执行scripts，执行时会将node_modules下的bin目录加到执行路径path中
* script可以添加pre、post钩子，如preinstall、postinstall

## 异步I/O

### I/O操作

* 阻塞I/O：发送I/O请求，I/O完成后才返回
* 非阻塞I/O：发送I/O请求，直接返回，轮询I/O是否完成
* 理想非阻塞异步I/O：发送I/O请求，直接返回，I/O完成时通知
* NodeJS异步I/O：主线程发送I/O请求时，创建I/O线程，由I/O线程去完成I/O操作，完成后通知主线程

### 事件循环

#### 任务队列

宏任务

* 定时器队列：setTimeout、setInterval
* I/O队列：文件请求、网络请求
* Immediate队列：setImmediate
* close队列：close事件

微任务

* nextTick队列：process.nextTick
* 其他微任务队列：promise

#### 执行顺序

* timers阶段：执行定时器队列中的回调
* pending callbacks阶段：
* idle, prepare阶段：系统内部使用
* poll阶段：执行I/O队列中的回调
* check阶段：执行Immediate队列中的回调
* close callbacks阶段：执行close队列中的回调
* 两个阶段之间执行所有微任务，nextTick队列优先级高于其他微任务队列
* Node11后执行一个timer、immediate回调后执行所有微任务

## 参考资料

* 《深入浅出Node.js》
* [Event Loop](https://blog.insiderattack.net/event-loop-and-the-big-picture-nodejs-event-loop-part-1-1cb67a182810)
