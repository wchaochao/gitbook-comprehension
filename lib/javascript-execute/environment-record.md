# 环境记录项

标签（空格分隔）： 理解

---

## Environment Record

环境记录项，记录绑定的标志符

### 通用内部状态

| 内部状态 | 类型 | 描述 |
| --- | --- | --- |
| [[OuterEnv]] | Environment Record &#x7c; Null | 外层环境记录项 |

### 通用内部操作

| 内部方法 | 类型 | 描述 |
| --- | --- | --- |
| HasBind(N) | (String) -> Boolean | 是否绑定了标志符N |
| CreateMutableBinding(N, D) | (String, Boolean) -> void | 创建可变绑定，未初始化 |
| CreateImmutableBinding(N, S) | (String, Boolean) -> void | 创建不可变绑定，未初始化 |
| InitializeBinding(N, V) | (String, any) -> void | 初始化绑定的标志符 |
| SetMutableBinding(N, V, S) | (String, any, Boolean) -> void | 设置可变绑定的值 |
| GetBindValue(N, S) | (String, Boolean) -> any | 获取绑定标志符的值 |
| DeleteBinding(N) | (String) -> Boolean | 删除绑定 |
| HasThisBinding() | () -> Boolean | 是否有this绑定 |
| HasSuperBinding() | () -> Boolean | 是否有super绑定 |
| WithBaseObject() | () -> Object &#x7c; Undefined  | with的绑定对象 |

## declarative Environment Record

声明式环境记录项，继承自Environment Record

* 执行函数、模块、变量声明、cause语句时产生

### 标志符记录

* Mutable：可变标志符，可重复赋值
 * Name：标志符名
 * Value：标志符值
 * Deleted：标志符是否可删除
* Immutable：不可变标志符，只能赋值一次
 * Name：标志符名
 * Value：标志符值
 * Strict：是否是严格绑定，用于控制报错

### 特定内部方法

#### HasBinding(N)

* 绑定了标志符N，返回true
* 没有绑定标志符N，返回false

#### CreateMutableBinding(N, D)

* 断言没有绑定标志符N
* 创建可变绑定，未初始化

#### CreateImmutableBinding(N, S)

* 断言没有绑定标志符N
* 创建不可变绑定，未初始化

#### InitializeBinding(N, V)

* 断言绑定了标志符N，且未初始化
* 设置标志符N的值为V

#### SetMutableBinding(N, V, S)

* 未绑定标志符N时
 * S为true时，抛出ReferenceError
 * S为false时，创建可变绑定，并初始化为V
* 绑定了标志符N时
 * 未初始化时，抛出ReferenceError
 * 已初始化时
  * 可变绑定设置值
  * 不可变绑定，为严格绑定或S为true，抛出TypeError

#### GetBindingValue(N, S)

* 断言绑定了标志符N
* 未初始化时，抛出ReferenceError
* 已初始化时，返回标志符值

#### DeleteBinding(N)

* 断言绑定了标志符N
* 标志符N为可变绑定
 * 可删除时，删除N并返回true
 * 不可删除时，返回false
* 标志符N为不可变绑定，返回false

#### HasThisBinding()

* 返回false

#### HasSuperBinding()

* 返回false

#### WithBaseObject()

* 返回undefined

## function Environment Record

函数式环境记录项，继承自declative Environment Record

* 执行函数时产生
* 提供this、super，记录参数和顶层标志符

### 特定内部状态

| 内部状态 | 类型 | 描述 |
| --- | --- | --- |
| [[ThisValue]] | Any | 函数的this值 |
| [[ThisBindingStatus]] | lexical &#x7c; initialized &#x7c; uninitialized | thisd lexical |

## module Environment Record

模块式环境记录项

* 执行模块时产生
* 记录模块的import值和顶层标志符
* [[OuterEnv]]为global Environment Record

## object Environment Record

对象式环境记录项，继承自Environment Record

* 执行with等语句时产生，只绑定可变标志符
* 有一个绑定对象，标志符绑定操作等价于绑定对象的属性操作

### 特定内部状态

| 内部状态 | 类型 | 描述 |
| --- | --- | --- |
| [[BindingObject]] | Object | 当前环境记录项的绑定对象 |
| [[IsWithEnvironment]] | Boolean | 是否是with语句产生的环境 |

### 特定内部方法

#### HasBinding(N)

* N不是绑定对象的属性，返回false
* N是绑定对象是属性
 * 不是with语句环境时，返回true
 * 是with语句环境且N不在绑定对象的Symbol.unscopables中，返回true

#### CreateMutableBinding(N, D)

* 设置属性的属性描述符为{[[Value]]: undefined, [[Writable]]: true, [[Enumerable]]: true, [[Configurable]]: D}

#### CreateImmutableBinding(N, S)

不能使用

#### InitializeBinding(N, V)

* SetMutableBinding(N, V, false)

#### SetMutableBinding(N, V, S)

* N不是绑定对象的属性，S为true时抛出ReferenceError
* N是绑定对象是属性，设置属性为V

#### GetBindingValue(N, S)

* N不是绑定对象的属性
 * S为true时抛出ReferenceError
 * S为false时，返回undefined
* N是绑定对象是属性，获取属性

#### DeleteBinding(N)

* 删除绑定对象属性

#### HasThisBinding()

* 返回false

#### HasSuperBinding()

* 返回false

#### WithBaseObject()

* 是with语句环境时返回绑定对象
* 不是with语句环境，返回undefined

## global Environment Record

全局环境记录项

* 执行全局代码时产生
* 有一个全局对象，标志符绑定操作等价于全局对象的属性操作
* [[OuterEnv]]为null

## 参考资料

* [ECMASCript Environment Records](https://tc39.es/ecma262/#sec-environment-records)
