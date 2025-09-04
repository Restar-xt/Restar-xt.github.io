---
title: Ray geometrical optics-Chapter3 Optical aberrations 光学像差
tags: [Zemax]
categories: [光设理论基础]
date: 2025-9-3
description: 本笔记参考 《Optical imaging and aberrations part I. Ray geometrical optics》
articleGPT: 这是Optical imaging and aberrations part I. Ray geometrical optics中第三章Optical aberrations的相关笔记，本章从波像差和几何像差的定义入手，点明波像差与几何像差之间的关系，明确从波像差中可以推导出几何像差这一重要结论。在此基础上，引入离焦波像差和波前倾斜两类因为观察角度或元件装配等问题产生的波像差。进一步地，讨论了关于其光轴旋转对称的成像系统可能存在的像差。将系统像差函数展开为物坐标与瞳坐标的幂级数，引入初级、二级、三级像差理论。该像差也可通过泽尼克圆（Zernike circle polynomials）多项式进行展开，并给出了两类展开系数之间的转换关系。文中简要讨论了初级像差的干涉图特征，以阐明实践中如何识别此类像差。最终通过论述系统在何种条件下可形成无像差完美成像来结束本章，重点推导了正弦条件：若满足该条件的离轴共轭点所在平面中，轴向共轭点已实现完美成像，则所有阶彗差均为零。
references:
  - title: 《Optical imaging and aberrations part I. Ray geometrical optics》
  - url: https://doi.org/10.1117/3.265735
   
---




# Ray geometrical optics-Chapter3 Optical aberrations 光学像差

> **参考书目：**  
>**$\text{Optical imaging and aberrations: part I. Ray geometrical optics}$**                &ensp;      $\text{Virendra N. Mahajan}$
>
>$\text{ISBN 0-8194-2515-X}$



## 本章概述


对特定物点而言，其**波像差表征出射光瞳处波前偏离球面的光学偏差量**。若波像差为零（即波前呈理想球面），则所有光线汇聚于曲率中心形成完美点像。系统像差将导致成像质量劣化，而**光线像差（即几何像差）则反映光线在过曲率中心的像平面上相对该中心的位移量**。

虽然**可通过全光路追迹至像平面获得特定物点的光线像差，但亦可从波像差推导获取**。需注意：**<font color='red'>像平面上的光线分布并非真实成像图景，因其未计入出射光瞳处的波前衍射效应</font>**。波像差作为决定成像质量的核心参数，其量化表征至关重要。

值得强调的是：**多元件系统的波像差具有可加性——全系统的光线波像差等于各元件波像差之和**。但**光线像差不具此性质，最终像平面上的光线像差不可通过元件像平面值简单叠加获得**。

当观测平面偏离曲率中心所在像面时，将引入**离焦波像差**；同理，系统内成像元件沿光轴位移亦会产生此效应。我们将推演像面纵向离焦量与由此引发的离焦像差之函数关系。类似地，当成像元件微倾或横向偏离光轴时，会产生**波前倾斜**现象。我们将阐明波前倾斜与其对应像差的关联机制。

其次，讨论了关于其光轴旋转对称的成像系统可能存在的像差。将系统像差函数**展开为物坐标与瞳坐标的幂级数，引入初级、二级、三级像差理论**。该像差也可通过**泽尼克圆（Zernike circle polynomials）多项式**进行展开，并给出了两类展开系数之间的转换关系。文中简要讨论了初级像差的干涉图特征，以阐明实践中如何识别此类像差。最终通过论述系统在何种条件下可形成无像差完美成像来结束本章，重点推导了正弦条件：若满足该条件的离轴共轭点所在平面中，轴向共轭点已实现完美成像，则所有阶彗差均为零。

## 波像差、光线像差的定义

[![通过光学系统实现完美成像。P为物点，P′为其对应的高斯像点。](https://free.picui.cn/free/2025/09/02/68b65eb3d8c62.png)](https://free.picui.cn/free/2025/09/02/68b65eb3d8c62.png)

### 波像差 wave aberration

> - 光程：即折射率乘光线传播路径长度
> - 波前：如果从某一个点处发出的光线经过光学系统，并追溯其至出瞳处，同时确保每条光束的实际光程均等于主光线光程（主光线即穿过出瞳中心的光线），将这些光线的等光程点连接构成的曲面即为波前。

先考虑**完善成像**。
- 从**波的角度**分析：若**出瞳处的波前为球面，且其曲率中心在高斯像点处**，我们就称该系统完善成像（波前原本是球面，经过光学系统后仍是球面；原始波前以物点为曲率中心扩散，经过系统后的波前以高斯像点为中心收敛）
- 从**光线角度**分析：通过$P$传播至$P'$的**所有光线光程都相同**，即为完善成像。

完善成像时出瞳位置处的波前为球面，我们称之为高斯参考球面（Gaussian reference sphere）如果，
- 从**波的角度**分析：实际波前偏离高斯参考球面，则称该系统成像有像差。
- 从**光线角度**分析：通过$P$传播至$P'$的光线光程不都相同，则称该系统成像有像差。

在参考球面上某点处光线的**波像差**，**等于该光线对应的波前相对于高斯球面波前的光程差**。它反映了所考察光线与主光线从**点物传播至参考球面**过程中的**光程差**。而主光线对应的波像差恒为零，加之所有理想光线从参考球面到高斯像点的光程相等，因此，**任意光线的波像差亦可表述为：该光线从点物$P$到高斯像点$P'$的光程与主光线光程之差**。更详细的表述是：实际光线从物点$P$传播到高斯参考球面$Q$点（**这一部分光线是真实的，即为实际光线的传播路径**）后，再由$Q$传播到高斯像点$P'$（**这一部分光线是虚拟的，实际光线并不会传播到高斯像点**）的光程和主光线光程之差。


### 轴上物点对应的波像差

[![轴上物点对应的波像差示意图](https://free.picui.cn/free/2025/09/03/68b7be45f0f8f.png)](https://free.picui.cn/free/2025/09/03/68b7be45f0f8f.png)

- 高斯像点-高斯参考球面曲率中心：$P_{0}'$
- 实际像点：$P_{0}''$
- 理想波前-高斯参考球面：虚线绘制，通过出瞳中心点$O$
- 实际波前：实线绘制，通过出瞳中心点$O$
- 实际光线与高斯参考球面的交点：$Q$
- 实际光线与实际波前的交点：$\overline{Q}$
- 主光线：$CR_{0}$
- 实际光线：$GR_{0}$
- 波像差：$n_{i}\overline{Q} Q$

### 轴外物点对应的波像差

[![轴外物点对应的波像差示意图](https://free.picui.cn/free/2025/09/03/68b7be45ee7d8.png)](https://free.picui.cn/free/2025/09/03/68b7be45ee7d8.png)

- 高斯像点-高斯参考球面曲率中心：$P_{0}'$
- 实际像点：$P''$
- 理想波前-高斯参考球面：虚线绘制，通过出瞳中心点$O$
- 实际波前：实线绘制，通过出瞳中心点$O$
- 实际光线与高斯参考球面的交点：$Q$
- 实际光线与实际波前的交点：$\overline{Q}$
- 主光线：未绘制
- 实际光线：$GR$
- 波像差：$n_{i}\overline{Q} Q$

### 几何像差/光线像差 geometrical aberration
以轴外物点对应的波像差示意图为例，高斯像点为$P'$，实际像点为$P''$，实际像点与高斯像点的偏移$P'P''$即为几何像差。


### 研究波像差时的坐标系建立

均为右手直角坐标系（笛卡尔坐标系）。其中光轴沿$z$轴，物体平面、出瞳平面、高斯像面均垂直于$z$轴并相互平行。
- 物平面 object：坐标原点位于$P_{0}$，物点位于$x$轴上。
- 出瞳平面 pupil：坐标原点位于$O$，$Q$为出瞳面实际波前上一点。
- 高斯像面 Gaussian image：坐标原点位于$P_{0}$，高斯像点为$P'(x_{g},0,z_{g})$，实际像点为$P''(x_{i},y_{i},z_{g})$
  
将轴外物点位置假设在$x$轴上虽然很特殊，但是**考虑系统的旋转对称性**，这样特殊假设得出的结论是具有一般性的。

[![坐标系](https://free.picui.cn/free/2025/09/04/68b94b3066fe9.png)](https://free.picui.cn/free/2025/09/04/68b94b3066fe9.png)

### 波像差与几何像差对比

| 对比维度         | 波像差 (Wavefront Aberration)                          | 几何像差 (Geometrical Aberration)                       |
|------------------|--------------------------------------------------------|-------------------------------------------------------|
| 定义             | 实际波前与理想球面波前的偏差                           | 光线经光学系统后实际像点与理想像点的偏离                      |
| 理论基础         | 基于波动光学理论                                       | 基于几何光学理论                                      |
| 描述对象         | 描述波前的畸变                                         | 描述光线的传播误差                                    |
| 数学表达         | 通常用**多项式**（如泽尼克多项式）表示                     | 用**赛德尔像差（球差、彗差、像散等）分类**描述            |
| 分析视角         | 相位分布视角                                           | 光线追迹视角                                          |
| 像质评价联系     | 与斯特列尔比（Strehl Ratio）和调制传递函数（MTF）直接相关 | 与点列图、光线扇图直接相关                            |
| 优点             | 更接近光的本质，能精确描述衍射效应                     | 直观易懂，计算相对简单                                |
| 局限性           | 计算复杂，对高数值孔径或大像差系统分析困难             | 忽略衍射效应，在接近衍射极限的系统中准确性下降        |
| 多元件叠加性           | 可以直接叠加得到系统总波像差             | 无法直接相加        |

**几何像差直观易算，能够用数值来描述一点成像时的几何光线的密集程度，从而评估像质的优劣。但光线本身是一抽象的近似概念，用密集程度来评价，往往与实际不符，因此必须考虑像差的最佳校正方案，并根据光学系统的要求和使用状况给出合理像差。而这些像质评价问题常须基于光的波动本质才能解决。此外，波像差可以推导出几何像差。**

## 哈密顿点特征函数 Hamilton’s Point Characteristic Function

[![在具有折射率  $n'$  的介质中，单位矢量为  $\hat{u}'$  的光线传播路径。波阵面  $W'$  和  $W''$  分别通过该光路上两点  $P'$  和  $A$ ](https://free.picui.cn/free/2025/09/03/68b85629e1880.png)](https://free.picui.cn/free/2025/09/03/68b85629e1880.png)

若考虑折射率分别为  $n$  和  $n'$  的两种介质中的点  $P$  和  $P'$ ，其三维位置矢量分别为  $\mathbf{r}$  和  $\mathbf{r}'$ ，则从  $P$  到  $P'$  的光线光程长度称为**哈密顿点特征函数**，可表示为  $V(P, P')$  或  $V(\mathbf{r}, \mathbf{r}')$ 。

令  $\mathbf{\hat{u}}'$  为过  $P'$  的射线方向的单位矢量，**显然物点$P$应该在该光线上的反向延长线上，即$P$与$P'$共线**。如上图所示，考察邻近点  $P''$ ，其位置矢量为  $\mathbf{r}' + \delta\mathbf{r}'$ （此处  $\delta\mathbf{r}'$  表示从  $P'$  指向  $P''$  的矢量  $\overrightarrow{P'P''}$ ）。沿光线路径  $PBP''$（仍为一条直线）  的点特征函数可写作  $V(\mathbf{r}, \mathbf{r}' + \delta\mathbf{r}')$ 。若将  $V$  视为  $\mathbf{r}'$  的函数，则可表示为:

$$V(\mathbf{r},\mathbf{r'}+\delta{\mathbf{r'}})-V(\mathbf{r},\mathbf{r'})=\delta\mathbf{r'}\cdot \nabla'V$$

其中，$\nabla'$是关于$\mathbf{r'}$的梯度算子。

- **对于公式左侧**：考虑波前的定义，同一波前上的某点到物点的光程应相同，即:
  $$opl(PB)=opl(PP')$$
  $$opl(PBP'')=opl(PP'A)$$
  那么则有：
  $$opl(PBP'')-opl(PB)=opl(PP'A)-opl(PP')$$
  即：
  $$opl(BP'')=opl(P'A)$$
  因此
  $$\begin{aligned}
    V(\mathbf{r},\mathbf{r'}+\delta{\mathbf{r'}})-V(\mathbf{r},\mathbf{r'}) &= opl(PBP'') - opl(PP') \\
    &= opl(PP'A) - opl(PP') \\
    &= opl(P'A) \\
    &= opl(BP'')
    \end{aligned}$$

  而对于$P'A$，根据向量数量积的定义可知：
  $$\overline{P'A}=\overrightarrow{P'P''}\cdot \mathbf{\hat{u}'}=\delta\mathbf{r'}\cdot \mathbf{\hat{u}}'$$

  那么等式左侧即可写为：
  $$opl(P'A)=n'\mathbf{\hat{u}'}\cdot \delta \mathbf{r'}$$

- **对于公式右侧**：不需要进一步整理。
  
综上所述，即可得到：
$$\boxed{n'\mathbf{\hat{u}'}\cdot \delta \mathbf{r'}=\delta\mathbf{r'}\cdot \nabla'V}$$

化简即可得到：

$$\boxed{n'\mathbf{\hat{u}'}= \nabla'V}$$

上述公式的物理意义：**终点$P'$处的光线方向$\mathbf{\hat{u}'}$由哈密顿点特征函数对终点位置的梯度决定**。

## 波像差和几何像差关系推导

[![轴上物点对应的波像差示意图](https://free.picui.cn/free/2025/09/03/68b7be45f0f8f.png)](https://free.picui.cn/free/2025/09/03/68b7be45f0f8f.png)

[![轴外物点对应的波像差示意图](https://free.picui.cn/free/2025/09/03/68b7be45ee7d8.png)](https://free.picui.cn/free/2025/09/03/68b7be45ee7d8.png)


在上面两个图中，以实际光线$GR_{0}$或$GR$为例，该光线分别与波前及参考球面相交于点$\overline{Q}$和点$Q$。根据波前的定义，从物点出发终止于$\overline{Q}$的光线，其光程与终止于$O$点的主光线光程相等。因此，$n_{i}\overline{Q}Q$表征了所研究光线的波像差（如图所示，其数值为正）。设$W(x,y)$代表该波像差，其中$(x,y,z)$为点Q的空间坐标。由于点$Q$位于参考球面上，**其$z$坐标与$x$、$y$呈函数关系**，故无需显式考虑$W$对$z$的依存性。

> **波像差的正负问题：**
>
> - 从光程角度入手：
>   若实际光线传播到高斯参考球面的光程大于主光线传播到高斯参考球面的光程，则波像差为正，反之则否。
> - 从几何上直观来看：
>   若实际波前位于高斯参考球面（理想波前）左侧，波像差为正，反之则否。

对于上图中的实际光线$GR_{0}$与$GR$对应的波像差，可以用哈密顿点特征函数表示：

$$W(x,y)=V(P,Q)-V(P,\overline{Q})$$
又因为，
$$V(P,\overline{Q})=V(P,O)$$
所以有：
$$W(x,y)=V(P,Q)-V(P,O)$$
上式对$x$求偏导可得：
$$\frac{\partial W}{\partial x}=\frac{\partial V(P,Q)}{\partial x}-0=\frac{\partial V(P,Q)}{\partial x}$$
考虑到，$z$是关于$x$,$y$的函数，那么上式可写为：
$$\frac{\partial W}{\partial x}=\frac{\partial V}{\partial x}+\frac{\partial V}{\partial z}\frac{\partial z}{\partial x}$$

[![坐标系](https://free.picui.cn/free/2025/09/04/68b94b3066fe9.png)](https://free.picui.cn/free/2025/09/04/68b94b3066fe9.png)

利用公式：
$$\boxed{n'\mathbf{\hat{u}'}= \nabla'V}$$
考虑其物理意义：**终点$P'$处的光线方向$\mathbf{\hat{u}'}$由哈密顿点特征函数对终点位置的梯度决定**。

将该公式应用至$QP''$段，则有：
$$\bigg(\frac{\partial V}{\partial x},\frac{\partial V}{\partial y},\frac{\partial V}{\partial z}\bigg)=\frac{n_{i}}{R'}(x_{i}-x,y_{i}-y,z_{g}-z)$$
其中，$R'$为$QP''$长度，$n_{i}$为其所在空间中的折射率。

而，
$$QP'=OP'=R$$
则有：
$$x_{g}^{2}+z_{g}^{2}=R^{2}$$
$$(x-x_{g})^{2}+y^{2}+(z-z_{g})^{2}=R^{2}$$
即：
$$x_{g}^{2}+z_{g}^{2}=(x-x_{g})^{2}+y^{2}+(z-z_{g})^{2}$$
化简可得：
$$x^{2}+y^{2}+z^{2}-2xx_{g}-2zz_{g}=0$$
上式对$x$求偏导即可得到：
$$2x+2z\frac{\partial z}{\partial x}-2x_{g}-2z_{g}\frac{\partial z}{\partial x}=0$$
即：
$$\frac{\partial z}{\partial x}=-\frac{x-x_{g}}{z-z_{g}}$$

综上，得到三个等式：
$$\begin{cases}
\dfrac{\partial W}{\partial x}=\dfrac{\partial V}{\partial x}+\dfrac{\partial V}{\partial z}\dfrac{\partial z}{\partial x}\\ 
\space \\  
\left( \dfrac{\partial V}{\partial x}, \dfrac{\partial V}{\partial y}, \dfrac{\partial V}{\partial z} \right) = \dfrac{n_{i}}{R'} \left( x_{i} - x, y_{i} - y, z_{g} - z \right) \\
\space \\
\dfrac{\partial z}{\partial x} = -\dfrac{x - x_{g}}{z - z_{g}}

\end{cases}$$

三式结合，最终可以得到:


$$
\begin{aligned}
\frac{\partial W}{\partial x} &= \frac{n_{i}}{R'}(x_{i}-x) - \frac{n_{i}}{R'}(z_{g}-z) \cdot \frac{x - x_{g}}{z - z_{g}} \\
&= \frac{n_{i}}{R'}(x_{i}-x_{g})
\end{aligned}
$$

可改写为：
$$\boxed{x_{i}-x_{g}=\frac{R'}{n_{i}}\frac{\partial W}{\partial x}}$$

同理：
$$\boxed{y_{i}=\frac{R'}{n_{i}}\frac{\partial W}{\partial y}}$$

上述二式给出了参考球面上点$(x, y, z)$处的波像差 $W(x, y)$ 与高斯像平面中光线像差 $(x_i-x_g,y_i)$ 之间的精确关系。然而，这两个公式所含的距离 $R'$ 本身取决于点P′′的坐标 $(x_i, y_i)$ 。


由于实际参考球面的曲率半径 $R$ 远大于光线分布范围，可将 $R'$ 替换为 $R$ ，并表述为：

