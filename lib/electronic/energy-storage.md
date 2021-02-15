# 储能元件

标签（空格分隔）： 理解

---

## 电容

存储电场能量

### 组成

* 电流流进电容正端时，电荷q传送到正极板上
* 电流从电容负端流出时，等量的电荷q从负极板上送出
* 正极板上的电荷q和负极板上的电荷-q在电介质中形成电场E(t)=q(t)/(εA(t))，产生电压v(t)=E(t)l(t)

![电容](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/capacitor.png)

### 元件方程

一般电容

* 电容：C(t)=εA(t)/l(t)，单位F（法）
* 电荷量：q(t)=C(t)v(t)，单位C（库伦）
* 电流：i(t)=dq(t)/dt=d(C(t)v(t))/dt

线性非时变电容

* 电容：C=εA/l
* 电荷量：q(t)=Cv(t)
* 电流：i(t)=dq(t)/dt=Cdv(t)/dt

![理想线性电容](https://raw.githubusercontent.com/wchaochao/images/master/gitbook-circuit/ideal-linear-capacitor.png)

### 记忆性质

* $q(t)=\int_{-∞}^{t}i(t)dt \Rightarrow q(t_2)=q(t_1)+\int_{t_1}^{t_2}i(t)dt$
* $v(t)=\frac{1}{C}\int_{-∞}^{t}i(t)dt \Rightarrow  v(t_2)=v(t_1)+\frac{1}{C}\int_{t_1}^{t_2}i(t)dt$

### 能量存储性质

* $w_E(t)=\frac{q^2(t)}{2C}=\frac{Cv^2(t)}{2}$
