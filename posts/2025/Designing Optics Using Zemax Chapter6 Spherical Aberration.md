---
title: Designing Optics Using Zemax Chapter6 Spherical Aberration  （球差）
tags: [Zemax]
categories: [光设软件基础-Zemax]
date: 2025-9-23
description: 本笔记参考 《Designing Optics Using Zemax》
articleGPT: 本章主要介绍在在将镜头输入 OpticStudio® 后，如何分析系统球差。主要介绍了横向光线像差曲线 transverse ray curve、点列图Spot diagram等手段。
references:
  - title: 《Designing Optics Using Zemax OpticStudio》
  - url: https://ebooks.spiedigitallibrary.org/ebooks/PM/designing-optics-using-zemax-opticstudio/eISBN-9781510668577/10.1117/3.100004
   
---

# 《Designing Optics Using Zemax 》 Chapter6 Spherical Aberration（球差）

> **参考书目：**  
> 《Designing Optics Using Zemax OpticStudio》 SPIE Press     &ensp;      Donald O’Shea and Julie Bentley 
>
> **使用软件：**\
> Ansys Zemax OpticStudio 2023 R2.00
>
> **课程概述：**\
> 本书旨在系统阐述使用光学设计软件Zemax OpticStudio®构建光学系统的设计方法。通过该软件平台，本书将完整呈现光学设计流程（从镜头参数定义到公差分析），并辅以详细的操作演示。本书的编排架构可使读者实现以下目标：
> 
> （1）完整重现设计过程中的每个操作步骤（包括生成光学性能分析图的流程）；
> 
> （2）透彻理解各环节在最终设计方案形成中的核心作用。



## 回顾：波像差推导出几何像差
像差函数由含$h^{2}$、$r^{2}$和$hr \cos \theta$因子的项构成。于是有：

$$
\begin{aligned}
W(\vec{h} ;\vec{r}) &= \sum_{l=0}^{\infty}\sum_{p=0}^{\infty}\sum_{m=0}^{\infty} C_{lpm}(h^{2})^{l}(r^{2})^{p}[h r\cos (\theta-\theta_{o})]^{m} \\
&= \sum_{l=0}^{\infty}\sum_{p=0}^{\infty}\sum_{m=0}^{\infty} C_{lpm}h^{2l+m}r^{2p+m}\cos ^{m}\left(\theta-\theta_{o}\right)
\end{aligned}
$$



**当  $2p + m = 0$  时（即所有不含  $r$  的项），其和必须为零**，因为与主光线（ $r = 0$  的情况）相关的像差为零。因此，零度项  $C_{000}$  及诸如  $C_{100}h^2$ 、 $C_{200}h^4$  等项在式（3-31）中不出现；

同时，**二阶项亦不存在**。项  $C_{010}r^2$  表示一个独立于  $h$  的离焦像差：若在略偏焦的平面（即通过图像面的纵向位移）观测图像，该像差可被消除，但这意味着定义像差函数所依据的高斯像点必定有误，故此像差项必须为零。

类似地，**项  $C_{001}hr \cos \theta$  表示一个依赖于  $h$  的波前倾斜像差**：其可通过图像在  $C_{001}Rh$  量级上的横向位移校正，隐含图像放大率为  $M(1 + C_{001}R)$ 。然而，这与图像放大率固定为  $M$  的事实相悖，因此该像差项亦必须为零。综上所述，像差函数的幂级数展开仅包含四阶、六阶、八阶等项，相应的像差分别称为初级像差、二级像差、三级像差等。

继续考虑之前的假设，即物点在$x_{o}$轴上，并用像高替换物高（一般情况下，均使用像高表征波像差展开，本质一样），则波像差幂级数展开可表示为：

$$W(h';r,\theta)=\sum_{l=0}^{\infty}\sum_{n=1}^{\infty}\sum_{m=0}^{\infty}\space_{2l+m}a_{nm}h'^{2l+m}r^{n}\cos^{m}\theta$$

这里,
$$\boxed{n=2p+m}$$

为正整数，即不为0（主光线没有像差）

$h'$是高斯像面像点高度，$\space_{2l+m}a_{nm}$是展开系数。

$n-m=2p \geq 0$，且为偶数。

**像差级次$i$等于物点坐标与瞳面坐标幂级次之和。**
$$\boxed{i=2l+m+n=2(l+p+m)}$$
从上式明显看出，$i$是偶数。

现在研究一个重要问题，即**对于同样一个$i$，有多少个$l、m、n$组合？**

梳理一下该问题的前提条件：
- $i=2l+m+n=2(l+m+p)$
- $n-m=2p \geq 0$，即$n\geq m$且$n-m$是偶数

$$\because i=2l+m+n$$
固定$i$时，$l$可以由$m$，$n$进行确定：
$$l=\frac{i-(m+n)}{2}$$
要求$l\neq 0$，则有：
$$m+n\leq i,m+n=i$$
则问题转化为：

$$\begin{cases}
m+n&\leq i\\
n&\equiv m(\text{mod}2)\\
n &\geq m
\end{cases}$$

在整数点阵里满足$m,n\geq 0,n\geq m,m+n\leq i$且$m+n$与$i$同奇偶的点的个数。

[![取点示意图](https://free.picui.cn/free/2025/09/22/68d0da1874dec.png)](https://free.picui.cn/free/2025/09/22/68d0da1874dec.png)

最终得到组合的数量应该满足：
$$N_{i}=\frac{(i+2)(i+4)}{8}$$

- 当$i=2$时
  $$N_{2}=\frac{(2+2)(2+4)}{8}=3$$
  满足$2l+m+n=2$，且$n-m$为偶数的项**共有3项**。
  - **$l=1,m=0,n=0$**
  
    代入波像差幂级数展开式可得：
    - $h'^{2}$： 被排除，因为主光线上必须像差为零。
  - **$l=0,m=0,n=2$**
  
    代入波像差幂级数展开式可得：
    - $r^{2}$：离焦（可通过像面平移消去）。
  - **$l=0,m=1,n=1$**
  
    代入波像差幂级数展开式可得：
    - $h'r\cos \theta$：波前倾斜（可通过横向移像消去）。

- 当$i=4$时
  $$N_{4}=\frac{(4+2)(4+4)}{8}=6$$
  满足$2l+m+n=4$，且$n-m$为偶数的项**共有6项**。
  - **$l=2,m=0,n=0$**

    代入波像差幂级数展开式可得：
    - $h'^{4}$：被排除，因为主光线上必须像差为零。
  
  - **$l=1,m=0,n=2$**
  
     代入波像差幂级数展开式可得：

     - $h'^{2}r^{2}$：**场曲**
  
  - **$l=0,m=0,n=4$**

    代入波像差幂级数展开式可得：

    - $r^{4}$：**球差**

  - **$l=1,m=1,n=1$**
  
    代入波像差幂级数展开式可得：
    - $h'^{3}r\cos \theta$：**畸变**
  - **$l=0,m=1,n=3$**
    代入波像差幂级数展开式可得：
    - $h'r^{3}\cos \theta$：**慧差**
  - **$l=0,m=2,n=2$**
    代入波像差幂级数展开式可得：
    - $h'^{2}r^{2}\cos \theta$：**像散**

  
| l | n | m | Aberration Term                       | Aberration Name |
| - | - | - | ------------------------------------- | --------------- |
| 0 | 4 | 0 | ${}_{0}a_{40} r^4$                    | Spherical       |
| 0 | 3 | 1 | ${}_{1}a_{31} h' r^3 \cos \theta$     | Coma            |
| 0 | 2 | 2 | ${}_{2}a_{22} h'^2 r^2 \cos^2 \theta$ | Astigmatism     |
| 1 | 2 | 0 | ${}_{2}a_{20} h'^2 r^2$               | Field curvature |
| 1 | 1 | 1 | ${}_{3}a_{11} h'^3 r \cos \theta$     | Distortion      |

**值得注意的一点，对于Zemax来说，分析像差主要分析的是横向像差，即二维平面上实际像点和高斯像点的偏差，而并非三维空间中的偏差，因此实际二维像面上的横向像差应为实际像差在一个方向上的梯度，因此有：**

| Aberration      | Wave Aberration ($W$) | Transverse Aberration ($\nabla W$) |
| --------------- | ------------------- | -------------------------- |
| Spherical       | $\rho^4$            | $\rho^3$                   |
| Coma            | $h \rho^3$          | $h \rho^2$                 |
| Astigmatism     | $h^2 \rho^2$        | $h^2 \rho$                 |
| Field curvature | $h^2 \rho^2$        | $h^2 \rho$                 |
| Distortion      | $h^3 \rho$          | $h^3$                      |

上表中$\rho$即为$r$。

## 单透镜轴上光线误差

### SINGLELET 镜头数据
[![镜头数据](https://free.picui.cn/free/2025/09/22/68d1174e611ca.png)](https://free.picui.cn/free/2025/09/22/68d1174e611ca.png)


### 切面光线
[![切面光线](https://free.picui.cn/free/2025/09/22/68d1174e84d4f.png)](https://free.picui.cn/free/2025/09/22/68d1174e84d4f.png)

**现象：光线并不汇聚在一点，而是在距离高斯像面的不同距离处。**

- **Paraxial focal point-PF：** 近轴焦点，近轴平行光线在近轴焦点处相交。
- **MargF：** 入射到入瞳边缘的一对边缘平行光线在距离透镜更近的轴上一点处相交。
- **MinF：** 光学系统中存在一个轴上的特定点，称为最小聚焦点（MinF）。该点处聚焦光锥束达到**最小截面**，**所有光线**在该位置被约束于最小面积范围内。

## 球差的直观展示

### LSA 轴向球差

从上面的图中可以得到一个结论：**一束对称的平行光线，随着其入射到入瞳的高度$\rho$不同，其与光轴的交点位置也随之发生变化。** 这一现象即为**LSA（longitudinal spherical aberration）纵向球差/轴向球差**

在Zemax中，可以通过**Analyze > Aberration > Longitudinal Aberration**进行直观评判。


[![LongitudinalAberration.png](https://free.picui.cn/free/2025/09/22/68d126dca58fb.png)](https://free.picui.cn/free/2025/09/22/68d126dca58fb.png)


- 纵坐标：Normalized Pupil Coordinate 归一化入瞳直径，即将入瞳直径缩放到$[0,1]$范围内
- 纵坐标：Millimeters 主要反映两条对称平行光线交点距离近轴像点的位置，坐标原点为近轴像点。

从上图也可以看出，在示例镜头下，一对平行光线的入瞳直径越大，其交点越接近透镜，远离PF。

### Spot diagram 点列图

另一种表征透镜像差大小的方法，是利用单物点发出的光线在入瞳处形成二维阵列，通过绘制该阵列中**大量光线与像平面相交点**的分布规律实现，即Spot diagram 点列图。

在Zemax中，**Analyze > Rays & Spots > Standard Spot Diagram**即可得到点列图。

- 取消选择 Use Symbols
- Pattern修改为Square

[![SpotDiagram.png](https://free.picui.cn/free/2025/09/22/68d12c6fe7330.png)](https://free.picui.cn/free/2025/09/22/68d12c6fe7330.png)

点列图可使设计人员清晰了解**光斑在评估面（此处指近轴焦平面）的聚集程度**。图中比例尺可用于评估光线分布范围，底部叠加标注了光斑的**均方根半径（RMS）**及包围所有追迹光线的**几何半径（GEO，该参数通常显示于图例区域）**。

### Zemax的快速聚焦功能-Quick Focus

将**像面由近轴焦点移至光轴上的其他位置称为透镜离焦，移动距离即离焦量**。

针对单透镜系统进行离焦操作时，**需在LDE中的S2面后插入新表面（标注为"Defocus"）。通过手动调节离焦面的厚度值（T3）** 并同步查看每次调节后的点列图数据，可确定100%几何直径（GEO）最小的焦点位置——该直径为所有透射光线的最小外接圆直径。

[![加入离焦面后的LDE](https://free.picui.cn/free/2025/09/22/68d1174e611ca.png)](https://free.picui.cn/free/2025/09/22/68d1174e611ca.png)

- defocus 4.600mm
  [![SpotDiagram-defoucus4600.png](https://free.picui.cn/free/2025/09/22/68d13197733b0.png)](https://free.picui.cn/free/2025/09/22/68d13197733b0.png)

- defocus 4.059mm
  [![SpotDiagram-defocus4059.png](https://free.picui.cn/free/2025/09/22/68d131976b67c.png)](https://free.picui.cn/free/2025/09/22/68d131976b67c.png)

- defocus 0.000mm
  [![SpotDiagram-defocus0000.png](https://free.picui.cn/free/2025/09/22/68d12c6fe7330.png)](https://free.picui.cn/free/2025/09/22/68d12c6fe7330.png)

然而，OpticStudio软件内置快速优化功能，可通过**计算单位面积最大能量密度自动定位透镜最佳焦面**。操作流程如下：**Optimize > Quick Focus**。此时系统将弹出优化目标类型选择窗口，需从下拉菜单中选取"径向点尺寸（**Spot Size Radial**）"作为优化判据。执行该操作后，软件将基于选定判据计算出最佳成像面位置（本例计算结果为4.059毫米），并自动将第三表面厚度参数更新为该优化值。

[![Quick Focus](https://free.picui.cn/free/2025/09/22/68d132d52da7b.png)](https://free.picui.cn/free/2025/09/22/68d132d52da7b.png)

## Transverse Ray Plots 横向光线图/横向像差曲线


---
**点列图的作用**

所谓 **点列图（spot diagram）**，是把一组光线在像平面上的交点投影出来的图像。它能直观反映系统成像点和理想点的偏离程度，也就是说它揭示了“像点的扩散情况”，因此可以看出透镜误差大小的大致水平。比如点列图越分散，说明像差越大；越集中，说明成像质量越好。

**局限性：无法区分像差种类**

但是，点列图只展示了光线最终“落在像平面上的分布结果”，并没有告诉我们这些偏差是由哪种像差引起的。

* 如果系统中只有一种主要像差（例如纯球差），点列图可能还能表现出某种典型的对称或分布特征。
* 可是当 **多种像差（球差、彗差、像散、场曲、畸变）同时存在** 时，它们的作用在点列图中是叠加在一起的，表现为一个综合的光斑分布。这样一来，就很难“解耦”，也就是难以通过点列图直接判断是哪一种像差贡献了多少。

**举例说明**

* 单纯球差时，点列图可能是对称环状的分布；
* 彗差时，点列图可能是拖尾的彗星状；
* 但如果两者同时存在，点列图会混合成不规则形态，让人难以分辨其中具体是哪种像差导致的特征。

**因此需要其他工具**

为了分析具体像差的来源，通常要借助 **像差曲线（transverse ray plot）**、**波像差函数（wavefront aberration）** 或 **Zernike 多项式展开** 等方法。它们能把不同像差成分分开表示，从而帮助设计者明确误差来源。


::: danger
区分透镜中特定像差的一种方法是绘制经入瞳（包括子午和弧矢方向）的光线束的偏差（$e_{x}$与$e_{y}$）分布图。
::: 



::: warning
**<font color='red'>横向像差曲线的原理</font>**

[![绘制示意图](https://free.picui.cn/free/2025/09/22/68d154a9f28c0.png)](https://free.picui.cn/free/2025/09/22/68d154a9f28c0.png)

如上图所示，绘制了$y-z$面的15条子午光线束，与瞳面交于不同位置。

若不存在球面像差，光线束中的所有光线均将会聚于高斯像面上同一点。由于球面像差的存在，光线束中每条光线的误差以光轴为基准，表现为该光线偏离光轴的横向距离。

需要明确的是，射线的光瞳坐标可沿透镜$x$轴或$y$轴分布，但在**曲线图中统一表现为$x$轴数值**；同理，**射线的横向偏差（$e_{x}$或$e_{y}$）将统一表示为$y$轴数值**。

- 横向像差曲线的横轴：表示出瞳位置$\rho_{x}$、$\rho_{y}$
- 横向像差曲线的纵轴：表示横向偏差$e_{x}$、$e_{y}$

:::

在Zemax中，通过**Analyze > Rays & Spots > Ray Aberration**即可绘制出子午、弧矢两个方向上的横向像差曲线图。

[![横向像差曲线图](https://free.picui.cn/free/2025/09/22/68d15a6f04468.png)](https://free.picui.cn/free/2025/09/22/68d15a6f04468.png)

横向像差曲线可以直接识别透镜像差的种类。例如上图，横向像差曲线仅仅绘制了视场$h=0$的光线在瞳面处，随入瞳直径的半径变化，其横向偏差的变化。而$h=0$对应的轴上点初级像差即为球差。且横向球差与$\rho$成三次方。

### 横向像差曲线特征

- 横向光线曲线的一个重要特性是：**当评价平面因离焦而发生位置变化时，曲线形状保持不变，仅绕原点发生旋转。** 

> 举例说明：可以想象单透镜成像特点，当一束平行光进入单透镜，单透镜后的光线截面面积随着与单透镜距离的增加，呈现先减小后增大的趋势。**以光轴上方边缘光线为例，当评价平面无限接近透镜时，其横向偏差一定大于0；而当评价平面位于近轴像面PF时，显然评价平面在MargF之后，其横向偏差一定小于0。**

[![transrvers MargF.png](https://free.picui.cn/free/2025/09/23/68d2261c75b46.png)](https://free.picui.cn/free/2025/09/23/68d2261c75b46.png)

[![transrvers MinF.png](https://free.picui.cn/free/2025/09/23/68d2261ccaa9c.png)](https://free.picui.cn/free/2025/09/23/68d2261ccaa9c.png)

[![transrvers PF.png](https://free.picui.cn/free/2025/09/23/68d2261ccc965.png)](https://free.picui.cn/free/2025/09/23/68d2261ccc965.png)

- 当初选评估平面为近轴焦点时，**接近光轴的入射光线会聚焦于近轴焦点附近，此时光线误差极小，横向光线曲线在原点处与$x$轴相切**。 **在这些曲线中，原点处若存在斜率即表明：当前评估未满足近轴像平面条件，透镜实际呈现离焦现象。**

- 通过绘制曲线最高点与最低点处的水平直线，可形成包含所有曲线点的带状区域，进而完成**对像差弥散斑直径的估测过程**。该直径的量化表征可由图中穿过曲线最大值点与最小值点的两条平行水平线所构成的带状区域宽度获得。

## Third-Order Aberration Coefficients 三阶（初级）像差系数

对于横向球差来说，球差大小正比于光线在入瞳处高度$\rho$的三次方。

当光线高度为$\rho=1$（归一化的高度）时，球差的总误差由横向球差系数（TSPH）决定。

$$e_{y}(\rho,h)=TSPH \rho^{3}$$

Zemax中在分析选项**Analysis > Aberrations >Seidel Coefficients**中自动计算透镜中每个面的像差系数。

选择横向像差系数作为评价指标，这些像差系数缩写均以'T'作为开头，对应的缩写和实际像差名称如下表：

| **Labels** | **Aberrations** | **中文** |
|------------|-----------------|----------|
| **TSPH**   | SP**Herical** aberration | 球差 |
| **TSCO**   | Sagittal **CO**ma (not used in THIRD) | 弧矢彗差（在 THIRD 中未使用） |
| **TTCO**   | Tangential **CO**ma | 子午彗差 |
| **TAST**   | Average **AST**igmatism | 平均散光/像散 |
| **TPFC**   | **P**etzval **F**ield **C**urvature | Petzval 场曲 |
| **TSFC**   | **S**agittal **F**ield **C**urvature (= TAST/2 + TPFC) | 弧矢场曲 |
| **TTFC**   | **T**angential **F**ield **C**urvature (= 3TAST/2 + TPFC) | 子午场曲 |
| **TDIS**   | **DIS**tortion | 畸变 |
| **TAXC**   | **AX**ial **C**olor | 轴向色差 |
| **TLAC**   | **LA**teral **C**olor | 横向色差 |

### 像差系数计算宏代码 THIRD.zpl


```
! this macro calculates the transverse ray aberrations
! v0.1 MRH: 2020-08-13
! 2020-09-17: updated the non-color terms to have the correct sign
! JLB 2021-01-18 Reordered the coefficients and names to match ZOS
! JLB 2022-07-23 updated formatting to fit SPIE text page

REWIND
PRINT "THIRD"
dummy = SYPR(16)
str$ = $BUFFER()
IF SLEN(str$) > 0 THEN PRINT "Title: ", $BUFFER()
!PRINT
PRINT "Primary Wavelength: ", WAVL(PWAV()), " um"
!PRINT

w = WAVL(PWAV()) / 1000
DECLARE t, DOUBLE, 1, 11

s$ = " "
PRINT "Surf", " ", "TSPH", s$, "TTCO", s$, "TAST", s$, "TPFC", s$, "TSFC", s$, "TTFC", s$, "TDIS", s$, "TAXC", s$, "TLAC"

! get paraxial values for image space
m = OPEV(OCOD("PARB"), NSUR(), PWAV(), 0, 0, 0, 1)
n = OPEV(OCOD("PARC"), NSUR(), PWAV(), 0, 0, 0, 1)
nu = INDX(NSUR()) * m / n


! get the stop surface
GETSYSTEMDATA 1
ss = VEC1(23)

! get the min/max index values for axial and lateral color
mm = 1
xx = 1
FOR i = 1, SYPR(201), 1
    IF WAVL(i) < WAVL(mm) THEN mm = i
    IF WAVL(i) > WAVL(xx) THEN xx = i
NEXT

DECLARE nm, DOUBLE, 1, NSUR() + 1
DECLARE nx, DOUBLE, 1, NSUR() + 1
twav = PWAV()
PWAV mm
FOR i = 0, NSUR(), 1
    nm(i + 1) = INDX(i)
NEXT
PWAV xx
FOR i = 0, NSUR(), 1
    nx(i + 1) = INDX(i)
NEXT
PWAV twav

nus = 0
FOR surf = 1, NSUR(), 1
    ! get wavefront coefficients
    w040 = OPEV(OCOD("SPHA"), surf, PWAV(), 0, 0, 0, 0)
    w131 = OPEV(OCOD("COMA"), surf, PWAV(), 0, 0, 0, 0)
    w222 = OPEV(OCOD("ASTI"), surf, PWAV(), 0, 0, 0, 0)
    w220 = OPEV(OCOD("FCUR"), surf, PWAV(), 0, 0, 0, 0)
    w311 = OPEV(OCOD("DIST"), surf, PWAV(), 0, 0, 0, 0)

    ! calculate seidel coefficients
    s1 = (8 * w) * w040
    s2 = (2 * w) * w131
    s3 = (2 * w) * w222
    ! there is a bug between the reported Seidel and TRA...TRA is correct
    s4 = (4 * w) * w220       # as reported in ‘Seidel Aberration Coefficients’ section
    !s4 = (4 * w) * w220 - (2 * w) * w222
    s5 = (2 * w) * w311

    ! calculate transverse ray aberrations
    tsph = s1 / (2 * nu)
    tsco = s2 / (2 * nu)
    ttco = 3 * s2 / (2 * nu)
    tast = s3 / (nu)
    tpfc = s4 / (2 * nu)
    tsfc = (s3 + s4) / (2 * nu)
    tstf = (3 * s3 + s4) / (2 * nu)
    tdis = s5 / (2 * nu)

    ! cl = -ni_m * ys_m * dn
    !     ni_m = nu_m + INDX * y_m * CURV
    !     nu_m = u_m + INDX = m_m / n_m * INDX
    !     dn = (nm2 - nx2) / n2 - (nm1 - nx1) / n1
    ! ct = -ni_c * y_c * dn
    m_m = OPEV(OCOD("PARB"), surf, PWAV(), 0, 0, 0, 1)
    n_m = OPEV(OCOD("PARC"), surf, PWAV(), 0, 0, 0, 1)
    y_m = OPEV(OCOD("PARY"), surf, PWAV(), 0, 0, 0, 1)
    m_c = OPEV(OCOD("PARB"), surf, PWAV(), 0, 1, 0, 0)
    n_c = OPEV(OCOD("PARC"), surf, PWAV(), 0, 1, 0, 0)
    y_c = OPEV(OCOD("PARY"), surf, PWAV(), 0, 1, 0, 0)

    nu_m = 0
    IF ABSO(n_m) > 0 THEN nu_m = m_m / n_m * INDX(surf)
    ni_m = nu_m + INDX(surf) * y_m * CURV(surf)

    nu_c = 0
    IF ABSO(n_c) > 0 THEN nu_c = m_c / n_c * INDX(surf)
    ni_c = nu_c + INDX(surf) * y_c * CURV(surf)

    dn = ((nm(surf + 1) - nx(surf + 1)) / INDX(surf)) - ((nm(surf) - nx(surf)) / INDX(surf - 1))

    cl = -ni_m * y_m * dn
    ct = -ni_c * y_m * dn

    taxc = cl / nu
    tlac = ct / nu

    ! keep a running sum of all transverse ray aberrations
    t(1) = t(1) + tsph
    !t(2) = t(2) + tsco
    t(3) = t(3) + ttco
    t(4) = t(4) + tast
    t(5) = t(5) + tpfc
    t(6) = t(6) + tsfc
    t(7) = t(7) + tstf
    t(8) = t(8) + tdis
    t(9) = t(9) + taxc
    t(10) = t(10) + tlac

s$ = " "

    FORMAT 3.0
    s$ = $STR(surf) + " "
    s$ = $LEFTSTRING(s$, 4)

    IF surf == ss THEN s$ = "STO "
    IF surf == NSUR() THEN s$ = "IMA "
    PRINT s$, "",

    FORMAT 9.4
    PRINT tsph,
    !PRINT tsco,
    PRINT ttco,
    PRINT tast,
    PRINT tpfc,
    PRINT tsfc,
    PRINT tstf,
    PRINT tdis,
    PRINT taxc,
    PRINT tlac
NEXT

PRINT "TOT ", t(1), t(3), t(4), t(5), t(6), t(7), t(8), t(9), t(10)

  
```

运行结果如下：只有$TSPH$一列存在非零数值，原因是视场设置为轴上物点，只有0°，故其他离轴像差均为0。Zemax会计算出每一个面对某类像差的贡献。注意该宏代码仅仅计算初级像差，忽略更高阶的像差。

```
THIRD
Primary Wavelength: 0.5876 um
Surf TSPH TTCO TAST TPFC TSFC TTFC TDIS TAXC TLAC
STO   -0.0032  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
  2   -1.1333   0.0000  -0.0000  -0.0000  -0.0000  -0.0000   0.0000  -0.0000  -0.0000
  3   -0.0000   0.0000  -0.0000   0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
IMA   -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
TOT   -1.1366   0.0000   0.0000   0.0000   0.0000   0.0000   0.0000   0.0000   0.0000

```

