---
title: Designing Optics Using Zemax Chapter9  Chromatic Aberration（色差）
tags: [Zemax]
categories: [光设软件基础-Zemax]
date: 2025-10-08
description: 本笔记参考 《Designing Optics Using Zemax》
articleGPT: 本章主要介绍在在将镜头输入 OpticStudio® 后，如何分析系统色差。
references:
  - title: 《Designing Optics Using Zemax OpticStudio》
  - url: https://ebooks.spiedigitallibrary.org/ebooks/PM/designing-optics-using-zemax-opticstudio/eISBN-9781510668577/10.1117/3.100004
   
---




# 《Designing Optics Using Zemax 》 Chapter9  Chromatic Aberration（色差）

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

## 折射与色散

光学材料（如玻璃、晶体及塑料）具备密度、硬度等多种物性参数。针对光学设计需求，其核心材料特性在于折射率与色散。

由斯涅尔定律：

$$n'\sin i'=n\sin i$$

在光学界面处，当入射角为  $i$  且界面一侧介质的折射率为  $n$ ，另一侧入射角为  $i'$ 、折射率为  $n'$  时，若初始介质为空气，则其折射率 $n = 1$，**界面另一侧材料的折射率$n'$应如何确定？**

在之前的例子中，均指定了波长为d-line，当工作波长发生变化时，光学介质的折射率是否保持不变？成像结果是否保持不变？答案是否定的，**介质折射率随波长变化的现象被称为色散。**

### N-BK7折射率变化曲线

[![ N-BK7折射率变化曲线](https://free.picui.cn/free/2025/10/08/68e5d828b57aa.png)](https://free.picui.cn/free/2025/10/08/68e5d828b57aa.png)

图中标注的d线、F线与C线波长，对应夫琅和费于1814年在太阳光谱中发现的元素吸收线，**这些特征谱线被用于评估光学镜头在整个可见光谱区的性能**。其中氢原子发射的红色谱线（$λ_c=656.3nm [\text{H}\alpha]$）代表可见光谱区长波端，氦原子光谱中的黄色谱线（$λ_d=587.56nm [\text{He}]$）表征可见光谱区中心位置，氢原子发出的蓝色谱线（$λ_F=486.13nm [\text{H}\beta]$）则标志可见光谱区短波边界。

### Abbe number/V-number 阿贝数

光学材料的色散用阿贝数Abbe number或者V-number进行表示：

$$V=\frac{n_{d}-1}{n_{F}-n_{C}}$$

- $n_{d}$：代表材料对d光的折射率
- $n_{F}$：代表材料对F光的折射率
- $n_{C}$：代表材料对C光的折射率

观察阿贝数计算公式不难看出：分子$(n_{d}-1)$是一个小于1的正数，所以对于阿贝数数值大小影响最大的其实是分母$n_{F}-n_{C}$

- 对于**高色散玻璃**，其$n_{F}$与$n_{C}$差距较大，因此对应的**V-number较小**，这样的玻璃称为flints，即**火石玻璃**。
- 对于**低色散玻璃**，其$n_{F}$与$n_{C}$差距较小，因此对应的**V-number**较大，这样的玻璃称为crown，即**冕牌玻璃**。
- **冕牌玻璃V-number数值比火石玻璃大。**

::: danger
注意：上文提到的V-number的计算式仅适用于可见光波段。
:::

:::info
一旦选定特定光谱带，就需确定在该光谱带内均匀分布的波长数量，这些波长应允许设计人员对光学系统进行分析与修正，从而确保系统性能在整个光谱带内保持稳定性能。例如，光谱学领域存在多种适用于可见光波段之外的三波长组合（如同d、F、C基组一样），其中若干组合已被整合至OpticStudio®预设光谱库中（System Explorer > Wavelengths > Settings > Preset）。此类三波长组合可借助光谱带内的长波（$λ_{long}$）、中波（$λ_{mid}$）及短波（$λ_{short}$）波长，定义该光谱带的广义V值：
$$V_{gen} = \frac{n_{mid} - 1}{n_{short} - n_{long}} $$
:::

### glass map 玻璃图

对于光学制造商来说，绘制可制造的玻璃种类对应的中心波长折射率$n_{d}$和对应的V-number的关系图即为玻璃图。

[![肖特公司玻璃图](https://free.picui.cn/free/2025/10/08/68e6180f34a71.png)](https://free.picui.cn/free/2025/10/08/68e6180f34a71.png)

注意该图的特点：
- 横轴代表阿贝数即V-number，其正反向为从右至左，从右至左其V-number依次增大。
- 纵轴代表中心波长折射率$n_{d}$，其正方向为从上至下，从上至下其$n_{d}$依次增大。

该玻璃图的交互版本可以从：**Libraries > Material Analyses > Glass Map**获取。

### glass number 玻璃编号

有时，也可以通过玻璃编号指定某特定玻璃。即使用阿贝图涉及到的两个坐标，阿贝数与中心波长折射率。

**前三位数字为$n_{d}-1$保留最高三位的结果，后三位数字为V-number乘10倍的结果。** 以N-BK7为例，前三位数字为517（1.517-1=0.517），后三位数字642（64.2×10=642），因此N-BK7的玻璃编号为517642。最近，Schott对玻璃数进行了扩展，增加了一个小数点，后面是密度乘100倍并保留最高三位。即N-BK7的玻璃编号为517642.251。

::: info
**关于玻璃命名规则**

光学玻璃的命名体系存在多种惯例。部分玻璃制造商在其火石玻璃产品名称中加入"F"标识（如F2）；而冕牌玻璃则采用含"K"的命名规则（例如N-BK7，源于德语中"Krone"的拼写惯例）。另有一些企业采用纯数字命名法。通常情况下，制造商会提供跨公司产品的名称对照表。

N-BK7作为常见硼硅酸盐玻璃，常作为光学设计的初始材料。随着设计优化进程的推进，将逐步引入其他玻璃类型，最终可能实现N-BK7的替代。该材料原始名称为BK7，在传统透镜规格书中仍可见此称谓。

鉴于早期光学玻璃的化学成分中含有对生态环境不友好的物质（如铅、砷等），业界已通过配方革新实现有害成分剔除。改良后的新型玻璃通过前缀"N"进行标识（如N-SF5）。虽然新型玻璃（N-SF5）与原始型号（SF5）在折射率和阿贝系数方面高度近似，但因材料属性存在细微差异，导致采用新型材料制造的透镜在一阶光学参数上会产生可度量的变化。BK7与N-BK7属于特例，因其原始配方无需改良，故二者可互换使用。为避免术语混淆，本文统一采用N-BK7作为标准命名。

:::

## Longitudinal Chromatic Aberration 沿轴色差

有两种色差：

- **longitudinal chromatic aberration/axial color**：即沿轴色差/轴向色差/位置色差，英文翻译为纵向色差，比较容易混淆，此处纵向指的是以光轴为标准，沿光轴即为纵向。
- **transverse chromatic aberration/lateral color**：即垂轴色差/倍率色差，英文翻译为横向色差，比较容易混淆，此处横向指的是以光轴为标准，垂轴即为横向。

本小节主要研究前者，即沿轴色差，指的是随着光线波长（颜色）的不同，焦点位置会沿轴移动。

### LDE

[![用于研究色差的单透镜数据](https://free.picui.cn/free/2025/10/08/68e6253bbe30b.png)](https://free.picui.cn/free/2025/10/08/68e6253bbe30b.png)

设置入瞳直径为20mm，Field仅有轴向视场0°，**波长需要更改，更改为F,d,C(visible)。**

[![修改波长](https://free.picui.cn/free/2025/10/08/68e625bad7051.png)](https://free.picui.cn/free/2025/10/08/68e625bad7051.png)

选择正确波长后，**一定要点击Select Preset**才可以使设置生效。

[![生效后的波长](https://free.picui.cn/free/2025/10/08/68e626466de78.png)](https://free.picui.cn/free/2025/10/08/68e626466de78.png)

### Surface Data 查看表面数据

上图中的波长虽然只有三位小数，但实际上Zemax计算时的精度远比三位小数高，更加详细的信息可以通过**Analyze > Reports > Surface Data**进行查看，注意在点击之前，一定要在LDE中选中表面1（本例中表面1是N-BK7玻璃材料，才会有不同波长的折射率），即可显示波长(至五位有效数字)和N - BK7在这些波长(十位数字以内)处的折射率。

[![Surface Data打开方式](https://free.picui.cn/free/2025/10/08/68e629c9595d5.png)](https://free.picui.cn/free/2025/10/08/68e629c9595d5.png)

Surface Data部分数据如下：
```
Index of Refraction:
Glass: 	N-BK7
#  	    Wavelength   	 Index
1    	 0.48613   	    1.5223762897
2    	 0.58756   	    1.5168000345
3    	 0.65627   	    1.5143223473
```

### Prescription Data 处方数据

由于每个波长的折射率不同，因此透镜的EFL会随着波长的变化而变化。为了观察到这一点，可以通过Analyze > Reports > Prescription Data进行查看，Prescription Data与Surface Data按钮位于同一选择框，此处不再示意如何选择。

Prescription Data的部分数据如下：

```
                                 	Object Space           	Image Space
W = 	0.486133	
Focal Length          : 	         -49.470612 	          49.470612
Focal Planes          : 	         -48.763322 	          -0.520380
Principal Planes      : 	           0.707290 	         -49.990992
Anti-Principal Planes : 	         -98.233934 	          48.950232
Nodal Planes          : 	           0.707290 	         -49.990992
Anti-Nodal Planes     : 	         -98.233934 	          48.950232

W = 	0.587562	(Primary)
Focal Length          : 	         -50.000393 	          50.000393
Focal Planes          : 	         -49.290560 	          -0.000000
Principal Planes      : 	           0.709833 	         -50.000393
Anti-Principal Planes : 	         -99.290954 	          50.000393
Nodal Planes          : 	           0.709833 	         -50.000393
Anti-Nodal Planes     : 	         -99.290954 	          50.000393

W = 	0.656273	
Focal Length          : 	         -50.239467 	          50.239467
Focal Planes          : 	         -49.528498 	           0.234875
Principal Planes      : 	           0.710969 	         -50.004592
Anti-Principal Planes : 	         -99.767965 	          50.474342
Nodal Planes          : 	           0.710969 	         -50.004592
Anti-Nodal Planes     : 	         -99.767965 	          50.474342

```
长波长 C 处的有效焦距为 50.239mm，而短波长 F 处的有效焦距为 49.470mm。因此，该光谱带内焦距差值为 50.239 减去 49.470，即 0.769mm。**表示焦点位置随波长沿光轴发生的偏移，因此此误差被称为：位置色差/沿轴色差。**

### 沿轴色差的直观展示

需要在Layout窗口的Settings中进行设置，要将Color Rays By由Field#改为Wave#，Number Of Rays修改为3，即只绘制两条边缘光线以及主光线以便于清晰观察。

[![沿轴色差光线切面图.png](https://free.picui.cn/free/2025/10/08/68e6369027e7b.png)](https://free.picui.cn/free/2025/10/08/68e6369027e7b.png)

不难看出，由于蓝光折射率较大，汇聚焦点更加靠近透镜。

### 横向像差曲线

在理想情况下，即只有色差的情况下，横向像差曲线应该能看到三条斜率不同的直线，然而这种情况是不存在的，因为单透镜系统总是含有球差。为了减少球差对色差观察的影响，将系统入瞳直径减小到5mm，再进行观察。

[![横向像差曲线.png](https://free.picui.cn/free/2025/10/08/68e649345e57d.png)](https://free.picui.cn/free/2025/10/08/68e649345e57d.png)

不同波长曲线在原点处的斜率角存在差异。该图中黄色波长曲线（为清晰起见以绿色显示）与x轴相切，**表明该评估平面处于d光（主波长）的旁轴焦点位置。** 其他波长曲线的斜率则反映了色焦距误差的量值。

### 更换玻璃材料

N-BK7并非唯一可用的透镜玻璃材料（尽管在我们的案例使用中常给人这种印象）。光学制造商提供的玻璃产品目录为设计人员提供了丰富的材料选择空间。

在刚刚更改入瞳直径为5mm的基础上，将N-BK7冕牌玻璃换为F2火石玻璃，再次观察系统数据。

- Surface Data 表面数据

    ```
    Index of Refraction:
    Glass: 	F2
    #  	    Wavelength   	 Index
    1    	 0.48613   	    1.6320814568
    2    	 0.58756   	    1.6200401372
    3    	 0.65627   	    1.6150316916
    ```
    相比N-BK7，同样的参数下，F2对应的EFL为41.7329，这是因为F2折射率大，对光线的偏折（会聚）能力更强。

- transverse ray curves 横向像差曲线

  为了和N-BK7进行对比，首先要保证更换F2后，系统的F/#保持不变，即控制变量，让色差变化的原因只归结为一个，即材料的更换。**在透镜第二表面的曲率半径上求解边缘光线角可以用来保持50mm的EFL。**

  ::: danger
  **保持EFL在更改透镜材料后不变的方法**

  本方法不仅适用于更改透镜材料后保持不变，同样适用于表面半径、表面类型等。

  首先，要搞清楚EFL、EPD、F/#与边缘光线角度的关系：

  $$\text{F /\#}=\frac{\text{EPD}}{\text{EFL}}$$

  $$|\text{Marginal Ray Angle}|\approx\frac{0.5\cdot EPD}{EFL}$$
  
  根据上述，结合符号规则，要保证上文提到的参量不变，则可以对透镜第二表面使用边缘光线角度Marginal Ray Angle求解，填入数值-0.05rad。

  [![对透镜第二表面半径使用边缘光线角度求解](https://free.picui.cn/free/2025/10/08/68e657fd9b5f4.png)](https://free.picui.cn/free/2025/10/08/68e657fd9b5f4.png)
  :::

  对比更换玻璃材料前后的横向像差曲线：

  


| [![](https://free.picui.cn/free/2025/10/08/68e65a7c75b6c.png)](https://free.picui.cn/free/2025/10/08/68e65a7c75b6c.png)|[![](https://free.picui.cn/free/2025/10/08/68e6587c60b15.png)](https://free.picui.cn/free/2025/10/08/68e6587c60b15.png)|
|:--:|:--:|
| N-BK7 | F2 |

注意F2坐标单位长度比N-BK7大，换算后发现F2材质镜头的C谱线(红)与F谱线(蓝)焦平面分离程度显著加剧。
  
