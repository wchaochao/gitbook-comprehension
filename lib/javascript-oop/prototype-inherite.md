# 原型继承

标签（空格分隔）： 理解

---

## 理解

每个对象都有原型对象，对象可从原型对象中继承属性

* 原型对象的数据属性可以被对象获取
* 原型对象的访问器属性可以被对象获取和设置

## 原型

* 任一构造函数都有原型属性，通过该构造函数创建的对象继承该原型
* 可以通过Object.setPrototypeof()、Object.create()方法设置原型

## 原型链

原型对象也是一个对象，也会有自己的原型，形成原型链

* 原型链是有限长度的，最终都指向null，不能形成循环原型链

```javascript
arr -> Array.prototype -> Object.prototype -> null
Array -> Function.prototype -> Object.prototype -> null
```

## 属性获取

* 在当前对象中查找属性
 * 查找到，获取该属性
 * 查找不到，继续沿着原型链查找
* 在原型链上查找到属性，获取该属性
* 在原型链上查找不到属性，返回undefined

## 属性设置

* 在当前对象中查找属性
 * 查找到，设置该属性
 * 查找不到，继续沿着原型链查找
* 在原型链上查找到属性
 * 为数据属性，该原型属性不能设置，会创建对象自身属性
 * 为访问器属性，该原型属性可以设置
* 在原型链上查找不到属性，设置时创建新的自身属性