# 放大器

标签（空格分隔）： 理解

---

## MOSFET放大器

### 组成

MOSFET符合SCS模型

![MOSFET放大器](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier.png)

### 传递特性

* $v_o=V_S-i_DR_L$
* $i_D=\frac{K(v_{IN}-v_T)^2}{2}$
* $v_{IN}>v_T$且$v_o>=v_{IN}-v_T$

![MOSFET放大器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-analysis.png)

![MOSFET放大器传递特性2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-analysis-2.png)

### 饱和原则

约束输入使符合饱和原则

* 有效输入电压范围：$v_T \sim v_T+v_k$，$v_k=\frac{-1+\sqrt{1+2V_SR_LK}}{R_LK}$
* 有效输出电压范围：$v_k \sim V_S$
* 有效输出电流范围：$0 \sim \frac{Kv_k^2}{2}$

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

* 输出电流增量分析：$i_d=K(V_I-V_T)v_i$，增量跨导$g_m=K(V_I-V_T)$
* 输出电压增量分析：$v_o=-R_Li_d=-R_Lg_mv_i$
* 小信号增益：$A=\frac{v_o}{v_i}=-g_mR_L$

![MOSFET放大器小信号分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-amplifier-small-singal.png)

### 增量参数

增量输入电阻：输入电压变化与输入电流变化之比，为无穷大

![增量输入电阻](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/incremental-input-resistance.png)

增量输出电阻：输出电压变化与输出电流变化之比，为R<sub>L</sub>

![增量输出电阻](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/incremental-output-resistance.png)

增量电流增益：对于给定外部负载电阻，输出电流和输入电流之比，为$-g_m(R_L||R_O)\frac{R_i}{R_o}$

![电流增益](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/incremental-i-gain.png)

增量功率增益：对于给定外部负载，输出功率和输入功率之比，为$[g_m(R_L||R_O)]^2\frac{R_i}{R_o}$

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

* $v_o=V_S-i_CR_L$
* $i_C=βi_B$
* $i_B=\frac{v_{IN}-0.6}{R_I}$
* $v_{IN}>=0.6$且$v_o>0.2$

![BJT放大器传递特性](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-amplifier-analysis.png)

## BJT小信号放大器

### 小信号模型

![BJT小信号放大器模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-amplifier-small-singal-model.png)

### 增量分析

* 输出电流增量分析：$i_c=βi_b$
* 输出电压增量分析：$v_o=-i_cR_L=-βi_bR_L=-βR_L\frac{v_i}{R_I}$
* 小信号增益：$A=\frac{v_o}{v_i}=-β\frac{R_L}{R_I}$

### 增量参数

* 增量输入电阻：${R_I}$
* 增量输出电阻：${R_L}$
* 增量电流增益：$-β\frac{R_L||R_{OUT}}{R_{OUT}}$
* 增量功率增益：$\frac{[β(R_L||R_{OUT}]^2}{R_IR_{OUT}}$

![BJT增量电阻](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-incremental-resistance.png)

![BJT增量电流增益](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/BJT-incremental-i-gain.png)

## 差分放大器

### 组成

![差分放大器](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/differential-amplifier.png)

### 传递特性

* 输出电压：$v_o=A_Dv_D+A_Cv_C$
* 差模成分：$v_D=v_A-v_B$，表示有用信号
* 共模成分：$v_C=\frac{v_A+v_B}{2}$，表示噪声信号
* 共模抑制比：$CMRR=\frac{A_D}{A_C}$

### 源极耦合对

由一对匹配晶体管构成

![源极耦合对](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/source-coupled-pair.png)

### 差模模型

* $v_x=\frac{-g_mR_Lv_d}{2}$
* $v_y=\frac{g_mR_Lv_d}{2}$
* $v_o=v_x-v_y=-g_mR_Lv_d$
* $A_D=\frac{v_o}{v_d}=-g_mR_L$

![差模模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/differential-model.png)

### 共模模型

* $v_x=\frac{-R_Lv_c}{2R_i}$
* $v_y=\frac{-R_Lv_c}{2R_i}$
* $v_o=v_x-v_y=0$
* $A_C=0$

![共模模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/common-model.png)

## 参考资料

* 《模拟和数字电子电路基础》
