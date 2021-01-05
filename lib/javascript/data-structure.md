# 数据结构

标签（空格分隔）： 理解

---

## Iterator

迭代器

### 创建

```javascript
const iterable = {
  [Symbol.iterator] () {
    return {
      next () {
        return {
          done,
          value
        }
      }
    }
  }
}

const iterator = iterable[Symbol.iterator]()
```

### next方法

获取下一个迭代值

* 返回值为{value: any, done: boolean}

### for val of iterable

* 执行iterable[Symbol.iterator]()，获取iterator
* 执行iterator.next()
 * 返回值中的done属性为false时，val = value，继续循环
 * 返回值中的done属性为true时退出循环

### 数组处理

* Array.from(iterable)：转换为数组
* ...iterable：转换为数组再展开

### 原生Iterable

* String：自动处理多字节字符
* Array
* Arguments
* Generator

## 参考资料

* [JavaScript.info](https://javascript.info/)
