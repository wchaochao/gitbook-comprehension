# 渲染机制

标签（空格分隔）： 理解

---

## 渲染引擎

* HTML被HTML引擎解析为DOM树
* CSS被CSS引擎解析为CSSOM树
* DOM树和CSSOM树结合为渲染树
* 渲染树变化时进行重排和重绘

### HTML引擎

* HTML字符流会被HTML词法解析器解析为HTML Token流
* HTML Token流会被HTML语法解析器解析为DOM树

#### HTML词法解析

* 声明：文档类型声明
* 标签：开始标签、结束标签
* 属性：属性名、属性值
* 文本：Unicode字符
* 实体：命名实体、十进制实体、十六进制实体
* 其他字符数据：注释、指令、CDATA数据

#### HTML语法解析

将HTML Token解析为对应的DOM节点

* Document: 文档节点
 * HTMLDocument：HTML文档节点
* DocumentType: 文档类型节点
* DocumentFragment: 文档片段节点
* Element: 元素节点
 * HTMLElement：HTML元素节点
* Attr: 属性节点
* CharacterData: 字符数据节点
 * Text: 文本节点
 * CDATASection: CDATA节点
 * ProcessingInstruction: 指令节点
 * Comment：注释节点

资源类的HTML元素节点会加载相应的资源

* link：加载CSS
* script：加载js
* img：加载图片
* audio：加载音频
* video：加载视频
* iframe：加载html

### CSS引擎

* CSS字符流会被CSS词法解析器解析为CSS Token流
* CSS Token流会被CSS语法解析器解析为CSSOM树

#### CSS词法解析

* 选择器
* 样式规则

#### CSS语法解析

CSS Rule节点

### 重排

* 盒模型尺寸、位置发生更改会导致重排

### 重绘

* 盒模型字体、颜色、背景颜色等样式发生更改会导致重绘

## JavaScript引擎

* JavaScript源代码会被JavaScript词法分析器解析为JavaScript Token流
* JavaScript Token流会被JavaScript语法分析器解析为ESTree
* ESTree被翻译为优化后的JavaScript字节码
* 执行JavaScript字节码，操作DOM、CSSOM、Web API

### JavaScript词法解析

非Token类

* 空白字符：`\t \v \f 空格 不可见空格`
* 行终结符：`\r \n 行分隔符 段分隔符`
* 注释：单行注释、多行注释

Token类型

* 标志符名
 * 保留字：关键字、未来保留字、Null字面量、Boolean字面量
 * 标志符：保留字外的标志符名
* 符号：运算符号、语句符号
* 字面量
 * Null字面量
 * Boolean字面量
 * 数字字面量：整数、小数、科学计数法
 * 字符串字面量：单引号或双引号包围的普通字符、转义字符、行延续符
 * 正则字面量

### JavaScript语法解析

* 字面量节点
* 表达式节点
* 语句节点
* 函数节点
* script/module节点

### JavaScript执行

* 环境准备：执行上下文、Realm、环境记录项
* 标志符绑定：将声明的标志符绑定到环境记录项中
* 引用求值：标志符解析、this解析、对象属性访问
* 运算：各类表达式
* 操作：各类语句、内置对象操作、宿主对象操作（DOM、CSSOM、Web API）

### 互斥

JavaScript引擎线程和渲染线程互斥

* 渲染时会阻塞JavaScript执行
* JavaScript下载、执行会阻塞页面渲染

## 事件循环

### 任务队列

* 宏任务：script、setTimeout、setInterval、http请求、DOM事件
* 微任务：Promise、MutationObserver

### 异步任务

* 执行setTimeout、setInterval时，将定时器下发到定时器线程，计数结束时将定时器回调加入到宏任务中
* 执行http请求，将http请求下发到http线程，请求状态发生变更时将相应的回调加入宏任务中
* 执行Promise，promise状态发生变更时将相应的回调加入到微任务中
* 执行MutationObserver，节点发生变更时将相应的回调加入微任务中

### 执行顺序

* 执行一个宏任务
* 执行所有微任务
* 渲染页面
* 执行Web worker
