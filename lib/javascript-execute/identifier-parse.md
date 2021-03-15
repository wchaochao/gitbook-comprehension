# 标志符解析

标签（空格分隔）： 理解

---

## 理解

沿着作用域链查找标志符

* 在当前作用域查找标志符
 * 可以找到，返回标志符的值
 * 找不到，继续查找外层作用域
* 所有外层作用域都找不到，报错

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

### 标志符绑定

| Method | Purpose |
| --- | --- |
| HasBind(N) | 是否绑定了标志符N |
| CreateMutableBinding(N, D) | 创建可变绑定，未初始化 |
| CreateImmutableBinding(N, S) | 创建不可变绑定，未初始化 |
| InitializeBinding(N, V) | 初始化绑定的标志符 |
| SetMutableBinding(N, V, S) | 设置可变绑定的值 |
| GetBindValue(N, S) | 获取绑定标志符的值 |
| DeleteBinding(N) | 删除绑定 |
| HasThisBinding() | 是否绑定了this |
| HasSuperBinding() | 是否绑定了super |
| WithBaseObject() | 绑定对象 |

## declarative Environments Records

声明式环境记录项

* 由函数、变量声明、cause语句等产生

### function Environment Record

函数式环境记录项

* 由函数产生
* 记录函数中的this、参数、super和顶层标志符

### module Environment Record

模块式环境记录项

* 有模块产生
* 记录模块中的import值和顶层标志符

## object Environment Record

对象式环境记录项

* 由with语句产生
* 有一个绑定对象，标志符绑定操作等价于绑定对象的属性操作

## global Environment Record

全局环境记录项

* 由全局代码产生
* 有一个全局对象，标志符绑定操作等价于全局对象的属性操作

## 参考资料

* [ECMASCript Environment Records](https://tc39.es/ecma262/#sec-environment-records)
