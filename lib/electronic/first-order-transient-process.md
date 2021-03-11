# 一阶暂态过程

标签（空格分隔）： 理解

---

## 串联RC电路

### 阶跃输入

#### 电路分析

节点分析得$$0 = \frac{v_c - v_1}{R} + C\frac{dv_c}{dt}$$
写为非齐次线性一阶常微分方程$$\frac{dv_c}{dt} + \frac{v_c}{RC} = \frac{v_1}{RC}$$
全解为齐次解和特解之和$$\begin{cases} \frac{dv_{ch}}{dt} + \frac{v_{ch}}{RC} = 0 \\ \frac{dv_{cp}}{dt} + \frac{v_{cp}}{RC} = \frac{V}{RC} \end{cases}$$

* 齐次解为$v_{ch} = Ae^{st}$，代入齐次式得$s = -\frac{1}{RC}$
* 特解为$v_{cp} = K$，代入特解式得$K = V$
* 全解为$v_c = Ae^{-\frac{t}{RC}} + V$，代入初始条件$v(0) = V_0$，得$A = V_0 - V$，，为零状态响应和零状态输入之和
* 全解$v_c = (V_0 - V)e^{-\frac{t}{RC}} + V$，为零状态输入$v_c = V_0e^{-\frac{t}{RC}}$和零状态响应$v_c = V(1 - e^{-\frac{t}{RC}})$之和

![串联RC](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/series-rc.png)

#### 图形分析

* $t = 0$时，曲线斜率为$-\frac{A}{\tau}, \ \tau=RC$
* $t = \tau$时，曲线值为$\frac{A}{e} + V$
* $t = 5\tau$，曲线值接近V

#### 充电过程

$V>V_0$，电容进行充电

* $t = 0$时，曲线斜率为$\frac{V - V_0}{\tau}$
* $t = \tau$时，曲线值为$V - \frac{V - V_0}{e}V$
* $t = 5\tau$，曲线值接近V

#### 放电过程

$V<V_0$，电容进行放电

* $t = 0$时，曲线斜率为$-\frac{V_0 - V}{\tau}$
* $t = \tau$时，曲线值为$V + \frac{V_0 - V}{e}V$
* $t = 5\tau$，曲线值接近V

### 方波输入

电容改变了输入方波的形状

* 时间常数RC远小于脉冲长度时，电容波形与输入波形相似
* 时间常数RC的5倍小于脉冲长度时，电容完成完整的充放电
* 时间常数RC远大于脉冲长度时，电容电压为输入电压的积分，$v_c = \frac{1}{RC}\int_{0}^{t}v_idt$，接近于0

![串联RC-方波输入](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/series-rc-square.png)

## 参考资料

* 《模拟和数字电子电路基础》
