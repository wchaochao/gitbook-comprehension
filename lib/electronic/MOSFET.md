# MOSFET开关

标签（空格分隔）： 理解

---

## 开关

### 开关模型

* 控制
* 输入
* 输出

![开关模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/switch-model.png)

### 开关特性

* 控制为0时，开关断开，i=0
* 控制为1时，开关联通，v=0

![开关特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/switch-characteristic.png)

### 开关逻辑门

* 开关串联：逻辑与
* 开关并联：逻辑或

## MOSFET开关

金属氧化物半导体场效应晶体管

### MOSFET组成

* 控制端：栅极G（gate）
* 输入端：漏极D（drain）
* 输出端：源极S（source）

![MOSFET组成](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-composition.png)

### MOSFET结构

* 栅极G加正电压时，会吸引源极S中的电子到沟道表面
* 栅极G的电压大于v<sub>T</sub>时，源极S与漏极D之间连通

![MOSFET结构](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-constructor.png)

![MOSFET结构2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-constructor-2.png)

### MOSFET分类

* N型半导体：源极S、漏极D为电子材料
* P型半导体：源极S、漏极D为空穴材料

## MOSFET逻辑门

### MOSFET反相器

电源、负载电阻、MOSFET串联

![MOSFET反相器](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-NOT.png)

### MOSFET与非门

多个MOSFET串联

![MOSFET与非门](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-NAND.png)

### MOSFET或非门

多个MOSFET并联

![MOSFET或非门](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-NOR.png)

## S模型

源极S与漏极D之间为理想导体

### S模型特性

* i<sub>G</sub>=0
* v<sub>G</sub>小于v<sub>T</sub>时，D端和S端开路，v<sub>DS</sub>=v<sub>S</sub>
* v<sub>G</sub>大于等于v<sub>T</sub>时，D端和S端短路，v<sub>DS</sub>=0

![S模型特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/S-model.png)

### S模型静态分析

* v<sub>S</sub>>=v<sub>OH</sub>>=v<sub>IH</sub>>=v<sub>T</sub>
* 0<=v<sub>OL</sub><=v<sub>IL</sub><=v<sub>T</sub>

![S模型静态分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/S-model-analysis.png)

## SR模型

v<sub>DS</sub><=v<sub>G</sub>-v<sub>T</sub>时，源极S与漏极D之间有导通电阻R<sub>ON</sub>=R<sub>N</sub>L/W

* W/L增大时，导通电阻减小

### SR模型特性

* i<sub>G</sub>=0
* v<sub>G</sub>小于v<sub>T</sub>时，D端和S端开路，v<sub>DS</sub>=v<sub>S</sub>
* v<sub>G</sub>大于等于v<sub>T</sub>时，D端和S端存在导通电阻，v<sub>DS</sub>=v<sub>S</sub>R<sub>ON</sub>/(R<sub>ON</sub> + R<sub>L</sub>)

![SR模型特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SR-model.png)

### SR模型静态分析

* v<sub>S</sub>>=v<sub>OH</sub>>=v<sub>IH</sub>>=v<sub>T</sub>
* v<sub>S</sub>R<sub>ON</sub>/(R<sub>ON</sub> + R<sub>L</sub>)<=v<sub>OL</sub><=v<sub>IL</sub><=v<sub>T</sub>

![SR模型静态分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SR-model-analysis.png)

## 信号重构

* v<sub>IH</sub> - v<sub>IL</sub>尽可能小
* v<sub>OH</sub> - v<sub>OL</sub>尽可能大

### 缓冲器传递特性

* v小于v<sub>IL</sub>时，v<sub>OL</sub>/v<sub>IL</sub><1，信号衰减
* v在v<sub>IL</sub>、v<sub>IH</sub>之间时，(v<sub>OH</sub> - v<sub>OL</sub>)/(v<sub>IH</sub> - v<sub>IL</sub>)>1，信号增益
* v大于v<sub>IH</sub>时，(5 - v<sub>OH</sub>)/(5 - v<sub>IH</sub>)<1，信号衰减

![缓冲器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/buffer-transfer-characteristics.png)

### 反相器传递特性

* v小于v<sub>IL</sub>时，(5 - v<sub>OH</sub>)/v<sub>IL</sub><1，信号衰减
* v在v<sub>IL</sub>、v<sub>IH</sub>之间时，(v<sub>OH</sub> - v<sub>OL</sub>)/(v<sub>IH</sub> - v<sub>IL</sub>)>1，信号增益
* v大于v<sub>IH</sub>时，v<sub>OL</sub>/(5 - v<sub>IH</sub>)<1，信号衰减

![反相器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/inverter-transfer-characteristics.png)

## 参考资料

* 《模拟和数字电子电路基础》
