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

## MOSFET特性

### MOSFET实际模型

* i<sub>G</sub>=0
* v<sub>G</sub>&lt;v<sub>T</sub>时，D端和S端开路，处于截止区域
* v<sub>G</sub>>=v<sub>T</sub>时，D端和S端连通
 * v<sub>DS</sub>&lt;v<sub>G</sub>-v<sub>T</sub>时，处于三极管区域，D端和S端相当于导通电阻R<sub>ON</sub>=R<sub>N</sub>L/W
 * v<sub>DS</sub>>=v<sub>G</sub>-v<sub>T</sub>时，处于饱和区域，D端和S端相当于压控电流源i<sub>DS</sub>=K(v<sub>GS</sub>-v<sub>T</sub>)<sup>2</sup>/2

![MOSFET实际模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-model.png)

### S模型

三极管区域模型，D端和S端为理想导体

* i<sub>G</sub>=0
* v<sub>G</sub>&lt;v<sub>T</sub>时，D端和S端开路，v<sub>DS</sub>=v<sub>S</sub>
* v<sub>G</sub>>=v<sub>T</sub>时，D端和S端短路，v<sub>DS</sub>=0

![S模型特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/S-model.png)

传递特性

* v<sub>S</sub>>=v<sub>OH</sub>>=v<sub>IH</sub>>=v<sub>T</sub>
* 0<=v<sub>OL</sub><=v<sub>IL</sub><=v<sub>T</sub>

![S模型静态分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/S-model-analysis.png)

### SR模型

三极管区域模型，D端和S端为线性电阻

* i<sub>G</sub>=0
* v<sub>G</sub>&lt;v<sub>T</sub>时，D端和S端开路，v<sub>DS</sub>=v<sub>S</sub>
* v<sub>G</sub>>=v<sub>T</sub>时，D端和S端存在导通电阻，v<sub>DS</sub>=v<sub>S</sub>R<sub>ON</sub>/(R<sub>ON</sub> + R<sub>L</sub>)

![SR模型特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SR-model.png)

传递特性

* v<sub>S</sub>>=v<sub>OH</sub>>=v<sub>IH</sub>>=v<sub>T</sub>
* v<sub>S</sub>R<sub>ON</sub>/(R<sub>ON</sub> + R<sub>L</sub>)<=v<sub>OL</sub><=v<sub>IL</sub><=v<sub>T</sub>

![SR模型静态分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SR-model-analysis.png)

### SCS模型

饱和区域模型

* i<sub>G</sub>=0
* v<sub>G</sub>&lt;v<sub>T</sub>时，D端和S端开路，i<sub>DS</sub>=0
* v<sub>G</sub>>=v<sub>T</sub>时，D端和S端为压控电流源，i<sub>DS</sub>=K(v<sub>GS</sub>-v<sub>T</sub>)<sup>2</sup>/2

![SCS模型特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SCS-model.png)

v-i特性

![SCS v-i特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SCS-vi.png)

## MOSFET逻辑门

* 约束输入使MOSFET位于截止区域和三极管区域
* 符合静态原则

### 缓冲器

* v&lt;v<sub>IL</sub>时，v<sub>OL</sub>/v<sub>IL</sub><1，信号衰减
* v>v<sub>IL</sub>且v&lt;v<sub>IH</sub>之间时，(v<sub>OH</sub> - v<sub>OL</sub>)/(v<sub>IH</sub> - v<sub>IL</sub>)>1，信号增益
* v>v<sub>IH</sub>时，(5 - v<sub>OH</sub>)/(5 - v<sub>IH</sub>)<1，信号衰减

![缓冲器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/buffer-transfer-characteristics.png)

### MOSFET反相器

电源、负载电阻、MOSFET串联

![MOSFET反相器](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-NOT.png)

传递特性

* v&lt;v<sub>IL</sub>时，(5 - v<sub>OH</sub>)/v<sub>IL</sub><1，信号衰减
* v>v<sub>IL</sub>且v&lt;v<sub>IH</sub>之间时，(v<sub>OH</sub> - v<sub>OL</sub>)/(v<sub>IH</sub> - v<sub>IL</sub>)>1，信号增益
* v>v<sub>IH</sub>时，v<sub>OL</sub>/(5 - v<sub>IH</sub>)<1，信号衰减

![反相器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/inverter-transfer-characteristics.png)

### MOSFET与非门

多个MOSFET串联

![MOSFET与非门](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-NAND.png)

### MOSFET或非门

多个MOSFET并联

![MOSFET或非门](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-NOR.png)

## 参考资料

* 《模拟和数字电子电路基础》
