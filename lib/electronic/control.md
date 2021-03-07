# 控制元件

标签（空格分隔）： 理解

---

## 开关

### 开关模型

* 控制
* 输入
* 输出

![开关模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/switch-model.png)

### 开关特性

* 控制为0时，开关断开，$i=0$
* 控制为1时，开关联通，$v=0$

![开关特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/switch-characteristic.png)

### 开关逻辑门

* 开关+电源电阻：反相器
* 开关串联+电源电阻：与非门
* 开关并联+电源电阻：或非门

## MOSFET开关

金属氧化物半导体场效应晶体管

### MOSFET组成

* 控制端：栅极G（gate）
* 输入端：漏极D（drain）
* 输出端：源极S（source）

![MOSFET组成](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-composition.png)

### MOSFET结构

栅极G施加正电压时，会吸引源极S中的电子到沟道表面

* $v_{GS}<v_T$时，源极S与漏极D之间断开
* $v_T<=v_{GS}<=v_T+v_k$时，源极S与漏极D之间相当于压控电流源
* $v_{GS}>v_T+v_k$时，源极S与漏极D之间相当于非线性电阻

![MOSFET结构](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-constructor.png)

![MOSFET结构2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-constructor-2.png)

### MOSFET分类

* N型半导体：源极S、漏极D为电子材料
* P型半导体：源极S、漏极D为空穴材料

## MOSFET模型

### SU模型

MOSFET开关的精确模型

* $i_{GS}=0$
* $v_{GS}<v_T$时，D端和S端开路，处于截止区域
* $v_{GS}>=v_T$时，D端和S端连通
 * $v_{DS}<v_{GS}-v_T$时，处于三极管区域，D端和S端相当于非线性电阻$i_{DS}=K[(v_{GS}-v_T)v_{DS}-\frac{v_{DS}^2}{2}]$
 * $v_{DS}>=v_{GS}-v_T$时，处于饱和区域，D端和S端相当于压控电流源$i_{DS}=\frac{K(v_{GS}-v_T)^2}{2}$

v-i特性

![MOSFET v-i特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-model.png)

传递特性

![MOSFET传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-model-analysis.png)

### S模型

三极管区域模型，D端和S端为理想导体

* $i_G=0$
* $v_{GS}<v_T$时，D端和S端开路，$v_{DS}=v_S$
* $v_{GS}>=v_T$时，D端和S端短路，$v_{DS}=0$

![S模型特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/S-model.png)

v-i特性

![S模型v-i特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/S-model-vi.png)

传递特性

* $v_S>=v_{OH}>=v_{IH}>=v_T$
* $0<=v_{OL}<=v_{IL}<=v_T$

![S模型静态分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/S-model-analysis.png)

### SR模型

三极管区域模型，D端和S端为线性电阻

* $i_G=0$
* $v_{GS}<v_T$时，D端和S端开路，$v_{DS}=v_S$
* $v_{GS}>=v_T$时，D端和S端存在导通电阻，$v_{DS}=v_S\frac{R_{ON}}{R_{ON}+R_L}$

![SR模型特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SR-model.png)

v-i特性

![SR模型v-i特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SR-model-vi.png)

传递特性

* $v_S>=v_{OH}>=v_{IH}>=v_T$
* $v_S\frac{R_{ON}}{R_{ON}+R_L}<=v_{OL}<=v_{IL}<=v_T$

![SR模型静态分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SR-model-analysis.png)

### SCS模型

饱和区域模型

* $i_G=0$
* $v_{GS}<v_T$时，D端和S端开路，$i_{DS}=0$
*  $v_{GS}>=v_T$时，D端和S端为压控电流源，$i_{DS}=\frac{K(v_{GS}-v_T)^2}{2}$

![SCS模型特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SCS-model.png)

v-i特性

![SCS模型v-i特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SCS-vi.png)

传递特性

![SCS模型传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/SCS-model-analysis.png)

## MOSFET逻辑门

* MOSFET符合S模型或SR模型
* 符合静态原则

### 缓冲器

电源、负载电阻、MOSFET串联

![MOSFET缓冲器](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-buffer.png)

传递特性

* $v<v_{IL}$时，$\frac{v_{OL}}{v_{IL}}<1$，信号衰减
* $v_{IL}<v<v_{IH}$时，$\frac{v_{OH}-v_{OL}}{v_{IH}-v_{IL}}>1$，信号增益
* $v>v_{IH}$时，$\frac{5-v_{OH}}{5-v_{IH}}<1$，信号衰减

![缓冲器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/buffer-transfer-characteristics.png)

### MOSFET反相器

电源、负载电阻、MOSFET串联

![MOSFET反相器](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-NOT.png)

传递特性

* $v<v_{IL}$时，$\frac{5-v_{OH}}{v_{IL}}<1$，信号衰减
* $v_{IL}<v<v_{IH}$时，$\frac{v_{OH}-v_{OL}}{v_{IH}-v_{IL}}>1$，信号增益
* $v>v_{IH}$时，$\frac{v_{OL}}{5-v_{IH}}<1$，信号衰减

![反相器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/inverter-transfer-characteristics.png)

### MOSFET与非门

多个MOSFET串联

![MOSFET与非门](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-NAND.png)

### MOSFET或非门

多个MOSFET并联

![MOSFET或非门](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-NOR.png)

## BJT开关

双极结晶体管

### BJT组成

* 控制端：基极B
* 输入端：集电极C
* 输出端：发射极E

![BJT组成](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-composition.png)

### BJT特性

* $i_B=0$时，C端与E端断开，处于截止区域
* $i_B>0$时，C端与E端连通
 * $v_{CE}<=0.2V$时，处于饱和区域，C端与E端之间等价于电阻
 * $v_{CE}>0.2V$时，处于放大区域，C端与E端之间等价于流控电流源

![BJT特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-characteristic.png)

### BJT分段线性模型

* $i_B=0$时，两个二极管断开，C端与E端断开
* $i_B>0$且$v_{CE}>0.2V$时，BC之间的二极管断开，BE之间的二极管连通，$i_C=βi_B，i_E=(1+β)i_B$，β一般为100
* $i_B>0$且$v_{CE}=0.2V$时，两个二极管都连通，C端与E端短路

![BJT分段线性模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-segment-model.png)

v-i特性

![BJT分段线性模型v-i特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-segment-model-vi.png)

传递特性

![BJT放大器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-amplifier-analysis.png)

## 参考资料

* 《模拟和数字电子电路基础》
