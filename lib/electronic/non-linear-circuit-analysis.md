# 非线性电路分析

标签（空格分隔）： 理解

---

## 非线性元件

### 二极管元件

$I_D=I_s(e^{\frac{V_D}{V_{TH}}}-1)$

![二极管符号](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/diode.png)

![二极管特性曲线](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/diode-characteristic.png)

### 平方律元件

$I_{DS}=\frac{K(V_{DS}-V_T)^2}{2}，V_{DS}>=V_T$

![平方律元件](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/square-characteristic.png)

## 节点分析

对非线性元件进行节点分析

* DC、电阻、平方律元件串联：对平方律元件进行节点分析
* 线性网络、平方律元件串联：对平方律元件的接线端进行等效分析

## 图像分析

将节点分析的解方程转化为曲线的交点

* DC、电阻、二极管元件串联：进行节点分析，解方程组转化为二极管元件v-i特性曲线与直线的交点
* 半波滤波器：AC、电阻、二极管元件串联，输出电压只有AC的半波

## 分段线性分析

将非线性元件的v-i曲线分解为一系列线段进行分析

### 理想二级管

* 二极管开通：短路，$v_D=0，i_D>0$
* 二极管断开：断路，$i_D=0，v_D<0$

![理想二极管](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/ideal-diode.png)

## 增量分析

电路在一个工作点上对一个小扰动的响应是线性的，$x_B=f(x_A)$，则$x_B$在工作点$X_A$的增量变化为$x_b=\frac{df(x_A)}{dx_A}|_{x_A=X_A}x_a$

* 设小信号电源为0，得到DC子电路，根据非线性分析求工作点电流、电压
* 设DC电源为0，根据工作点电流、电压使用小信号模型替代元件，得到小信号子电路，根据线性分析求增量电流、增量电压

![增量分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/incremental-analysis.png)

### 小信号模型

* 理想电压源：短路
* 理想电流源：断路
* 理想线性电阻R：理想线性电阻R
* MOSFET放大器：压控电流源$i_{ds}=k(V_{GS}-V_T)v_{gs}$

![增量分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/small-signal-model.png)

### 增量分析实例

* 二极管稳压器：DC、AC、电阻、二极管串联，输出电压的AC、DC比减少

## 参考资料

* 《模拟和数字电子电路基础》
