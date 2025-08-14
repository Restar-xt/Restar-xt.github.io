---
title: Designing Optics Using Zemax Chapter5 Stops&Pupils&Windows
tags: [Zemax]
categories: [光设软件基础-Zemax]
date: 2025-8-13
description: 本笔记参考 《Designing Optics Using Zemax》。
articleGPT: 在将镜头输入 OpticStudio® 后通过近轴像面厚度求解确定轴上物点的像平面位置后，需进一步评估该镜头离轴物点的成像表现。首先在物平面选取少量代表扩展物体的视场点，随后引入孔径光阑、视场光阑、入/出瞳及入/出窗等核心概念以分析光线在系统中的传播路径。这些定义看似繁琐，但需明确：镜头的本质功能是实现物体至像面的辐射能传输。若成像亮度不足或物体未能完整成像，即使轴上分辨率表现再佳，该设计仍为失败。初学者首次接触光学系统的光瞳与光阑概念时往往感到困惑——此亦本章标题的由来。本章目标在于清晰阐释光阑、光瞳及视场窗等概念原理，使学习者能在光学系统构建与评估中游刃有余地运用这些核心要素。
references:
  - title: 《Designing Optics Using Zemax OpticStudio》
  - url: https://ebooks.spiedigitallibrary.org/ebooks/PM/designing-optics-using-zemax-opticstudio/eISBN-9781510668577/10.1117/3.100004
   
---


# 《Designing Optics Using Zemax 》 Chapter5 Stops and Pupils and Windows（光阑、入瞳出瞳、入射出射窗）

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

在将镜头输入 OpticStudio® 后通过近轴像面厚度求解确定轴上物点的像平面位置后，需进一步评估该镜头离轴物点的成像表现。首先在物平面选取少量代表扩展物体的视场点，随后引入孔径光阑、视场光阑、入/出瞳及入/出窗等核心概念以分析光线在系统中的传播路径。这些定义看似繁琐，但需明确：镜头的本质功能是实现物体至像面的辐射能传输。若成像亮度不足或物体未能完整成像，即使轴上分辨率表现再佳，该设计仍为失败。初学者首次接触光学系统的光瞳与光阑概念时往往感到困惑——此亦本章标题的由来。本章目标在于清晰阐释光阑、光瞳及视场窗等概念原理，使学习者能在光学系统构建与评估中游刃有余地运用这些核心要素。

## Fields 视场

### Zemax输入镜头参数

**5mm thick NBK-7 equiconvex singlet lens（5mm厚N-BK7等凸单透镜）**

- 厚度（thick）：$d=5mm$
- 材质：$N-BK7$
- 半径（radius）：$R_{1}=-R_{2}=60mm$
- 物距：$120mm$
- 入瞳直径（entrance aperture）: $20mm$
- 工作波长（wavelength）：$d-line \space\space 0.5876nm$

#### 设定入瞳直径 System Explorer>Aperture
[![入瞳直径设定](https://free.picui.cn/free/2025/08/13/689c4665294bf.png)](https://free.picui.cn/free/2025/08/13/689c4665294bf.png)

#### 设定视场System Explorer>Fields

> Note: **For finite object distances (like this one), it is important to change the object field specification in the System Explorer (System Explorer > Fields > Settings > Type) from Angle to Object Height as angular fields of view only make sense for objects at infinity.**

注意：对于有限远的物距，需要将视场类型由**Angle**改变为**Object Height**，因为角视场只对于无限远处物体才有意义。

[![修改视场类型，Object Height](https://free.picui.cn/free/2025/08/13/689c46646aff1.png)](https://free.picui.cn/free/2025/08/13/689c46646aff1.png)

#### 设定工作波长 System Explorer>Wavelengths
[![波长设定.png](https://free.picui.cn/free/2025/08/13/689c467582244.png)](https://free.picui.cn/free/2025/08/13/689c467582244.png)

#### 输入镜头数据 Lens Data

[![chapter5LDE数据.png](https://free.picui.cn/free/2025/08/13/689c4675b4d16.png)](https://free.picui.cn/free/2025/08/13/689c4675b4d16.png)

#### 查看切面图 Layout 
[![Layout.png](https://free.picui.cn/free/2025/08/13/689c4b5c03677.png)](https://free.picui.cn/free/2025/08/13/689c4b5c03677.png)

### 分析离轴性能

#### 分析方法-三点法

对于离轴性能分析，我们可以在离轴处增加物方点进行分析。但是问题是**选多少个物方点？** **如何选取物方点？**

一般采取**三点法**，将中点设置为全视场高度$h$的$0.707$倍，即$(1/\sqrt{2})h$处，这样一来，以中点距离为半径的圆形区域面积恰好等于全视场总面积的一半。这种取点方式，赋予三个视场点等面积加权性质，能够有效表征整个物方视场的性能。3个视场点分表标记为：**$Full(F3)、Mid(F2)、Axis(F1)$**，即轴心、中场、全视场。

[![三点示意图](https://free.picui.cn/free/2025/08/13/689c5406cbb2d.png)](https://free.picui.cn/free/2025/08/13/689c5406cbb2d.png)

#### 在Zemax中设置三点 Field Data Editor

[![Setup-Editors-Field Data Editor](https://free.picui.cn/free/2025/08/13/689c603205008.png)](https://free.picui.cn/free/2025/08/13/689c603205008.png)

FDE操作和LDE（镜头数据编辑器）操作相同，insert插入行，delete删除列，按照三点法以及原始设置的镜头数据，在FDE内依次输入$Y$坐标，大小分别为0，14（取0.7即可），20。FDE右侧即为视场点图像。
[![屏幕截图 2025-08-13 180512.png](https://free.picui.cn/free/2025/08/13/689c635c60cde.png)](https://free.picui.cn/free/2025/08/13/689c635c60cde.png)

设置完成后打开Layout查看截面图：
[![Layout3.png](https://free.picui.cn/free/2025/08/13/689c6aa1d9bc9.png)](https://free.picui.cn/free/2025/08/13/689c6aa1d9bc9.png)

可以明显发现，**离轴点离轴程度越高，成像质量越差，体现在像面弥散斑越大**。

可以使用3D视图查看3D图像，**Setup>System Viewers>3D Viewer**
[![3DLayout.png](https://free.picui.cn/free/2025/08/13/689c6db46a6dc.png)](https://free.picui.cn/free/2025/08/13/689c6db46a6dc.png)


## Special Rays 特殊光线

**在明确物面场的对应关系后，通过多组特殊定义的射线可进一步简化系统分析。**

### Meridional or tangential rays 子午光线

可以在3D Layout Settings>Field>3，选择3仅保留$F3$场点，并将3D Layout Settings>Ray Pattern改为Y Fan，即Y扇形模式。

[![YFan光线束.png](https://free.picui.cn/free/2025/08/13/689ca8198fbfe.png)](https://free.picui.cn/free/2025/08/13/689ca8198fbfe.png)

**凡处于包含发光物点与光学主轴平面内的射线，均属子午射线**。

### Sagittal Rays 弧矢光线

与子午射线共用主光线，**与子午扇面垂直成直角的扇面**为弧矢扇面。

[![XFan光线束.png](https://free.picui.cn/free/2025/08/13/689ca76c448ff.png)](https://free.picui.cn/free/2025/08/13/689ca76c448ff.png)

观察发现，**来自同一物点的子午光线束和弧矢光线束各自的聚焦点并不在同一个平面上，这就是像散(astigmatism)**

### Skew Rays 斜射线 

子午光线因其传播路径限定于一个平面内，且该平面必须同时包含物点与光轴，故呈现出独特的性质。然而绝大多数由物点发出的光线并不满足此约束条件，此类光线被定义为空间光线。以上图所示弧矢光束为例，除中心光线外，其余光线皆属斜光线——该中心光线因其所在平面同时贯穿物点与光轴，其性质正符合子午光线的定义。

### Axis Rays 轴向光线

从轴上点发出的一束轴向光线。需要在3D Layout Settings>Ray Pattern改为Ring，即环形模式。

[![Axis Rays.png](https://free.picui.cn/free/2025/08/14/689d2dadcacfc.png)](https://free.picui.cn/free/2025/08/14/689d2dadcacfc.png)


### Rays for objects at infinity 无限远处物体发出的光线

在等凸透镜的上述示例中，我们采用有限物距的物体阐释了光学设计中的视场与特征光线路径。当物体位于无穷远时，其高度将趋近无限大（例如：**一与光轴夹角为7°的物点，在10¹³ mm物距条件下高度将达1.2187×10¹² mm**）。对于无穷远物距场景，宜采用光线与光轴的夹角（而非物高）表征物点位置。在OpticStudio软件中，可通过视场数据编辑器（Field Data Editor，FDE）将视场类型由"**Object Height**"切换为"**Angle**"实现该设定。

在物距有限远的条件下，对于离轴性能分析，我们可以在离轴处增加物方点进行分析，使用**三点法**进行分析；同样地，在物距无限远的条件下，对于离轴性能分析，可以在物方**增加多个视场角**进行分析。

本文中的诸多设计示例采用无穷远物体，并应用一组标准角度（0°、7°、10°）。鉴于此类角度指光轴与来自物点光线之间的夹角，故视场角表征为透镜角度覆盖范围的一半。因此，全角度覆盖范围达20°。

[![选择角度.png](https://free.picui.cn/free/2025/08/14/689d5290b9064.png)](https://free.picui.cn/free/2025/08/14/689d5290b9064.png)

[![Angle-YFan.png](https://free.picui.cn/free/2025/08/14/689d53876990b.png)](https://free.picui.cn/free/2025/08/14/689d53876990b.png)

[![Angle-XFan.png](https://free.picui.cn/free/2025/08/14/689d53874da46.png)](https://free.picui.cn/free/2025/08/14/689d53874da46.png)

[![Angle-XYFan.png](https://free.picui.cn/free/2025/08/14/689d538771b70.png)](https://free.picui.cn/free/2025/08/14/689d538771b70.png)


## The Aperture Stop and Marginal Rays 孔径光阑与边缘光线

在光学系统的设计和优化中，最有用的概念之一是孔径光阑的大小和位置。**孔径光阑是透镜组件中用以限制轴上光束尺寸的开孔。改变光阑的大小和位置往往可以极大地改善透镜的性能。** 

**然而，当孔径光阑发生改变时，系统中其他孔径的尺寸必须相应调整，以确保新的孔径光阑
能够有效控制轴向光线束的传输范围。**

### Zemax输入镜头参数

- Entrance Pupil Diameter（入瞳直径）：$10mm$
- Wavelength（工作波长）：$d-line$
- Fields（视场）：$0°$

上述操作类同前文，只需要修改部分数据即可。

#### 输入镜头数据 Lens Data
[![镜头数据.png](https://free.picui.cn/free/2025/08/14/689db6c5dfb6d.png)](https://free.picui.cn/free/2025/08/14/689db6c5dfb6d.png)

#### 查看切面图 Layout 
[![Layout2.png](https://free.picui.cn/free/2025/08/14/689dba3a68f7b.png)](https://free.picui.cn/free/2025/08/14/689dba3a68f7b.png)

#### 查看一阶数据 First-order

**Programming>MacroList**

```
File: asdoubletAxis.zmx
Title: 
Date: 2025/8/14

Infinite Conjugates
 Effective Focal Length       49.6049
 Back Focal Length       19.1683
 Front Focal Length       -9.1683
 F/#        4.9605
 Image Distance       19.1683
 Lens Length       58.0000
 Paraxial Image
 Height        0.0000
 Angle        0.0000
 Entrance Pupil
 Diameter       10.0000
 Location       40.4366
 Exit Pupil
 Diameter       10.0000
 Thickness      -30.4366

Object space positions are measured with respect to the first surface vertex
Image space positions are measured with respect to the last surface vertex
```

### 结论

> For the given EPD of 10 mm, the program automatically calculates the size (semi-aperture) of the stop surface needed to pass all of the rays from an axial object point. This semi-aperture or Clear Semi-Diameter (CSD) is listed in the LDE under the Clear Semi-Dia column as 3.516. Therefore, the stop surface’s circular aperture is 7.032 mm in diameter

对于给定的10 mm入瞳直径（EPD），该程序自动计算出需要通过所有轴上物点光线的光阑面尺寸（半孔径）。该净半口径（CSD）数值3.516已列于镜头数据编辑器（LDE）的"净半口径"栏中，因此相应光阑面的圆形孔径直径为7.032 mm。

- EPD (Entrance Pupil Diameter)：入瞳直径
- Clear Semi-Diameter (CSD)：净半口径（表征实际通光范围）/净口径
- stop surface：光阑面（核心光学元件）

### 改变数据观察结果

> Change the entrance pupil diameter of the OSasdoubletAxis to 20 mm and determine the diameter of the aperture stop that is needed to pass all rays from an axial object point using the LDE. When you finish this exercise, change the EPD back to 10 mm before you continue the narrative in the text.

将入瞳直径由10mm更改为20mm，观察光阑面尺寸大小。
[![更改入瞳直径为20mm后的LDE数据.png](https://free.picui.cn/free/2025/08/14/689dc24f4174c.png)](https://free.picui.cn/free/2025/08/14/689dc24f4174c.png)

可见光阑面CSD尺寸为7.005mm，则光阑直径应为14.01mm。

### 设置余量

OpticStudio会计算每个视场点所有光线通过各镜面所需的净口径（CSD），并将其列于镜头数据编辑器（LDE）的Clear SemiDiameter栏中。横截面示意图中，透镜表面随即根据这些尺寸绘制边界。如下图所示的空气间隔双胶合透镜，其光线示意图被绘制至镜片表面的**理论极限边缘**。

然而**在实际制造过程中，透镜的加工直径通常需大于光线追迹确定的净口径尺寸**。**该设计冗余旨在为清边区域外的表面保留额外空间：用于容纳抛光不均匀缺陷（通常称为"塌边"），为镀膜夹具提供操作区域，并为透镜组装的安装区域预留空间**。基于此工程考量，可通过**适当增大透镜直径的方式优化绘图效果，使其更符合实际生产情形**。

**可以在System Explorer > Aperture > Clear Semi Diameter Margin %进行余量设置。**


#### 数据对比

[![原数据.png](https://free.picui.cn/free/2025/08/14/689dcf9dd7503.png)](https://free.picui.cn/free/2025/08/14/689dcf9dd7503.png)

[![更改净口径余量后的数据.png](https://free.picui.cn/free/2025/08/14/689dc24f4174c.png)](https://free.picui.cn/free/2025/08/14/689dc24f4174c.png)

**设置余量后发现光阑的净口径和像面的净口径都不变。**

>在光学设计中，光阑（Stop）和像面（Image Surface）的 **CSD（Clear Semi Diameter）** 不需要增加余量的原因如下：
>### 📌 1. **光阑的功能特性**  
>  - **核心作用**：光阑是约束系统光束孔径（而非机械孔径）的关键元件，其大小需严格匹配目标F/#和视场角计算出的 **入瞳/出瞳尺寸（Entrance/Exit Pupil）**。  
> - **影响直接性**：增大光阑的CSD会导致无效光线进入系统（超出理论孔径），破坏像差控制逻辑并产生杂散光。  
> - **设计原则**：光阑尺寸在光学设计初期即被确定，必须严格保持其理论值 ⚠️。
>### 📐 2. **像面的物理约束**  
 >  - **匹配探测器**：像面CSD必须等于或略大于 **探测器靶面尺寸**，过大的CSD会导致：  
     - 错误模拟实际成像区域（有效光线可能被裁剪或干扰杂光分析）  
     - 影响公差分析和工艺装配的准确性  
>   - **公差处理**：探测器装配偏移的容差通常在独立公差模块（如Zemax的Tolerance）中设置，而非通过增大CSD实现。
>### 🛠 3. **透镜CSD余量的意义**  
>   - **机械安全区**：对折射/反射镜增加CSD余量（如10%）是为了预留：  
     - 镜片安装公差（偏心、倾斜）  
     - 温度形变缓冲空间  
     - 镀膜/抛光工艺的边缘裕度  
>   - **光能/像质无关**：此操作不影响光线追迹模型，仅保证透镜机械边缘**不遮挡设计孔径内的有效光线**。

---

> ### 📚 **操作逻辑总结**  
>| **元件类型** | **CSD调整需求** | **原因** |  
>|--------------|----------------|----------|  
>| 透镜表面     | **需增加余量** | 预留机械公差与热膨胀空间 |  
>| 光阑         | **禁止改动**   | 维持系统理论孔径角不变 |  
>| 像面         | **禁止改动**   | 匹配探测器实际尺寸 |  

---

>✅ 结论：光阑和像面的CSD不可增加余量是出于**光学功能的核心约束**——前者控制光束传播路径，后者对接物理探测器。而透镜CSD增加余量仅解决**机械可靠性问题**，不影响光学模型的准确性。

#### 切面图对比

[![原切面图.png](https://free.picui.cn/free/2025/08/14/689dcfd3dd35c.png)](https://free.picui.cn/free/2025/08/14/689dcfd3dd35c.png)

[![更改净口径余量后的切面图.png](https://free.picui.cn/free/2025/08/14/689dcfd3c294c.png)](https://free.picui.cn/free/2025/08/14/689dcfd3c294c.png)
