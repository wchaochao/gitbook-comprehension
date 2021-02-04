# 放大器

标签（空格分隔）： 理解

---

## MOSFET放大器

### 组成

MOSFET符合SCS模型

![MOSFET放大器](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier.png)

### 传递特性

* v<sub>o</sub>=V<sub>S</sub>-i<sub>D</sub>R<sub>L</sub>
* i<sub>D</sub>=K(v<sub>IN</sub>-v<sub>T</sub>)<sup>2</sup>/2
* v<sub>IN</sub>>v<sub>T</sub>且v<sub>o</sub>>=v<sub>IN</sub>-v<sub>T</sub>

![MOSFET放大器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-analysis.png)

![MOSFET放大器传递特性2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-analysis-2.png)

### 饱和原则

约束输入使符合饱和原则

* 有效输入电压范围：v<sub>T</sub> ~ v<sub>T</sub>+v<sub>k</sub>，v<sub>k</sub>=(-1+根号(1+2V<sub>S</sub>R<sub>L</sub>K))/R<sub>L</sub>K
* 有效输出电压范围：v<sub>k</sub> ~ V<sub>S</sub>
* 有效输出电流范围：0 ~ Kv<sub>k</sub><sup>2</sup>/2

![MOSFET放大器饱和原则1](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-constraint-1.png)

![MOSFET放大器饱和原则2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-constraint-2.png)

### 偏置

通过偏置电压使小信号位于MOSFET放大器的有效区域

![MOSFET放大器偏置电路](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-bias-1.png)

![MOSFET放大器偏置分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-bias-2.png)

## MOSFET小信号放大器

### 增量分析

* 输出电流增量分析：i<sub>d</sub>=K(V<sub>1</sub>-V<sub>T</sub>)v<sub>i</sub>，增量跨导g<sub>m</sub>=K(V<sub>1</sub>-V<sub>T</sub>)
* 输出电压增量分析：v<sub>o</sub>=-R<sub>L</sub>i<sub>d</sub>=-R<sub>L</sub>g<sub>m</sub>v<sub>i</sub>
* 小信号增益：A=v<sub>o</sub>/v<sub>i</sub>=-g<sub>m</sub>R<sub>L</sub>

![MOSFET放大器小信号分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-small-singal.png)

## BJT放大器

### 组成

约束输入使BJT开关位于放大区域

![BJT放大器](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-amplifier.png)

### 等效电路

![BJT放大器等效电路](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-amplifier-circuit.png)

### 传递特性

* v<sub>o</sub>=V<sub>S</sub>-i<sub>C</sub>R<sub>L</sub>
* i<sub>C</sub>=βi<sub>B</sub>
* i<sub>B</sub>=(v<sub>IN</sub>-0.6)/R<sub>1</sub>
* v<sub>IN</sub>>=0.6且v<sub>o</sub>0.2

![BJT放大器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-amplifier-analysis.png)
