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

### 小信号模型

![MOSFET放大器小信号电路模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-small-singal-model.png)

### 增量分析

* 输出电流增量分析：i<sub>d</sub>=K(V<sub>I</sub>-V<sub>T</sub>)v<sub>i</sub>，增量跨导g<sub>m</sub>=K(V<sub>1</sub>-V<sub>T</sub>)
* 输出电压增量分析：v<sub>o</sub>=-R<sub>L</sub>i<sub>d</sub>=-R<sub>L</sub>g<sub>m</sub>v<sub>i</sub>
* 小信号增益：A=v<sub>o</sub>/v<sub>i</sub>=-g<sub>m</sub>R<sub>L</sub>

![MOSFET放大器小信号分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-small-singal.png)

### 增量参数

增量输入电阻：输入电压变化与输入电流变化之比，为无穷大

![增量输入电阻](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/incremental-input-resistance.png)

增量输出电阻：输出电压变化与输出电流变化之比，为R<sub>L</sub>

![增量输出电阻](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/incremental-output-resistance.png)

增量电流增益：对于给定外部负载电阻，输出电流和输入电流之比，为-g<sub>m</sub>(R<sub>L</sub>||R<sub>O</sub>)R<sub>i</sub>/R<sub>o</sub>

![电流增益](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/incremental-i-gain.png)

增量功率增益：对于给定外部负载，输出功率和输入功率之比，为[-g<sub>m</sub>(R<sub>L</sub>||R<sub>O</sub>)]<sup>2</sup>R<sub>i</sub>/R<sub>o</sub>

### 工作点

* 输入工作点电压符合饱和原则
* 输入工作点电压越大小信号增益越大
* 输出工作点电压符合下一级输入工作点电压

## BJT放大器

### 组成

约束输入使BJT开关位于放大区域

![BJT放大器](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-amplifier.png)

![BJT放大器等效电路](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-amplifier-circuit.png)

### 传递特性

* v<sub>o</sub>=V<sub>S</sub>-i<sub>C</sub>R<sub>L</sub>
* i<sub>C</sub>=βi<sub>B</sub>
* i<sub>B</sub>=(v<sub>IN</sub>-0.6)/R<sub>1</sub>
* v<sub>IN</sub>>=0.6且v<sub>o</sub>0.2

![BJT放大器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-amplifier-analysis.png)

## 差分放大器

### 组成

![差分放大器](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/differential-amplifier.png)

### 传递特性

* 输出电压：v<sub>o</sub>=A<sub>D</sub>v<sub>D</sub>+A<sub>C</sub>v<sub>C</sub>
* 差模成分：v<sub>D</sub>=v<sub>A</sub>-v<sub>B</sub>，表示有用信号
* 共模成分：v<sub>C</sub>=(v<sub>A</sub>+v<sub>B</sub>)/2，表示噪声信号
* 共模抑制比：CMRR=A<sub>D</sub>/A<sub>C</sub>

### 源极耦合对

由一对匹配晶体管构成

![源极耦合对](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/source-coupled-pair.png)

### 差模模型

* v<sub>x</sub>=-g<sub>m</sub>R<sub>L</sub>v<sub>d</sub>/2
* v<sub>y</sub>=g<sub>m</sub>R<sub>L</sub>v<sub>d</sub>/2
* v<sub>o</sub>=v<sub>x</sub>-v<sub>y</sub>=-g<sub>m</sub>R<sub>L</sub>v<sub>d</sub>
* A<sub>D</sub>=v<sub>o</sub>/v<sub>d</sub>=-g<sub>m</sub>R<sub>L

![差模模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/differential-model.png)

### 共模模型

* v<sub>x</sub>=-R<sub>L</sub>v<sub>c</sub>/2R<sub>i</sub>
* v<sub>y</sub>=-R<sub>L</sub>v<sub>c</sub>/2R<sub>i</sub>
* v<sub>o</sub>=v<sub>x</sub>-v<sub>y</sub>=0
* A<sub>C</sub>=0

![共模模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/common-model.png)
