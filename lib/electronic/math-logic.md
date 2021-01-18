# 数字逻辑

标签（空格分隔）： 理解

---

## 数值离散化

将一定范围内的信号值集总为一个值

### 二值化

* 将信号值集总为两个值，表示真假、高低、开关、1/0等概念
* 超过两个值时用多位二进制编码表示

### 静态原则

二值化规范

![二值化](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/static-principle.png)

## 布尔逻辑

### 布尔值

* 真、假
* 高、低
* 开、关
* 1、0

### 逻辑算子

* AND：用点号表示
* OR：用加号表示
* NOT：用横线或波浪线表示

### 真值表

列出所有输入、输出的可能值，表示数字逻辑

#### 与

都为真时才为真

| A | B | X |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

#### 或

有一个为真时为真

| A | B | X |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

#### 非

取反

| A | X |
| --- | --- |
| 0 | 1 |
| 1 | 0 |

#### 异或

不同时为真

| A | B | X |
| --- | --- | --- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

#### 与非

都为真时才为假

| A | B | X |
| --- | --- | --- |
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

#### 或非

有一个为真时为假

| A | B | X |
| --- | --- | --- |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |

### 逻辑门电路

符号静态规则、输出仅为输入的函数的电路，表示数字逻辑

![门电路](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-computer-composition/gate.png)

### 布尔表达式

乘积之和，表示数字逻辑

#### 真值表转换

将真值表转换为最小乘积之和的布尔表达式

* 对真值表中输出为1的所有输入项，1为真，0为非，乘积起来
* 将上述项相加

#### 布尔表达式简化

使用布尔恒等式将布尔表达式简化为最小乘积之和形式

![布尔恒等式](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-computer-composition/boolean-identity.png)

#### 门电路简化

使用与非门或或非门表示其他门

![门转换1](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-computer-composition/gate-convert-1.png)

![门转换2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-computer-composition/gate-convert-2.png)

## 二进制

### 定义

* 每一位只能为0或1
* 逢二进一

### 转换

* 二进制转换为十进制：A<sub>i</sub>2<sup>i</sup>求和，i从0开始
* 十进制转换为二进制：整数除二取余数，小数乘二取进位
* 二进制转换为八进制：每三位二进制表示为一位八进制
* 二进制转换为十六进制：每四位二进制表示为一位十六进制

### 负数

* 首位表示正负，0为正，1为负
* 正数与负数互为补码加一

### 加法

* 输入：两个加数、低位进位
* 输出：和、高位进位

## 参考资料

* 《模拟和数字电子电路基础》
