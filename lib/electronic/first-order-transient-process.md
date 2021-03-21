# 一阶暂态过程

标签（空格分隔）： 理解

---

## RC电路

### 电路分析

节点分析得
    $$0 = \frac{v_c - v_i}{R} + C\frac{dv_c}{dt}$$

写为非齐次线性一阶常微分方程
    $$\frac{dv_c}{dt} + \frac{v_c}{RC} = \frac{v_i}{RC}$$

全解为齐次解和特解之和
    $$\begin{cases} \frac{dv_{ch}}{dt} + \frac{v_{ch}}{RC} = 0 \\ \frac{dv_{cp}}{dt} + \frac{v_{cp}}{RC} = \frac{v_i}{RC} \end{cases}$$

* 齐次解为$v_{ch} = Ae^{st}$，代入齐次式得$s = -\frac{1}{\tau}$，时间常数$\tau=RC$
* 特解为$v_{cp}$由输入决定
* 全解为$v_c = Ae^{-\frac{t}{\tau}} + v_{cp}$，代入初始条件$v_c(0)$，得$A = v_c(0) - v_{cp}(0)$，
* 全解$v_c = v_c(0)e^{-\frac{t}{\tau}} + v_{cp} - v_{cp}(0)e^{-\frac{t}{\tau}}$，为零输入响应和零状态响应之和

### 阶跃输入

* 特解为$v_{cp} = V_1$，代入特解式得终值$V_1 = V$
* 全解为$v_c = Ae^{-\frac{t}{\tau}} + V_1$，$A = V_0 - V_1$，
* 全解$v_c = V_0e^{-\frac{t}{\tau}} + V_1(1 - e^{-\frac{t}{\tau}})$，为零输入响应和零状态响应之和
* 电流为$i_c = \frac{V_1 - V_0}{R}e^{-\frac{t}{\tau}}$

![串联RC](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/series-rc.png)

#### 图形分析

* $t = 0$时，曲线斜率为$-\frac{A}{\tau}$
* $t = \tau$时，曲线值为$\frac{A}{e} + V_1$
* $t = 5\tau$，曲线值接近$V_1$

### 方波输入

电容改变了输入方波的形状

* 时间常数远小于脉冲长度时，输出波形与输入波形相似
* 时间常数的5倍小于脉冲长度时，电容完成完整的充放电
* 时间常数RC远大于脉冲长度时，电容电压为输入电压的积分，$v_c = \frac{1}{\tau}\int_{0}^{t}v_idt$，接近于0

![串联RC-方波输入](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/series-rc-square.png)

#### 长脉冲

完成了完整的充放电

$$v_c = \begin{cases} V_p(1 - e^{-\frac{t}{RC}}) & 0 \leq t \leq t_p \\ V_pe^{-\frac{t - t_p}{RC}} & t \geqslant t_p \end{cases}$$

![串联RC-长脉冲](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/series-rc-long-pulse.png)

#### 窄脉冲

未能完成完整的充放电

$$v_c = \begin{cases} V_p(1 - e^{-\frac{t}{RC}}) & 0 \leq t \leq t_p \\ [V_p(1 - e^{-\frac{t_p}{RC}}]e^{-\frac{t - t_p}{RC}} & t \geqslant t_p \end{cases}$$

当$t_p << RC$时，进行指数展开得

$$v_c = \begin{cases} \frac{V_p}{RC}t & 0 \leq t \leq t_p \\ \frac{V_pt_p}{RC}e^{-\frac{t - t_p}{RC}} & t \geqslant t_p \end{cases}$$

![串联RC-窄脉冲](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/series-rc-narrow-pulse.png)

### 冲击输入

极限的窄脉冲

$$v_c = \frac{A}{RC}e^{-\frac{t}{RC}}$$

![串联RC-冲击输入](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/series-rc-impact.png)

### 斜坡输入

* 特解为$v_{cp} = K_2t + K_3$，代入特解式得终值$v_{cp} = S_1t - S_1RC$
* 全解为$v_c = Ae^{-\frac{t}{\tau}} + v_{cp}$，$A = V_0 + S_1RC$，
* 全解$v_c = V_0e^{-\frac{t}{\tau}} + S_1t - S_1RC + S_1RC e^{-\frac{t}{\tau}}$，为零输入响应和零状态响应之和

![串联RC-斜坡输入](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/series-rc-ramp.png)

## RL电路

### 电路分析

节点分析得
    $$i_LR + L\frac{di_L}{dt} = v_i$$

写为非齐次线性一阶常微分方程
    $$\frac{di_L}{dt} + \frac{i_LR}{L} = \frac{v_i}{L}$$

全解为齐次解和特解之和
    $$\begin{cases} \frac{di_{LH}}{dt} + \frac{i_{LH}R}{L} = 0 \\ \frac{di_{LP}}{dt} + \frac{i_{LP}R}{L} = \frac{v_i}{L} \end{cases}$$

* 齐次解为$i_{LH} = Ae^{st}$，代入齐次式得$s = -\frac{1}{\tau}$，时间常数$\tau=\frac{L}{R}$
* 特解为$i_{LP}$由输入决定
* 全解为$i_L = Ae^{-\frac{t}{\tau}} + i_{LP}$，代入初始条件$i_L(0)$，得$A = i_L(0) - i_{LP}(0)$，
* 全解$i_L = i_L(0)e^{-\frac{t}{\tau}} +  i_{LP} - i_{LP}(0)e^{-\frac{t}{\tau}}$，为零输入响应和零状态响应之和

### 阶跃输入

* 特解为$i_{LP} = I_1$，代入特解式得终值$I_1 = \frac{V}{R}$
* 全解为$i_L = Ae^{-\frac{t}{\tau}} + I_1$，代入初始条件$I(0) = I_0$，得$A = I_0 - I_1$，
* 全解$i_L = I_0e^{-\frac{t}{\tau}} + I_1(1 - e^{-\frac{t}{\tau}})$，为零状态输入和零状态响应之和
* 电流为$v_L = (I_1 - I_0)Re^{-\frac{t}{\tau}}$

![串联RL](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/series-RL.png)

#### 图形分析

* $t = 0$时，曲线斜率为$-\frac{A}{\tau}$
* $t = \tau$时，曲线值为$\frac{A}{e} + I_1$
* $t = 5\tau$，曲线值接近$I_1$

### 方波输入

电感改变了输入方波的形状

![串联RL-方波输入](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/series-RL-square.png)

## 状态方程

### 状态变量

可以概括电路在$t_0$时刻以前历史的变量

* 电容中的电荷、电压
* 电感中的磁通量、电流

### 状态方程分析

RC、RL的一阶微分方程可以写成状态方程$\frac{d}{dt}(状态变量) = f(状态变量，输入变量)$

* 初始状态为$v_c(t_0)$
* $v_c(t_0 + \bigtriangleup t) = v_c(t_0) + \frac{dv_c}{dt}|_{t=t_0}\bigtriangleup t$
* $v_c(t_0 + 2\bigtriangleup t) = v_c(t_0 + \bigtriangleup t) + \frac{dv_c}{dt}|_{t=t_0 + \bigtriangleup t}\bigtriangleup t$
* 即状态变量的值由初始状态和输入变量决定

### 状态方程求解

使用叠加法求解暂态问题，全响应等于零输入响应和零状态响应之和

* 零输入响应：输入变量为0，由初始状态决定的状态变量
* 零状态响应：初始状态为0，由输入变量决定的状态变量

## 传播延迟

### 定义

* $t_{pd,1\rightarrow 0}$：输入由1变为0时，输出达到相应的有效电压水平的延迟
* $t_{pd,0\rightarrow 1}$：输入由0变为1时，输出达到相应的有效电压水平的延迟
* 输入输出端延迟$t_{pd}$：$t_{pd} = max(t_{pd,1\rightarrow 0}, t_{pd,0\rightarrow 1})$
* 门电路延迟：所有输入到输出的最大延迟

![传播延迟](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/spread-delay.png)

### MOSFET的传播延迟

使用SRC模型分析

* 输入为1并达到稳态时，输出为$V_{TH} = \frac{R_{ON}}{R_{ON} + R_L}V_S$
* 输入为0并达到稳态时，输出为$V_S$
* 输入由1变为0时，电容充电，输出由$V_{TH}$变为$V_S$
* 输入由0变为1时，电容放电，输出由$V_S$变为$V_{TH}$

![MOSFET的传播延迟-1](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSEFT-spread-delay-1.png)

![MOSFET的传播延迟-2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSEFT-spread-delay-2.png)

![MOSFET的传播延迟-3](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSEFT-spread-delay-3.png)

### VLSI的传播延迟

同MOSFET的传播延迟分析

![VLSI的传播延迟-1](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/VLSI-spread-delay-1.png)

![VLSI的传播延迟-2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/VLSI-spread-delay-2.png)

![VLSI的传播延迟-3](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/VLSI-spread-delay-3.png)

### 寄生电感的传播延迟

MOSFET漏极与反相器输出间有很长的导线相连，产生寄生电感

![寄生电感的传播延迟](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/inductance-spread-delay.png)

## 参考资料

* 《模拟和数字电子电路基础》
