# 对象

标签（空格分隔）： 理解

---

## 理解

属性的集合，一切皆对象

* 普通对象：拥有通用内部状态和通用内部方法的对象
* 特定对象：拥有特定内部状态和特定内部方法的对象

## 属性

key/value对

### 组成

* key：属性名，可为String值（普通字符串、标志符名、索引）和Symbol值
* value：属性值，可为任意值（为函数时称为方法）

### 分类

* 自身属性：对象自身的属性
* 继承属性：对象通过原型链继承的属性

## 属性描述符

属性的描述信息

### 数据属性

属性值由`[[value]]`决定

| 属性描述 | 类型 | 默认值 | 描述 |
| --- | --- | --- | --- |
| [[Value]] | any | undefined | 属性值 |
| [[Writable]] | Boolean | false | 属性值是否可写 |
| [[Enumerable]] | Boolean | false | 属性是否可枚举，为true时可在`for/in, Object.keys, JSON.stringify`中遍历 |
| [[Configurable]] | Boolean | false | 属性是否可配置，为false时属性不可删除、不可改为访问器属性、其他属性描述不能修改（[[Writable]]为true时，[[Value]]可修改，[[Writable]]可由true改为false） |

```javascript
let obj = {}

obj.defineProperty('a', {
  value: 1,
  writable: true,
  enumberable: true,
  configurable: true
})
```

### 访问器属性

属性值由`get/set`函数决定

| 属性描述 | 类型 | 默认值 | 描述 |
| --- | --- | --- | --- |
| [[Get]] | Function &#x7c; Undefined | undefined | 获取属性时执行的函数，参数为空，返回值为属性值 |
| [[Set]] | Function &#x7c; Undefined | undefined | 设置属性时执行的函数，参数为设置的值 |
| [[Enumerable]] | Boolean | false | 属性是否可枚举，为true时可在`for/in, Object.keys, JSON.stringify`中遍历 |
| [[Configurable]] | Boolean | false | 属性是否可配置，为false时属性不可删除、不可改为数据属性、其他属性描述不能修改 |

```javascript
let obj = {
  _a: 1
}

obj.defineProperty('a', {
  get: function () {return this._a},
  set: function (val) {this._a = val},
  enumberable: true,
  configurable: true
})
```

## 通用内部状态

| 内部状态 | 类型 | 描述 |
| --- | --- | --- |
| [[Prototype]] | Object &#x7c; Null | 对象的原型对象 |
| [[Extensible]] | Boolean | 对象是否可扩展 |

## 通用内部方法

| 内部方法 | 类型 | 描述 |
| --- | --- | --- |
| [[GetPrototypeOf]] | () -> Object &#x7c; Null | 获取对象原型 |
| [[SetPrototypeOf]] | (Object &#x7c; Null) -> Boolean | 设置对象的原型 |
| [[IsExtensible]] | () -> Boolean | 对象是否可扩展，为false时不能添加属性、不能修改原型 |
| [[PreventExtensions]] | () -> Boolean | 阻止对象扩展 |
| [[GetOwnProperty]] | (propertyKey) -> Property Descriptor &#x7c; Undefined | 获取对象自身属性的属性描述符 |
| [[DefineOwnProperty]] | (propertyKey, propertyDescriptor) -> Boolean | 创建或设置对象自身属性的属性描述符 |
| [[HasProperty]] | (propertyKey) -> Boolean | 是否是对象属性（自身属性或继承属性） |
| [[Get]] | (propertyKey, Receiver) -> any | 获取对象属性的属性值，Receiver为访问器函数的this值 |
| [[Set]] | (propertyKey, value, Receiver) -> Boolean | 设置对象属性的属性值，Receiver为访问器函数的this值 |
| [[Delete]] | () -> Boolean | 删除对象自身属性 |
| [[OwnPropertyKeys]] | () -> List of propertyKey | 获取对象自身属性的属性列表 |

### [[SetPrototypeOf]] (V)

* [[Extensible]]为false时，不能设置原型
* 对象在V的原型链上时，不能设置原型

### [[DefineOwnProperty]] (P, Desc)

* P不是对象自身属性时，创建自身属性，属性描述符为补充完整的Desc
* P时对象自身属性时，修改自身属性的属性描述符
 * P为数据属性且[[Configurable]]为false时，除[[Writable]]为true时，[[Value]]可修改，[[Writable]]可由true改为false，其他情况都不能修改
 * P为访问器属性且[[Configurable]]为false时，不能修改

### [[HasProperty]] (P)

* P是对象自身属性时，返回true
* P不是对象自身属性时，沿着原型链查找
 * 能查到，返回true
 * 不能查到，返回false

### [[Get]] (P, Receiver)

* P是对象自身属性时
 * P是数据属性，返回[[Value]]
 * P是访问器属性，调用[[Get]]，this为Receiver
* P不是对象自身属性时，沿着原型链查找
 * 能查到，同自身属性处理
 * 不能查到，返回undefined

### [[Set]] (P, Receiver)

## 参考资料

* [ECMAScript Object Type](https://tc39.es/ecma262/#sec-object-type)
