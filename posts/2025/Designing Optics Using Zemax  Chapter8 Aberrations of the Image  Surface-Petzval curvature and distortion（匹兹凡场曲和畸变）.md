---
title: Designing Optics Using Zemax Chapter8 Aberrations of the Image  Surface-Petzval curvature and distortion（匹兹凡场曲和畸变）
tags: [Zemax]
categories: [光设软件基础-Zemax]
date: 2025-9-24
description: 本笔记参考 《Designing Optics Using Zemax》
articleGPT: 本章主要介绍在在将镜头输入 OpticStudio® 后，如何分析系统匹兹凡场曲与畸变。
references:
  - title: 《Designing Optics Using Zemax OpticStudio》
  - url: https://ebooks.spiedigitallibrary.org/ebooks/PM/designing-optics-using-zemax-opticstudio/eISBN-9781510668577/10.1117/3.100004
   
---



# 《Designing Optics Using Zemax 》 Chapter8 Aberrations of the Image  Surface-Petzval curvature and distortion（匹兹凡场曲和畸变）

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

在设计光学系统（如相机镜头）时，通常要求透镜将物方场景成像到平面上。然而，实际透镜的成像面并非平面曲线，其$z$轴方向与近轴平面像面的偏离量构成了一种曲面像差——**匹兹凡场曲Petzval curvature**。若成像面本身为曲面（参考人眼视网膜的弯曲结构），匹兹凡场曲可能不会造成影响；但由于多数现代图像传感器为平面结构，在进行镜头设计时就必须严格控制该项像差。

本章更详细地探讨了Petzval曲率和第二个像面像差——**畸变distortion**。畸变是一种像面误差，它不会使图像模糊，但会使$x-y$平面内的主要光线位置产生误差，从而导致放大率随图像高度的变化。这就导致了物体的拉伸(或压缩)图像。


| Aberration      | Wave Aberration ($W$) | Transverse Aberration ($\nabla W$) |
| --------------- | ------------------- | -------------------------- |
| Spherical       | $\rho^4$            | $\rho^3$                   |
| Coma            | $h \rho^3$          | $h \rho^2$                 |
| Astigmatism(tangential)     | $h^2 \rho_{y}^2$        | $h^2 \rho_{y}$                 |
| Astigmatism(sagittal)     | $h^2 \rho_{x}^2$        | $h^2 \rho_{x}$                 |
|Petzval curvature | $h^2 \rho^2$        | $h^2 \rho$                 |
| Distortion      | $h^3 \rho$          | $h^3$                      |

## Field Curves 场曲

### 直观观察

可以从上一章的消球差镜头的切面图观察到，设置切面图显示三个视场的光线束，不难发现，这三个光线束的汇聚点不全都在近轴像面处，并且也不在同一个直线上。

[![消球差透镜切面图.png](https://free.picui.cn/free/2025/09/29/68da294bf0867.png)](https://free.picui.cn/free/2025/09/29/68da294bf0867.png)

如下图所示，可以直观看出像面有一定弯曲，并非一个平面：

[![像面弯曲-场曲](https://free.picui.cn/free/2025/09/29/68da510bbe10b.png)](https://free.picui.cn/free/2025/09/29/68da510bbe10b.png)

### field curvature plot 场曲曲线

尽管横向光线像差曲线仅提供少数视场点的信息，但另一种称为**场曲图**的图示可以更简洁、直观地展示镜头在整个视场范围内的成像性能。

**Analyze > Aberrations > Field Curvature and Distortion**即可得到下图：

[![场曲图.png](https://free.picui.cn/free/2025/09/29/68da54bb35934.png)](https://free.picui.cn/free/2025/09/29/68da54bb35934.png)

实际上这幅图左侧子图才是场曲图，右侧子图则是畸变图。

对于场曲图来说：

- 有**两支走向不同的曲线**。一支（实线）代表子午场曲，另一支（虚线）则代表弧矢场曲。
- 文本部分**详细展示了全视场光线聚焦的偏移值**：
  - Field Curvature Sagittal = 1.2781mm
  - Field Curvature Tangential = 2.7052mm

> **场曲所呈现的误差并非单一的三阶像差，而是像散与匹兹凡场曲的叠加效应。我们将阐明：像散导致子午与弧矢弯曲像面发生分离，而匹兹伐场曲作为基础场曲，在透镜经像散校正后依然持续存在。这些三阶像差须分别考量，因其需采用截然不同的校正策略才可以实现成像平面平整。**

## Petzval Curvature 匹兹凡场曲

最简单的展示匹兹凡场曲的方法就是使用一组反射镜，一个凸面，另一个为凹面，例如Schwarzchild系统。


### Schwarzchild系统构建

- aperture：EPD 20mm
- wavelength：d-line 0.588$\mu m$
- filed：angle 0°、7°、10°

**LDE数据**
  
[![Schwarzchild系统镜头数据](https://free.picui.cn/free/2025/09/29/68da683db5063.png)](https://free.picui.cn/free/2025/09/29/68da683db5063.png)

**切面图**

[![Schwarzchild系统.png](https://free.picui.cn/free/2025/09/29/68da697a9c5d3.png)](https://free.picui.cn/free/2025/09/29/68da697a9c5d3.png)

### THIRD.zpl的分析

```
THIRD
Primary Wavelength: 0.5876 um
Surf TSPH TTCO TAST TPFC TSFC TTFC TDIS TAXC TLAC
  1    0.0000   0.0000   0.0000   0.0000   0.0000   0.0000  -0.0000  -0.0000  -0.0000
STO    0.0265   0.1731   0.2515  -0.1258  -0.0000   0.2515   0.0000  -0.0000  -0.0000
  3   -0.0265  -0.1731  -0.2515   0.0480  -0.0777  -0.3293  -0.1694  -0.0000  -0.0000
IMA   -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
TOT    0.0000   0.0000   0.0000  -0.0777  -0.0777  -0.0777  -0.1694   0.0000   0.0000
```

从运行结果可以看出，对于上述系统来说，其球差TSPH、彗差TTCO以及像散TAST均为0，因此子午场曲TTFC和弧矢场曲TSFC的数值大小均取决于匹兹凡场曲，二者数值相等，均为-0.0777。

**同样地，从横向像差曲线中也可以分析出系统像散为0。**

[![横向像差曲线](https://free.picui.cn/free/2025/09/29/68da666213b6f.png)](https://free.picui.cn/free/2025/09/29/68da666213b6f.png)

从上图可以看出，无论在哪个视场下，子午光线与弧矢光线的横向像差曲线斜率相同，说明子午光线束和弧矢光线束应该汇聚点为同一点，否则在近轴像面的同一位置处，二者对应的光线高度不同。

### 场曲图

[![场曲图](https://free.picui.cn/free/2025/10/05/68e20a608aed6.png)](https://free.picui.cn/free/2025/10/05/68e20a608aed6.png)

可见子午场曲和弧矢场曲曲线重合。

## 场曲与初级像差系数

明确一点，子午场曲和弧矢场曲数值是由匹兹凡场曲与像散（不分子午弧矢方向）一起贡献的。在OpticStudio®光学设计软件中，场曲图中的T曲线与S曲线表征了对应方向像散（astigmatism）与匹兹凡场曲（Petzval curvature）之和。**无论是场曲图还是S/T曲线数值列表，均无法直接显示这两类像差的独立数据。那么如何分离这些成分？**

### 借助初级像差理论

根据初级像差理论，**子午光线像散是弧矢光线像散的三倍。** 记$\Delta$为沿光轴方向所测量的弧矢像散的最大值，$T$、$S$分别表示子午场曲与弧矢场曲，$P$表示匹兹凡场曲，则有：
$$T=3\Delta+P$$
$$S=\Delta+P$$

而$T$、$S$的数值可以根据场曲图下方的数据列表获得，根据上述两式可以计算出匹兹凡场曲大小：
$$P=\dfrac{3S-T}{2}$$

[![增添匹兹凡曲线](https://free.picui.cn/free/2025/10/05/68e2209fc2edc.png)](https://free.picui.cn/free/2025/10/05/68e2209fc2edc.png)

### 利用THIRD.zpl

## Anastigmatic Lens 消像散透镜

现有技术表明，仅采用双透镜配合微小空气间隙及贴附光阑的结构（即消球差双合镜）难以实现超越前述方案的显著优化。

核心制约在于：双透镜**仅提供四个光学表面、两种玻璃材料及两个透镜厚度作为变量，调节自由度不足以同时消除球差、彗差与像散**。

通过增加透镜元件以扩展设计维度，利用空气间隙作为附加可控变量，并允许光阑轴向位移，可构造出具有低像散特性的消像散透镜。其中最具代表性的解决方案是采用**空气隔离三片式结构—即库克三片式镜头**（Cooke triplet）。

### 镜头数据

[![镜头数据](https://free.picui.cn/free/2025/10/05/68e22b8543c9a.png)](https://free.picui.cn/free/2025/10/05/68e22b8543c9a.png)


### 切面图

[![库克三片式镜头切面图.png](https://free.picui.cn/free/2025/10/05/68e22bd6bcd5d.png)](https://free.picui.cn/free/2025/10/05/68e22bd6bcd5d.png)


### 场曲图

[![库克三片式镜头场曲图.png](https://free.picui.cn/free/2025/10/05/68e22c4086dcd.png)](https://free.picui.cn/free/2025/10/05/68e22c4086dcd.png)

虽然弧矢和子午场曲仍有偏离，但是在数量级上已经非常接近。

## Distortion 畸变
