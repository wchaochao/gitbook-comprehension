# 线性电路分析

标签（空格分隔）： 理解

---

## 一般分析

### 解方程组

* 标注支路电压、支路电流
* 列B个元件方程，B为元件数
* 列N-1个KCL方程，N为节点数
* 列B-N+1个KVL方程
* 解线性方程组

### 一般分析实例

* 单电阻电路：$v=iR$
* 分压器：理想电压源+电阻串联
 * 等效电阻等于各电阻之和$R=R_1+R_2+...+R_N$
 * $i=\frac{V}{R}$
 * $v_1=iR_1，v_2=iR_2...$，电压按电阻分压
* 分流器：理想电流源+电阻并联
 * 等效电容等于各电容之和$G=G_1+G_2+...G_N$
 * $v=\frac{I}{G}$
 * $i_1=vG_1, i_2=vG_2...$，电流按电容分流
 * 两电阻并联，等效电阻为$\frac{R1R2}{R1+R2}$
 * N个相同电阻并联，等效电阻为$\frac{R}{N}$
* 受控电路：输入电路、输出电路独立分析

## 直觉分析

电路合并法

* 电阻串联等价于一个等效电阻，电阻为各电阻之和
* 电阻并联等价于一个等效电容，电容为各电容之和
* 电压源串联等价于一个等效电压源，电压为各电压之和
* 电流源并联等价于一个等效电流源，电流为各电流之和

## 节点分析

简化一般分析

### 节点电压

节点相对于参考节点（地节点）的电压

### 节点法

* 选择地节点，一般为连接元件多的或连接电源多的
* 标注其他节点电压
* 列KCL方程，求节点电压
* 根据节点电压求支路电压、支路电流

### 特殊处理

* 浮动独立电压源：未与地相连的电压源，需要将两个接口当作一个超节点处理
* 受控源：将受控源当作独立源处理，最后再根据受控源的元件定律求解

## 叠加分析

多源线性网络在某点的响应等于各独立源在该点的响应之和

### 叠加法

* 为每个独立源构成一个其他独立源置为0的电路，受控源不动
 * 电压源为0等效于短路
 * 电流源为0等效于开路
* 计算每个独立源单独作用的子响应
* 子响应叠加求得全响应

### 叠加分析实例

* 加法电路：多个电压+相同电阻并联，输出电压为各电压源的平均值

![加法电路](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/adding-circuit.png)

## 等效分析

简化线性网络

### 戴维南定理

任意线性网络在一对给定接线端都可以抽象为一个电压源和一个电阻的串联，称为戴维南等效电路

* 电压源的电压为线性网络在给定接线端的开路电压，$v_{oc}=v_t|_{i_{test}=0}$
* 电阻为线性网络独立源置为0时的等效电阻，$R_t=\frac{v_t}{i_{test}}|_{internal\ source=0}$
* 接线端的元件特性为$v_t=v_{oc}+i_{test}R_t$

![戴维南等效电路](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/Thevenin-circuit.png)

### 诺顿定理

任意线性网络在一对给定接线端都可以抽象为一个电流源和一个电阻的并联，称为诺顿等效电路

* 电流源的电流为线性网络在给定接线端的短路，$i_{sc}=i_t|_{v_{test}=0}$
* 电阻为线性网络独立源置为0时的等效电阻，$R_t=\frac{v_{test}}{i_t}|_{internal\ source=0}$
* 接线端的元件特性为$i_t=-i_{sc}+\frac{v_{test}}{R_t}，R_t=\frac{v_{oc}}{i_{sc}}$

![诺顿等效电路](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/Norton-circuit.png)

### 等效分析实例

* 桥接电路：(R1+R2)||(R4+R5)，中间连一个R3，对R3两端进行等效分析

![桥接电路](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/bridge-circuit.png)

![桥接电路分析](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/bridge-circuit-analysis.png)

## 参考资料

* 《模拟和数字电子电路基础》
