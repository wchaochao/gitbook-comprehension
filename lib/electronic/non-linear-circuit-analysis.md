# 非线性电路分析

标签（空格分隔）： 理解

---

## 非线性元件

* 二极管元件：I<sub>D</sub>=I<sub>s</sub>(e<sup>V<sub>D</sub>/V<sub>TH</sub></sup>-1)
* 平均律元件：I<sub>D</sub>=KV<sub>D</sub><sup>2</sup>，V<sub>D</sub>>=0

## 直接分析

* 电压源、电阻、平均律元件串联：进行节点分析
* 线性网络、平均律元件串联：对平均律元件的接线端进行等效分析

## 图像分析

将解方程组转化为坐标轴上图形的交点

* 电压源、电阻、二极管元件串联：进行节点分析，解方程组转化为二极管元件v-i特性曲线与直线的交点

## 分段线性分析

将非线性元件的v-i曲线分解为一系列线段

### 理想二级管

* 二极管开通：短路，v<sub>D</sub>=0，i<sub>D</sub>为正
* 二极管断开：断路，i<sub>D</sub>=0，v<sub>D</sub>为负

## 增量分析

在很窄范围内的非线性元件线性话，i<sub>D</sub>=I<sub>D</sub>+(df/dv<sub>D</sub>)△v=I<sub>D</sub>+g<sub>d</sub>△v=I<sub>D</sub>+△v/r<sub>d</sub>

* 二极管元件的增量线性电阻为V<sub>TH</sub>I<sub>D</sub>

## 参考资料

* 《模拟和数字电子电路基础》
