# 原型

标签（空格分隔）： 理解

---

## 理解

* 每个对象都有一个原型对象
* 对象通过原型实现继承

## 对象原型

* 通过Object.create(proto)方法创建的对象的原型为指定的proto
* 通过构造函数创建的对象的原型为Constructor.prototype

## 原型操作

* 获取对象原型：Object.getPrototypeOf(obj)
* 设置对象原型：Object.setPrototypeOf(obj, proto)

## 原型链

* 原型对象也是一个对象，也会有自己的原型，从而形成原型链
* 原型链是有限长度的，最终都指向null，不能形成循环原型链

```javascript
arr -> Array.prototype -> Object.prototype -> null
Array -> Function.prototype -> Object.prototype -> null
```

## 原型继承

对象可从原型对象中继承属性

* 原型对象的数据属性可以被对象获取
* 原型对象的访问器属性可以被对象获取和设置

### 属性获取

* 在当前对象中查找属性
 * 查找到，获取该属性
 * 查找不到，继续沿着原型链查找
* 在原型链上查找到属性，获取该属性
* 在原型链上查找不到属性，返回undefined

### 属性设置

* 在当前对象中查找属性
 * 查找到，设置该属性
 * 查找不到，继续沿着原型链查找
* 在原型链上查找到属性
 * 为数据属性，不能设置，会创建对象自身属性
 * 为访问器属性，可以调用Set方法设置
* 在原型链上查找不到属性，设置时创建新的自身属性
