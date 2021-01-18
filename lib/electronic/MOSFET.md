# MOSFET开关

标签（空格分隔）： 理解

---

## 开关元件

### 模型

* 控制
* 输入
* 输出

### v-i曲线

* 控制为0，开关断开，i=0
* 控制为1，开关联通，v=0

### 逻辑门实现

* 开关串联：逻辑与
* 开关并联：逻辑或

## MOSFET元件

### 组成

* 控制端：栅极G（gate）
* 输入端：漏极D（drain）
* 输出端：源极S（source）

### S模型

* i<sub>G</sub>=0
* v<sub>G</sub>小于v<sub>T</sub>时，D端和S端开路，i<sub>DS</sub>=0
* v<sub>G</sub>大于等于v<sub>T</sub>时，D端和S端短路，v<sub>DS</sub>=0

### 逻辑门实现

* 反相器：电源、负载电阻、MOSFET串联
* 与非门：多个MOSFET串联
* 或非门：多个MOSFET并联

## 参考资料

* 《模拟和数字电子电路基础》
