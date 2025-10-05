---
title: Designing Optics Using Zemax Chapter7 Coma and Astigmatism（彗差与像散）
tags: [Zemax]
categories: [光设软件基础-Zemax]
date: 2025-9-24
description: 本笔记参考 《Designing Optics Using Zemax》
articleGPT: 本章主要介绍在在将镜头输入 OpticStudio® 后，如何分析系统彗差与像散。
references:
  - title: 《Designing Optics Using Zemax OpticStudio》
  - url: https://ebooks.spiedigitallibrary.org/ebooks/PM/designing-optics-using-zemax-opticstudio/eISBN-9781510668577/10.1117/3.100004
   
---


# 《Designing Optics Using Zemax 》 Chapter7 Coma and Astigmatism（彗差与像散）

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

上一章论证了球面像差的特性，借助横向像差曲线和点列图探究了其在光轴上的表现。若球差系透镜唯一存在的像差，其成像表现将在整个视场内保持一致。然而当偏离光轴观测视场点时，其他误差因素便会增入球差之中。本章将另行探讨后续两种三级横向像差：彗差（$\rho^{2}h$）与像散（$\rho_{x}h²$ 及 $\rho_{y}h^{2}$）。

| Aberration      | Wave Aberration ($W$) | Transverse Aberration ($\nabla W$) |
| --------------- | ------------------- | -------------------------- |
| Spherical       | $\rho^4$            | $\rho^3$                   |
| Coma            | $h \rho^3$          | $h \rho^2$                 |
| Astigmatism(tangential)     | $h^2 \rho_{y}^2$        | $h^2 \rho_{y}$                 |
| Astigmatism(sagittal)     | $h^2 \rho_{x}^2$        | $h^2 \rho_{x}$                 |
|Petzval curvature | $h^2 \rho^2$        | $h^2 \rho$                 |
| Distortion      | $h^3 \rho$          | $h^3$                      |

## Coma 彗差

$$\text{Coma}\propto \rho^{2}h$$

从上述公式明显可以看出，彗差是一个离轴像差。彗差的大小与入瞳直径$\rho$的二次方成正比，与视场$h$成正比。

为了观察彗差这种离轴像差，需要在之前单透镜的基础上，将视场调整为0°、7°、10°用以观察。

[![Coma Layout.png](https://free.picui.cn/free/2025/09/23/68d28087901c8.png)](https://free.picui.cn/free/2025/09/23/68d28087901c8.png)

上图绘制了10°视场角下，15束光线的汇聚情况，不难看出在像面上，从下至上相邻光线在像平面的交点距离逐渐增加，且非线性增加。


::: danger
区分离轴像差和轴上像差可以通过比较**点列图**和**横向像差**曲线。主要观察0°视场和其他非零视场对应的图像。
:::

### 点列图

- **0°**

[![0°点列图.png](https://free.picui.cn/free/2025/09/24/68d343d5db313.png)](https://free.picui.cn/free/2025/09/24/68d343d5db313.png)

- **7°**

[![7°点列图.png](https://free.picui.cn/free/2025/09/24/68d343d595c0f.png)](https://free.picui.cn/free/2025/09/24/68d343d595c0f.png)

- **10°**

[![10°点列图.png](https://free.picui.cn/free/2025/09/24/68d343d5eee4c.png)](https://free.picui.cn/free/2025/09/24/68d343d5eee4c.png)



### 横向像差曲线

- **0°**
  
[![0°横向像差曲线.png](https://free.picui.cn/free/2025/09/24/68d343b53bcc5.png)](https://free.picui.cn/free/2025/09/24/68d343b53bcc5.png)

- **7°**
  
[![7°横向像差曲线.png](https://free.picui.cn/free/2025/09/24/68d343b5559d4.png)](https://free.picui.cn/free/2025/09/24/68d343b5559d4.png)

- **10°**

[![10°横向像差曲线.png](https://free.picui.cn/free/2025/09/24/68d343b8e99f6.png)](https://free.picui.cn/free/2025/09/24/68d343b8e99f6.png)

**通过比较可以发现，0°视场下的横向像差曲线与球差一节完全相同。轴外曲线虽同样呈现S形，但受彗差影响，其形态相对坐标原点呈现非对称特性。同样的点列图也可以看出轴外的非对称性。**

### THIRD.zpl运行结果

```
THIRD
Primary Wavelength: 0.5876 um
Surf TSPH TTCO TAST TPFC TSFC TTFC TDIS TAXC TLAC
  1    0.0000   0.0000   0.0000   0.0000   0.0000   0.0000  -0.0000  -0.0000  -0.0000
STO   -0.0032  -0.0206  -0.0291  -0.0221  -0.0366  -0.0657  -0.0775  -0.0000  -0.0000
  3   -1.1333   1.0070  -0.1988  -0.0816  -0.1810  -0.3798   0.0536  -0.0000  -0.0000
IMA   -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
TOT   -1.1366   0.9863  -0.2279  -0.1036  -0.2176  -0.4455  -0.0239   0.0000   0.0000
```

横向彗差(TTCO)为0.9863，与三级球差(1.1366)近似相同但符号相反。这导致在10°横向像差曲线中，**对于$+\rho$（曲线的右侧部分）误差近似消减，而对于$-\rho$（曲线的左侧部分）误差近似加倍。**

## 使用Zemax观察彗差与孔径的关系

**固定10°视场，改变入瞳直径**

### 5mm入瞳直径下的THIRD.zpl结果

```
THIRD
Primary Wavelength: 0.5876 um
Surf TSPH TTCO TAST TPFC TSFC TTFC TDIS TAXC TLAC
  1    0.0000   0.0000   0.0000   0.0000   0.0000   0.0000  -0.0000  -0.0000  -0.0000
STO   -0.0001  -0.0013  -0.0073  -0.0055  -0.0092  -0.0164  -0.0775  -0.0000  -0.0000
  3   -0.0177   0.0629  -0.0497  -0.0204  -0.0452  -0.0950   0.0536  -0.0000  -0.0000
IMA   -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
TOT   -0.0178   0.0616  -0.0570  -0.0259  -0.0544  -0.1114  -0.0239   0.0000   0.0000

```
**TTCO-TOT 0.0616**

### 10mm入瞳直径下的THIRD.zpl结果

```
THIRD
Primary Wavelength: 0.5876 um
Surf TSPH TTCO TAST TPFC TSFC TTFC TDIS TAXC TLAC
  1    0.0000   0.0000   0.0000   0.0000   0.0000   0.0000  -0.0000  -0.0000  -0.0000
STO   -0.0004  -0.0052  -0.0146  -0.0110  -0.0183  -0.0329  -0.0775  -0.0000  -0.0000
  3   -0.1417   0.2517  -0.0994  -0.0408  -0.0905  -0.1899   0.0536  -0.0000  -0.0000
IMA   -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
TOT   -0.1421   0.2466  -0.1140  -0.0518  -0.1088  -0.2228  -0.0239   0.0000   0.0000
```
**TTCO-TOT 0.2466**

### 20mm入瞳直径下的THIRD.zpl结果

```
THIRD
Primary Wavelength: 0.5876 um
Surf TSPH TTCO TAST TPFC TSFC TTFC TDIS TAXC TLAC
  1    0.0000   0.0000   0.0000   0.0000   0.0000   0.0000  -0.0000  -0.0000  -0.0000
STO   -0.0004  -0.0052  -0.0146  -0.0110  -0.0183  -0.0329  -0.0775  -0.0000  -0.0000
  3   -0.1417   0.2517  -0.0994  -0.0408  -0.0905  -0.1899   0.0536  -0.0000  -0.0000
IMA   -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
TOT   -0.1421   0.2466  -0.1140  -0.0518  -0.1088  -0.2228  -0.0239   0.0000   0.0000
```
**TTCO-TOT 0.2466**

```
THIRD
Primary Wavelength: 0.5876 um
Surf TSPH TTCO TAST TPFC TSFC TTFC TDIS TAXC TLAC
  1    0.0000   0.0000   0.0000   0.0000   0.0000   0.0000  -0.0000  -0.0000  -0.0000
STO   -0.0032  -0.0206  -0.0291  -0.0221  -0.0366  -0.0657  -0.0775  -0.0000  -0.0000
  3   -1.1333   1.0070  -0.1988  -0.0816  -0.1810  -0.3798   0.0536  -0.0000  -0.0000
IMA   -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
TOT   -1.1366   0.9863  -0.2279  -0.1036  -0.2176  -0.4455  -0.0239   0.0000   0.0000
```

**TTCO-TOT 0.9863**

从上面的结果不难看出，入瞳直径扩大2倍，彗差扩大四倍。
即当视场不变时有：
$$\text{Coma}\propto \rho^{2}$$

## 使用Zemax观察彗差与视场的关系

固定入瞳直径20mm不变，改变视场大小。注意物高随视场正切值变化。

此处不再赘述，方法和上小节相同。

## 多种像差存在时如何分离各部分像差贡献

由于该透镜同时存在球差与彗差，因此难以在横向像差曲线或点列图中观察到纯粹彗差的效应。然而，可借助各类像差与孔径及视场的相关性，通过数值模拟展现彗差（$\rho²h$形式）或其他像差在横向像差曲线中的形态。此类曲线图可通过Excel或其他绘图程序实现。

### 模拟只有球差的情况

[![模拟的各个视场对应的横向像差曲线](https://free.picui.cn/free/2025/09/24/68d3afc0888b4.png)](https://free.picui.cn/free/2025/09/24/68d3afc0888b4.png)

**结果分析：** 各视场横向像差曲线均呈现相同三次函数形态，这与球差不随视场$h$变化的特性相符。

[![屏幕截图 2025-09-24 164537.png](https://free.picui.cn/free/2025/09/24/68d3afc081bd7.png)](https://free.picui.cn/free/2025/09/24/68d3afc081bd7.png)

**结果分析：** 纯彗差的横向像差曲线呈U形开放结构，即其**形态随光瞳坐标$\rho$呈二次函数变化。**

## 彗差与透镜弯曲

与球差类似，彗差随透镜形状（透镜弯曲）的改变而变化。为验证此现象，可反转单透镜结构，并建立三个视场角（0°、7°和10°）以评估该透镜的离轴性能。


### 点列图对比

**注意，反转结构和原始结构的点列图坐标轴标度不同，反转结构像差较小，但对应的标度也小，观察起来似乎像差变大了，实际上是变小了。可以直接对比两种结构的RMS/GEO数值大小。**





- **0°点列图对比**

| [![反转0°点列图.png](https://free.picui.cn/free/2025/09/24/68d3cfc35b5a3.png)](https://free.picui.cn/free/2025/09/24/68d3cfc35b5a3.png)|[![0°点列图.png](https://free.picui.cn/free/2025/09/24/68d343d5db313.png)](https://free.picui.cn/free/2025/09/24/68d343d5db313.png)|
|:--:|:--:|
| 反转结构 | 原始结构 |


- **7°点列图对比**



| [![反转7°点列图.png](https://free.picui.cn/free/2025/09/24/68d3cfc33b4d9.png)](https://free.picui.cn/free/2025/09/24/68d3cfc33b4d9.png)|[![7°点列图.png](https://free.picui.cn/free/2025/09/24/68d343d595c0f.png)](https://free.picui.cn/free/2025/09/24/68d343d595c0f.png)|
|:--:|:--:|
| 反转结构 | 原始结构 |

- **10°点列图对比**

| [![10°点列图.png](https://free.picui.cn/free/2025/09/24/68d343d5eee4c.png)](https://free.picui.cn/free/2025/09/24/68d343d5eee4c.png)|[![7°点列图.png](https://free.picui.cn/free/2025/09/24/68d343d595c0f.png)](https://free.picui.cn/free/2025/09/24/68d343d595c0f.png)|
|:--:|:--:|
| 反转结构 | 原始结构 |

### 横向像差曲线对比

**注意，反转结构和原始结构的横向像差曲线坐标轴标度不同，反转结构像差较小，但对应的标度也小，观察起来似乎像差变大了，实际上是变小了。这一点可以通过$\rho=+1/-1$处的数值反映出来。**

- **0° 横向像差曲线对比**

| [![反转0°横向像差曲线.png](https://free.picui.cn/free/2025/09/24/68d3cfc2e97d3.png)](https://free.picui.cn/free/2025/09/24/68d3cfc2e97d3.png) | [![0°横向像差曲线.png](https://free.picui.cn/free/2025/09/24/68d343b53bcc5.png)](https://free.picui.cn/free/2025/09/24/68d343b53bcc5.png) |
|:--:|:--:|
| 反转结构 | 原始结构 |

- **7° 横向像差曲线对比**

| [![反转7°横向像差曲线.png](https://free.picui.cn/free/2025/09/24/68d3cfc2df88b.png)](https://free.picui.cn/free/2025/09/24/68d3cfc2df88b.png) | [![0°横向像差曲线.png](https://free.picui.cn/free/2025/09/24/68d343b53bcc5.png)](https://free.picui.cn/free/2025/09/24/68d343b53bcc5.png) |
|:--:|:--:|
| 反转结构 | 原始结构 |


- **10° 横向像差曲线对比**

| [![反转10°横向像差曲线.png](https://free.picui.cn/free/2025/09/24/68d3cfc52b071.png)](https://free.picui.cn/free/2025/09/24/68d3cfc52b071.png)| [![10°横向像差曲线.png](https://free.picui.cn/free/2025/09/24/68d343b8e99f6.png)](https://free.picui.cn/free/2025/09/24/68d343b8e99f6.png) |
|:--:|:--:|
| 反转结构 | 原始结构 |

### THIRD.zpl运行结果

- **原始结构**

```
THIRD
Primary Wavelength: 0.5876 um
Surf TSPH TTCO TAST TPFC TSFC TTFC TDIS TAXC TLAC
  1    0.0000   0.0000   0.0000   0.0000   0.0000   0.0000  -0.0000  -0.0000  -0.0000
STO   -0.0032  -0.0206  -0.0291  -0.0221  -0.0366  -0.0657  -0.0775  -0.0000  -0.0000
  3   -1.1333   1.0070  -0.1988  -0.0816  -0.1810  -0.3798   0.0536  -0.0000  -0.0000
IMA   -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
TOT   -1.1366   0.9863  -0.2279  -0.1036  -0.2176  -0.4455  -0.0239   0.0000   0.0000
```

- **反转结构**

```
THIRD
Primary Wavelength: 0.5876 um
Surf TSPH TTCO TAST TPFC TSFC TTFC TDIS TAXC TLAC
  1    0.0000   0.0000   0.0000   0.0000   0.0000   0.0000  -0.0000  -0.0000  -0.0000
STO   -0.1641  -0.2819  -0.1076  -0.0816  -0.1354  -0.2429  -0.0775  -0.0000  -0.0000
  3   -0.2411   0.4382  -0.1770  -0.0221  -0.1105  -0.2875   0.0670  -0.0000  -0.0000
IMA   -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
TOT   -0.4053   0.1563  -0.2845  -0.1036  -0.2459  -0.5304  -0.0105   0.0000   0.0000

```

比较彗差TTCO，反转结构明显减小。


## Aplanatic Lenses 消球差透镜

### Zemax基本参数

- 孔径设置 aperture： 入瞳直径EPD $10mm$
- 波长设置 wavelength：d-line $0.5876\mu m$
- 视场设置 field：angle 类型 0°、7°、10°

### 镜头数据

[![消球差镜头的数据](https://free.picui.cn/free/2025/09/29/68da264b7abdd.png)](https://free.picui.cn/free/2025/09/29/68da264b7abdd.png)

注意一个操作点，即镜头材料material的输入。此处不再指定某种材料，而是点击Material一栏右侧的空格（类似用边缘高度计算厚度），solve type选择Model，输入折射率与阿贝数。

### 切面图

[![消球差透镜切面图.png](https://free.picui.cn/free/2025/09/29/68da294bf0867.png)](https://free.picui.cn/free/2025/09/29/68da294bf0867.png)

### 横向光线像差曲线与点列图

- **0°**

|[![屏幕截图 2025-09-29 144150.png](https://free.picui.cn/free/2025/09/29/68da2aeccc981.png)](https://free.picui.cn/free/2025/09/29/68da2aeccc981.png)|[![屏幕截图 2025-09-29 144419.png](https://free.picui.cn/free/2025/09/29/68da2aed22e93.png)](https://free.picui.cn/free/2025/09/29/68da2aed22e93.png)|
|:--:|:--:|
| 横向光线像差曲线 | 点列图 |

- **7°**

|[![屏幕截图 2025-09-29 144158.png](https://free.picui.cn/free/2025/09/29/68da2aed60c9b.png)](https://free.picui.cn/free/2025/09/29/68da2aed60c9b.png)|[![屏幕截图 2025-09-29 144427.png](https://free.picui.cn/free/2025/09/29/68da2aeced80e.png)](https://free.picui.cn/free/2025/09/29/68da2aeced80e.png)|
|:--:|:--:|
| 横向光线像差曲线 | 点列图 |

- **10°**

|[![屏幕截图 2025-09-29 144207.png](https://free.picui.cn/free/2025/09/29/68da2aed32c65.png)](https://free.picui.cn/free/2025/09/29/68da2aed32c65.png)|[![屏幕截图 2025-09-29 144439.png](https://free.picui.cn/free/2025/09/29/68da2aeebaab9.png)](https://free.picui.cn/free/2025/09/29/68da2aeebaab9.png)
|:--:|:--:|
| 横向光线像差曲线 | 点列图 |

### THIRD.zpl运行结果

```
THIRD
Primary Wavelength: 0.5876 um
Surf TSPH TTCO TAST TPFC TSFC TTFC TDIS TAXC TLAC
STO   -0.0261  -0.0829  -0.0585  -0.0445  -0.0738  -0.1323  -0.0781  -0.0000  -0.0000
  2   -1.8408   1.3211  -0.2107  -0.0908  -0.1961  -0.4068   0.0469  -0.0000  -0.0000
  3    1.9213  -1.3899   0.2234   0.0994   0.2112   0.4346  -0.0509  -0.0000  -0.0000
  4   -0.0502   0.1544  -0.1055  -0.0202  -0.0729  -0.1784   0.0747  -0.0000  -0.0000
IMA   -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000  -0.0000
TOT    0.0041   0.0027  -0.1512  -0.0561  -0.1317  -0.2829  -0.0073   0.0000   0.0000

```

尽管该消球差透镜在轴上的成像几乎完美，其彗差也趋于零，但两轴外视场点的光斑尺寸仍表现极差。从上图的点列图可见，消球差透镜远非理想透镜设计的终点。在7°与10°视场处，光斑范围显著大于轴上光斑，且呈现明显的非对称性——子午方向的光斑宽度明显大于弧矢方向。这种非对称特征同时体现在各视场点的子午与弧矢横向光迹曲线斜率差异上。

## Astigmatism 像散

| Aberration      | Wave Aberration ($W$) | Transverse Aberration ($\nabla W$) |
| --------------- | ------------------- | -------------------------- |
| Spherical       | $\rho^4$            | $\rho^3$                   |
| Coma            | $h \rho^3$          | $h \rho^2$                 |
| Astigmatism(tangential)     | $h^2 \rho_{y}^2$        | $h^2 \rho_{y}$                 |
| Astigmatism(sagittal)     | $h^2 \rho_{x}^2$        | $h^2 \rho_{x}$                 |
|Petzval curvature | $h^2 \rho^2$        | $h^2 \rho$                 |
| Distortion      | $h^3 \rho$          | $h^3$                      |

从上表不难看出：
$$\text{Astigmatism}\propto h^{2}\rho$$

描述像散误差时，两个入射光瞳位置尤为重要：一个位于$y-z$ 平面（子午面），另一个与之正交地位于 $x-z$ 平面（弧矢面）。若用蓝色光线绘制通过消球差镜的子午面（$y-z$ 平面）光线扇，同时用红色光线绘制与之垂直的弧矢面（$x-z$ 平面）光线扇，可观察到两个光线扇沿主光线聚焦于不同位置。该透镜中，子午光线聚焦点比弧矢光线聚焦点更靠近透镜。

[![像散示意图](https://free.picui.cn/free/2025/09/29/68da3416622c0.png)](https://free.picui.cn/free/2025/09/29/68da3416622c0.png)


从横向光线像差曲线上来看，若评价平面位于近轴像面处，当且仅当曲线与$x$轴重合，表明此时光线束汇聚到近轴像点上一点，即实现理想成像。以消球差透镜为例。其7°、10°的横向光线像差曲线中，无论子午面还是弧矢面，其曲线均与$x$轴有夹角，这就说明，光线束中的不同光线在近轴像面处并不相交于一点，这点从切面图上也可以看到，其子午面和弧矢面光线束均在近轴像面前的地方汇聚。

[![消球差透镜切面图.png](https://free.picui.cn/free/2025/09/29/68da294bf0867.png)](https://free.picui.cn/free/2025/09/29/68da294bf0867.png)

可以使用**optimize>slider**进行观察。现在像面前插入一个离焦面即S5，在slider进行如下设置：

[![Slider](https://free.picui.cn/free/2025/09/29/68da391f4b808.png)](https://free.picui.cn/free/2025/09/29/68da391f4b808.png)

Parameter设置为厚度，surface选择5，satrt设置为-1.5至+1.5。通过移动滑块，横向像差曲线也会发生变化，即可看到不同视场下，子午光线和弧矢光线在哪里汇聚。

















