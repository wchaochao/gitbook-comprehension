# 储能元件

标签（空格分隔）： 理解

---

## 电容

模拟电场效应的电路元件，存储电场能量

### 组成

* 电流流进电容正端时，电荷q传送到正极板上
* 电流从电容负端流出时，等量的电荷q从负极板上送出
* 正极板上的电荷q和负极板上的电荷-q在电介质中形成电场$E(t)=\frac{q(t)}{εA(t)}$，产生电压$v(t)=E(t)l(t)$

![电容](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/capacitor.png)

### 元件方程

* 电容：$C=εA/l$，单位F（法）
* 电荷量：$q(t)=Cv(t)$，单位C（库伦）
* 电流：$i(t)=\frac{dq(t)}{dt}=C\frac{dv(t)}{dt}$

![理想线性电容](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/ideal-linear-capacitor.png)

### 性质

记忆性质

* $q(t)=\int_{-∞}^{t}i(t)dt \Rightarrow q(t_2)=q(t_1)+\int_{t_1}^{t_2}i(t)dt$
* $v(t)=\frac{1}{C}\int_{-∞}^{t}i(t)dt \Rightarrow  v(t_2)=v(t_1)+\frac{1}{C}\int_{t_1}^{t_2}i(t)dt$

能量存储性质

* $w_E(t)=\frac{q^2(t)}{2C}=\frac{Cv^2(t)}{2}$

### 串并联

* 串联：电容减少，总电容的倒数为各电容的倒数之和
* 并联：电容增加，总电容为各电容之和

### 实际电容

* 会产生串联电阻和串联电感

## 电感

模拟磁场效应的电路元件，存储磁场能量

### 组成

* 电流在线圈中流通产生磁通，磁通密度为$B(t)=\frac{\mu Ni(t)}{l(t)}$
* 单匝磁通为$\Phi(t)=A(t)B(t)$
* 总磁通为$\lambda(t)=N\Phi(t)$

![电感](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/inductance.png)

### 元件方程

* 电感：$L=\frac{\mu N^2A}{l}$，单位H（亨）
* 磁通量：$\lambda(t)=Li(t)$，单位Wb（韦伯）
* 电压：$v(t)=\frac{d\lambda(t)}{dt}=L\frac{di(t)}{dt}$

![理想线性电感](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/ideal-linear-inductance.png)

### 性质

记忆性质

* $\lambda(t)=\int_{-∞}^{t}v(t)dt \Rightarrow \lambda(t_2)=\lambda(t_1)+\int_{t_1}^{t_2}v(t)dt$
* $i(t)=\frac{1}{L}\int_{-∞}^{t}v(t)dt \Rightarrow  i(t_2)=i(t_1)+\frac{1}{L}\int_{t_1}^{t_2}v(t)dt$

能量存储性质

* $w_M(t)=\frac{\lambda^2(t)}{2L}=\frac{Li^2(t)}{2}$

### 串并联

* 串联：电感增加，总电感为各电感之和
* 并联：总电感的倒数为各电感的倒数之和

### 实际电感

* 存在线圈电阻和匝间电容，使用并联电阻和电容来模拟

## 寄生电容和电感

### MOSFET栅极电容

* 栅极G施加正电压时，会吸引源极S中的电子到沟道表面
* 栅极与沟道之间形成一个平行极板电容，$C_{GS}=C_{OX}LW$， $C_{OX}=\frac{ε_{OX}}{d}$

![MOSFET栅极电容](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-capacitor.png)

SRC模型

* 栅极G和源极S之间存在电容，$i_C=C_{GS}\frac{dv_{GS}}{dt}$
* v<sub>G</sub>&lt;v<sub>T</sub>时，D端和S端开路，v<sub>DS</sub>=v<sub>S</sub>
* v<sub>G</sub>>=v<sub>T</sub>时，D端和S端短路，v<sub>DS</sub>=0

![MOSFETSRC模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/MOSFET-SRC-model.png)

### 变压器

* 电压关系：$\frac{v_1(t)}{N_1}=\frac{v_2(t)}{N_2}$
* 电流关系：$N_1i_1(t)=-N_2i_2(t)$
* 功率关系：$v_1(t)i_1(t)=-v_2(t)i_2(t)$

![理想变压器](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/transformer.png)

模型

![理想变压器模型](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/transformer-model.png)

### 导线回路电感

真空中的圆形导线回路产生的电感为$L=\mu_0R[ln(\frac{8R}{A})-2]$

![导线回路电感](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/loop-inductance.png)

### 集成电路的导线电容和电感

导体宽度远大于导体与底平面的距离时，单位长度的电容和电感为

![扁平导体1](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/ic-flat-conductor-1.png)

![扁平导体2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/ic-flat-conductor-2.png)

导体宽度相近导体与底平面的距离时，单位长度的电容和电感为

![圆柱导体1](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/ic-cylindrical-conductor-1.png)

![圆柱导体2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/ic-cylindrical-conductor-2.png)

单位长度的电容和电感满足$\widetilde C \widetilde L=ε\mu_0$

## 电路分析

### 电压源驱动电容

* 元件方程：$$i(t)=\frac{dq(t)}{dt}=C\frac{dV(t)}{dt}$$
* 输入：$$V(t)=\begin{cases}0 & t\leq0 \\ V_0 & t>0\end{cases}$$
* 输出：$$i(t)=C\frac{dV(t)}{dt}=CV_0\frac{du(t)}{dt}=CV_0\delta(t)$$

![阶跃输入电容1](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/step-input-capacitor-1.png)

### 电流源驱动电容

* 元件方程：$$v(t)=\frac{q(t)}{C}=\frac{1}{C}\int_{-∞}^{t}I(t)dt$$
* 输入：$$I(t)=\begin{cases}0 & t\leq0 \\ I_0 & t>0\end{cases}$$
* 输出：$$v(t)=\frac{1}{C}\int_{-∞}^{t}I(t)dt=\begin{cases}0 & t\leq0 \\ \frac{I_0t}{C} & t>0\end{cases}$$

![阶跃输入电容2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/step-input-capacitor-2.png)

### 电流源驱动电感

* 元件方程：$$v(t)=\frac{d\lambda(t)}{dt}=L\frac{dI(t)}{dt}$$
* 输入：$$I(t)=\begin{cases}0 & t\leq0 \\ I_0 & t>0\end{cases}$$
* 输出：$$v(t)=L\frac{dI(t)}{dt}=LI_0\frac{du(t)}{dt}=LI_0\delta(t)$$

![阶跃输入电感1](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/step-input-inductance-1.png)

### 电压源驱动电感

* 元件方程：$$i(t)=\frac{\lambda(t)}{L}=\frac{1}{L}\int_{-∞}^{t}V(t)dt$$
* 输入：$$V(t)=\begin{cases}0 & t\leq0 \\ V_0 & t>0\end{cases}$$
* 输出：$$i(t)=\frac{1}{L}\int_{-∞}^{t}V(t)dt=\begin{cases}0 & t\leq0 \\ \frac{V_0t}{L} & t>0\end{cases}$$

![阶跃输入电感2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/step-input-inductance-2.png)

### 冲激函数

$$\begin{cases}\delta(t)=0 & t\neq0 \\ \int_{-∞}^{t}\delta(t)dt=u(t) \\ \int_{-∞}^{+∞}\delta(t)dt=1\end{cases}$$

![冲激函数1](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/impulse-function-1.png)

![冲激函数2](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/impulse-function-2.png)

## 参考资料

* 《模拟和数字电子电路基础》
