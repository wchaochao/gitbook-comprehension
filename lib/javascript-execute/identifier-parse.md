# 标志符解析

标签（空格分隔）： 理解

---

## 理解

沿着环境记录项链查找标志符

* 在当前环境记录项中查找标志符
 * 可以找到，返回标志符的值
 * 找不到，继续查找外层环境记录项
* 所有外层环境记录项都找不到，报错

## Environment Record

环境记录项，记录绑定的标志符

### 标志符记录

* Mutable：可变标志符，可重复赋值
 * Name：标志符名
 * Value：标志符值
 * Deleted：标志符是否可删除
* Immutable：不可变标志符，只能赋值一次
 * Name：标志符名
 * Value：标志符值
 * Strict：是否是严格模式，用于控制报错

### 通用内部状态

| 内部状态 | 类型 | 描述 |
| --- | --- | --- |
| [[OuterEnv]] | Environment Record &#x7c; Null | 外层环境记录项 |

### 通用内部操作

| 内部方法 | 类型 | 描述 |
| --- | --- | --- |
| HasBind(N) | (String) -> Boolean | 是否绑定了标志符N |
| CreateMutableBinding(N, D) | (String, Boolean) -> Boolean | 创建可变绑定，未初始化 |
| CreateImmutableBinding(N, S) | (String, Boolean) -> Boolean | 创建不可变绑定，未初始化 |
| InitializeBinding(N, V) | (String, any) -> Boolean | 初始化绑定的标志符 |
| SetMutableBinding(N, V, S) | (String, any, Boolean) -> Boolean | 设置可变绑定的值 |
| GetBindValue(N, S) | --- | 获取绑定标志符的值 |
| DeleteBinding(N) | --- | 删除绑定 |
| HasThisBinding() | --- | 是否有this绑定 |
| HasSuperBinding() --- | | 是否有super绑定 |
| WithBaseObject() --- | | 绑定对象 |

## declarative Environment Record

声明式环境记录项

* 执行函数、模块、变量声明、cause语句时产生

### function Environment Record

函数式环境记录项

* 执行函数时产生
* 提供this、super，记录参数和顶层标志符

### module Environment Record

模块式环境记录项

* 执行模块时产生
* 记录模块的import值和顶层标志符
* [[OuterEnv]]为global Environment Record

## object Environment Record

对象式环境记录项

* 执行with语句时产生，只绑定可变标志符
* 有一个绑定对象，标志符绑定操作等价于绑定对象的属性操作

### 特定内部状态

| 内部状态 | 类型 | 描述 |
| --- | --- | --- |
| binding object | Object | 绑定对象 |
| withEnvironment | Boolean | 是否提供绑定对象，默认为false |

### 特定内部方法

#### HasBinding(N)

* N不是绑定对象的属性，返回false
* N是绑定对象是属性
 * withEnvironment为false，返回true
 * withEnvironment为true且N不在绑定对象的Symbol.unscopables中，返回true

#### CreateMutableBinding(N, D)

* 设置属性的属性描述符

## global Environment Record

全局环境记录项

* 执行全局代码时产生
* 有一个全局对象，标志符绑定操作等价于全局对象的属性操作
* [[OuterEnv]]为null

## 参考资料

* [ECMASCript Environment Records](https://tc39.es/ecma262/#sec-environment-records)
