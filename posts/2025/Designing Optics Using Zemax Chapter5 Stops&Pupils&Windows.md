---
title: Designing Optics Using Zemax Chapter5 Stops&Pupils&Windows （光阑+光瞳+出入射窗）
tags: [Zemax]
categories: [光设软件基础-Zemax]
date: 2025-8-18
description: 本笔记参考 《Designing Optics Using Zemax》
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

### 光阑尺寸自动计算

> For the given EPD of 10 mm, the program automatically calculates the size (semi-aperture) of the stop surface needed to pass all of the rays from an axial object point. This semi-aperture or Clear Semi-Diameter (CSD) is listed in the LDE under the Clear Semi-Dia column as 3.516. Therefore, the stop surface’s circular aperture is 7.032 mm in diameter

对于给定的10 mm入瞳直径（EPD），该程序自动计算出需要通过所有轴上物点光线的光阑面尺寸（半孔径）。该净半口径（CSD）数值3.516已列于镜头数据编辑器（LDE）的"净半口径"栏中，因此相应光阑面的圆形孔径直径为7.032 mm。

- EPD (Entrance Pupil Diameter)：入瞳直径
- Clear Semi-Diameter (CSD)：净半口径（表征实际通光范围）/净口径
- stop surface：光阑面（核心光学元件）

### 改变入瞳直径观察结果

> Change the entrance pupil diameter of the OSasdoubletAxis to 20 mm and determine the diameter of the aperture stop that is needed to pass all rays from an axial object point using the LDE. When you finish this exercise, change the EPD back to 10 mm before you continue the narrative in the text.

将入瞳直径由10mm更改为20mm，观察光阑面尺寸大小。
[![更改入瞳直径为20mm后的LDE数据.png](https://free.picui.cn/free/2025/08/14/689dc24f4174c.png)](https://free.picui.cn/free/2025/08/14/689dc24f4174c.png)

可见光阑面CSD尺寸为7.005mm，则光阑直径应为14.01mm。

### 设置净口径余量

OpticStudio会计算每个视场点所有光线通过各镜面所需的净口径（CSD），并将其列于镜头数据编辑器（LDE）的Clear SemiDiameter栏中。横截面示意图中，透镜表面随即根据这些尺寸绘制边界。如下图所示的空气间隔双胶合透镜，其光线示意图被绘制至镜片表面的**理论极限边缘**。

然而**在实际制造过程中，透镜的加工直径通常需大于光线追迹确定的净口径尺寸**。**该设计冗余旨在为清边区域外的表面保留额外空间：用于容纳抛光不均匀缺陷（通常称为"塌边"），为镀膜夹具提供操作区域，并为透镜组装的安装区域预留空间**。基于此工程考量，可通过**适当增大透镜直径的方式优化绘图效果，使其更符合实际生产情形**。

**可以在System Explorer > Aperture > Clear Semi Diameter Margin %进行余量设置。**


#### 数据对比

[![原数据.png](https://free.picui.cn/free/2025/08/14/689dcf9dd7503.png)](https://free.picui.cn/free/2025/08/14/689dcf9dd7503.png)

[![更改净口径余量后的数据.png](https://free.picui.cn/free/2025/08/14/689dd4e641765.png)](https://free.picui.cn/free/2025/08/14/689dd4e641765.png)

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

### 增加离轴场点

在System Explore>Fields>Field Data Editor中添加两个离轴场点，分别为7°、10°。并在切面图中的settings中将绘制光线数量调整为3。这三条光线分别为：一条经过光阑中心的主光线，两条经过光阑边缘的边缘光线。切面图如下图所示：

[![增加离轴物点后的切面图.png](https://free.picui.cn/free/2025/08/15/689e95e624260.png)](https://free.picui.cn/free/2025/08/15/689e95e624260.png)

从上图也可以明显看出，增加离轴场点以后，透镜口径自动增大，以保证离轴场点光线通过。原因是：点击表面S2对应CSD列"11.234"数值旁的方框，将弹出"Clear Semi-Doameter solve on surface2"下拉菜单，其"solve type"显示为"Automatic"。这表明S2的通光孔径已实现自动计算。

### Pupil Aberrations 光瞳像差

#### 现象

孔径光阑（也称为光圈或光圈孔径）是光学透镜系统中的关键部件，它就像一个“门”，专门限制来自轴上视场（optical axis，即系统中心轴）的光线输入量。在理想情况下：

- 如果没有其他遮挡物（如额外的光圈或物理障碍），孔径光阑不仅能限制轴上光线，还应限制来自离轴视场点（off-axis field points，即远离系统中心的点）的光线。
- 离轴光线也应完全“填充”光阑表面，即光线均匀通过开孔区域，形成光斑。
这类似于一个房间的门：当人站在门正前方（轴上），只能部分通过；当人站在角落（离轴），也应该能部分通过门洞。理论上，所有光线都该顺畅地穿过这扇门。

然而放大光阑处的图像：

[![放大后光阑处的图像](https://free.picui.cn/free/2025/08/15/689e9da483ddc.png)](https://free.picui.cn/free/2025/08/15/689e9da483ddc.png)

发现**离轴视场的边缘光线（marginal rays）无法完全填充光阑的下部**。这意味着光线分布不均匀——有些区域被遮挡而不通过，导致光能量损失或成像变形。原因在于像差（aberrations），特别是光瞳像差（pupil aberrations）：
- 像差是光学设计缺陷，使光线传播发生扭曲（比如因透镜形状不完美）。
- 光瞳像差是一种高级像差类型，指孔径光阑的“像”（image of the stop）在物方空间（object space，即物体侧）中变得异常：或严重变形（aberrated）、或位置偏移（shifted）、或角度倾斜（tilted）。

本例的描述表明，光学系统中的透镜设计导致光阑图像失真，从而使离轴光线不能充分覆盖整个开孔区。这是一个复杂话题，需要深入研究镜头设计，初学者可先理解为“扭曲的镜子导致光线路径混乱”。简单比喻：就像门本身的影子被扭曲了，角落的人无法顺利找到入口

#### 软件解决方案

当前，OpticStudio 采用名为光线瞄准（ray aiming）的算法修正此类偏差。

该算法通过精确计算物方空间中各视场点对应特定孔径光阑尺寸的光线路径，确保光阑表面被正确填充。一般而言，当物方空间所观测的光瞳像出现明显偏差、位置偏移或角度倾斜时，需启用光线瞄准功能。考虑到计算效率优化，系统初始设置中默认关闭此功能，以优先确保光线追迹效率。

光线瞄准功能可以在**System Explorer > Ray Aiming**中打开，从下拉菜单中选择"Paraxial"。Ray Aiming开启和关闭对比如下：

[![Ray Aiming Paraxial.png](https://free.picui.cn/free/2025/08/15/689ea2fd5db6d.png)](https://free.picui.cn/free/2025/08/15/689ea2fd5db6d.png)

[![Ray Aiming Off.png](https://free.picui.cn/free/2025/08/15/689ea2fd5d88e.png)](https://free.picui.cn/free/2025/08/15/689ea2fd5d88e.png)

打开光线瞄准后的镜头数据如下：
[![镜头数据](https://free.picui.cn/free/2025/08/15/689ead1d23ff6.png)](https://free.picui.cn/free/2025/08/15/689ead1d23ff6.png)

### 改变系统孔径光阑

**surface4为光阑面**的透镜原数据如下：

[![surface4为光阑面](https://free.picui.cn/free/2025/08/15/689ead1d23ff6.png)](https://free.picui.cn/free/2025/08/15/689ead1d23ff6.png)

将**surface2改为光阑面**后的透镜数据如下：

[![屏幕截图 2025-08-15 115205.png](https://free.picui.cn/free/2025/08/15/689eb1c1d2c0d.png)](https://free.picui.cn/free/2025/08/15/689eb1c1d2c0d.png)

**S5与S6镜组的孔径增大**（旨在消除10°离轴光束在第二透镜处产生的剪裁效应），同时第一透镜处的光束尺寸相应缩小。

[![surface2为光阑面时的切面图](https://free.picui.cn/free/2025/08/15/689ee03a0d2b1.png)](https://free.picui.cn/free/2025/08/15/689ee03a0d2b1.png)



### 关于光阑的对称性设计

上文中surface4处放置光阑具有对称性，这种对称性不仅能**优化透镜性能**，其**对称结构对制造与装配更具重要实践意义**。基于对称特征，该设计可采用两片直径相同的全同透镜实现制作，其优势如下：**仅需单一型号透镜元件，且系统中任意位置均可互换安装。**

[![对称设计切面图](https://free.picui.cn/free/2025/08/15/689efd8f9d4f2.png)](https://free.picui.cn/free/2025/08/15/689efd8f9d4f2.png)

## Chief Rays and Pupils of a Lens 主光线与透镜光瞳

### Chief Rays 主光线

> A chief ray is a ray that goes through the center of the aperture stop.

**主光线是穿过孔径光阑中心的光线**。对于一个光学系统来说，有无数个场点，**每个场点都有一条经过光阑中心的主光线**。

同样，每个场点都有自己的一组边缘光线，但是通常对于一个场点，**总是由其通过光阑上边缘的一条边缘光线和一条主光线进行表征。** 在**System Viewer>Cross-Section>settings**中，选择绘制光线数量为1，可得单个场点的主光线：

[![单个场点主光线](https://free.picui.cn/free/2025/08/17/68a1f08138847.png)](https://free.picui.cn/free/2025/08/17/68a1f08138847.png)

选择绘制光线数量为2，可得单个场点的上下两条边缘光线：

[![单个场点的两条边缘光线](https://free.picui.cn/free/2025/08/17/68a1f0813174f.png)](https://free.picui.cn/free/2025/08/17/68a1f0813174f.png)

选择绘制光线数量为3，可得单个场点的主光线与上下两条边缘光线：

[![单个场点的主光线与两条边缘光线](https://free.picui.cn/free/2025/08/17/68a1f081372d8.png)](https://free.picui.cn/free/2025/08/17/68a1f081372d8.png)




### Entrance Pupil 入瞳

> Question: 当光阑在第一个透镜表面时，进入光学系统入射光束的大小很容易确定。它等于第一个透镜表面的直径（孔径光阑直径）。但是**如果孔径光阑被设置在透镜内部，那么如何才能确定入射光束的大小？**
尽管初看这似乎是一个无足轻重的问题，但**透镜可收集的光束截面尺寸直接决定了其在弱光环境、高速成像条件下的工作效能，以及其是否适用于高分辨率应用场景。评定透镜聚光能力的核心参数是其入瞳直径**。

入瞳被定义为从物体空间看到的光阑的图像。（光阑通过位于光阑之前的光学系统所成的像）。

- 当光阑位于透镜前表面时，前表面即为入瞳，前表面直径即为入瞳直径。
- 当光阑在系统内部时，光阑变成被成像的物体，经过光阑前面的光学元件成像在物空间，利用光学基本定律即可求出光阑的像，从而得知入瞳的位置与大小。

入瞳的重要性在于其作为限制入射光量的关键孔径。当轴上物点发出的锥状光束充满入瞳时，经物像共轭原理可见该光束将在孔径光阑处实现完全填充。**入瞳决定了光学系统可收集并汇聚至像平面的光通量极限。**

删除上文中LDE中的偏移面，运行FIRST宏，结果如下：
```
File: asdoubletSym.zmx
Title: 
Date: 2025/8/15

Infinite Conjugates
 Effective Focal Length       49.6049
 Back Focal Length       19.1683
 Front Focal Length      -19.1683
 F/#        4.9605
 Image Distance       19.1683
 Lens Length       48.0000
 Paraxial Image
 Height        8.7467
 Angle       10.0000
 Entrance Pupil
 Diameter       10.0000
 Location       30.4366
 Exit Pupil
 Diameter       10.0000
 Thickness      -30.4366

Object space positions are measured with respect to the first surface vertex
Image space positions are measured with respect to the last surface vertex
```

### Exit Pupil 出瞳

出瞳被定义为从像空间看到的光阑的图像。（光阑通过位于光阑之后的光学系统所成的像）。在此不再赘述。

## The Field Stop and Its Windows 视场光阑及其窗口

在光学系统的集光极限由孔径光阑及光瞳的尺寸与位置确定后，需进一步考量系统可容纳的**最大成像尺寸**。因主光线代表来自物场特定点的光线束中央光线，成像边缘由光学系统可传输的最大视场角（或最大物点）处的主光线决定，此即系统的全视场主光线。限制该光线的系统元件即视场光阑。多数情况下，透镜系统的视场光阑为探测器（如数字CMOS阵列、摄影胶片框或其他光传感器）。此时光学元件需适当扩大尺寸以避免主光线被遮挡，如图所示。


[![A fan of chief rays through the OSasdoubletSym.](https://free.picui.cn/free/2025/08/16/689fe0657cad8.png)](https://free.picui.cn/free/2025/08/16/689fe0657cad8.png)


**简而言之，孔径光阑是限制透镜系统可传输的轴上物点光束尺寸的光学表面，而视场光阑则是限制系统最大视场尺寸的透镜系统内部表面。**

与孔径光阑类似，视场光阑的成像（称为视场窗）亦存在特定位置。对此双透镜系统而言，其出射窗定位较为直接：因视场光阑位于像空间内，故其本身即为出射窗。虽然确定系统入射窗稍显复杂，但通过空气间隔双透镜组从物空间观察时，可计算视场光阑所成像位置。若以传感器为视场光阑且其位于后焦平面（BFP），则入射窗位于无限远处。对于有限距离的物体，若以传感器为视场光阑，则入射窗位于物平面处。


## Aperture Stop and Field Stop 孔径光阑与视场光阑的区别

这两个光阑在光学系统中确实有本质区别，它们的核心功能和设计目标不同：
###  1.  孔径光阑(Aperture Stop / AS)
*   **核心作用** ：**限制通过系统的光能量（光通量）和控制像差大小。**
*   **如何限制光束**：
    *   它主要决定 **单个物点（无论是轴上点还是轴外点）** 发出的光束中，有多少比例的光线能通过整个系统。
    *   对于任何一个物点（尤其是轴向点），孔径光阑决定了到达其像点的主光线角度（决定了系统的F数或数值孔径）和光束的粗细。
*   **影响轴外光的原因**：对于轴外物点，由于光束是斜着射入系统的，孔径光阑的边缘会自然地“切割”掉光束最外缘的光线（导致渐晕现象）。但这并非其设计的主要目的，而是限制单个点成像光束带来的“副作用”。
*   **优先级**：在一个光学系统中，**孔径光阑是首要确定的**，它直接关系到系统的分辨率、亮度和核心像差。
### 2.  视场光阑(Field Stop / FS)
*   **核心作用** ：**明确定义系统的成像范围（视场），精确控制哪些部位的物点能够成像。**
*   **如何限制光束**：
    *   它位于**最终像面或其共轭面**附近（例如，中间实像面、探测器感光面、目镜的视场光阑位置）。
    *   它通过**完全阻挡特定区域的成像光线**来工作：
        *   对于视场角以内的物点，其中心光线（主光线）和大部分光束都能通过视场光阑成像。
        *   对于视场角以外的物点，其主光线甚至整个光束都会被视场光阑挡住，**完全无法成像**。
*   **重要性**：
    *   **清晰边界**：它决定了成像区域的形状（圆形、矩形）和大小。没有视场光阑，图像的边缘会非常模糊（暗角渐变），无法获得清晰的视场边界。🎯
    *   **阻挡杂光**：阻止视场以外的强杂散光进入探测器或眼睛，提高图像对比度。
    *   **无渐昏**：在视场光阑定义的视场内，理论上应无渐晕（即所有视场内物点的光束都同样大小不受阻碍地到达像面）。
### 为什么有了孔径光阑还需要视场光阑？
1.  **功能不同，目标明确**：
    *   **AS目标是控制单个点的成像质量**（分辨率、亮度）。
    *   **FS目标是定义整个成像平面的范围和边界清晰度**。
2.  **AS限制轴外光不完善且非目标**：
    *   虽然AS会因渐晕影响轴外点光束（部分遮挡），但它**无法精确地、彻底地、清晰地定义一个成像区域的边界**。其造成的边缘模糊过渡区对于很多应用（如摄像、显微镜、望远镜观测）是不可接受的。
    *   渐晕现象本身是AS位置带来的光学性质，而非其主动设计意图。
3.  **FS提供清晰的截止**：
    *   FS位于实像平面或其共轭面，可以直接、物理地“剪裁”最终的图像，提供清晰明确的视场边缘。
    *   **它是主动地、明确地定义了“什么能成像”（在视场内）和“什么不能成像”（在视场外）。** AS没有这个能力。
### 简单比喻
*   **孔径光阑 (AS) **：就像调节相机的**光圈**。开大光圈进光多，景深浅；缩小光圈进光少，景深大。它影响每个点成像的亮度和模糊程度（尤其是景深背景），但不决定相机能“看到”多宽的画面范围。
*   **视场光阑 (FS) **：就是相机**传感器或胶片的边框**。只有落在边框内的光线才能被记录下来形成图像。它决定了相机捕捉到的实际画面范围（视角），画框之外的内容完全不可见。这个边框就是最终的“剪裁工具”。
### 总结
*   **孔径光阑（AS）** 控制每个物点（尤其是中心点）发出的光量和光束角度，是系统核心光学性能的决定因素之一。它对轴外点的渐晕效果是伴随发生的附带现象。
*   **视场光阑（FS）** 负责精准界定成像区域的大小和几何形状边界，将系统实际成像的范围限定在期望的视场角以内，阻止视场外的光线进入成像通道，并提供清晰的视场边缘。它解决的是“哪些物点可以被成像到最终像面上”的问题。
因此，虽然孔径光阑客观上会影响轴外点的通光量（渐晕），但为了**明确划分成像范围、获得清晰边界、消除不必要的杂光**，视场光阑是必须设置的独立部件，两种光阑的功能不可替代。

## Tracing General Rays 追迹一般光线
在OpticStudio软件中，任何光学系统中的光线均可通过标准化方法进行描述：光线由物点（光线起始点）与入瞳点（定义光线传播方向）双坐标定位共同定义。为确保系统描述的普适性，通过**将实际坐标与其最大值的比值进行归一化处理**，**所有位置坐标均被映射至0至1的连续区间**。

在物点描述中，归一化视场坐标 $h$表征视场点与其最大值之比。当物方位于无穷远的镜头具有三个视场（0°、7°、10°）时，中间视场点对应 $h = 0.7$，而10°视场则对应 $h = 1.0$。由于该点可位于物平面内相对于光轴的任意位置，其坐标需标注下标 $x$ 或 $y$ 。因此，物平面内的任一点均可用坐标对 $(h_{x} ,  h_{y})$描述。同理，入瞳内的任一点由归一化光瞳坐标 $(p_{x} ,  p_{y})$标定。**基于这两组坐标系，任何通过光学系统传播的光线均可被精确定义和追迹。**

在OpticStudio中打开**Analysis > Rays & Spots > Single Ray Trace**，将物面坐标设置为$h_{x}=0$和$h_{y}=0$光瞳坐标设置为$p_{x}=0$及$p_{y}=1$，即轴上物点发出的边缘光线；将物面坐标设置为$h_{x}=0$和$h_{y}=1$光瞳坐标设置为$p_{x}=0$及$p_{y}=0$，即轴外物点发出的主光线。

[![(上)从轴上物点到入瞳边缘的边缘射线，(下)从离轴(全视场)物点到入瞳中心的主射线。](https://free.picui.cn/free/2025/08/16/689fedbf87085.png)](https://free.picui.cn/free/2025/08/16/689fedbf87085.png)

## Field and Pupil Specifications 视场和光瞳规格

在筛选镜头目录与专利库以获取新设计方案的初始候选结构时，尝尝将镜头的**光瞳孔径**与**视场角参数**（或围绕标称值的数值范围）作为搜索条件，从而缩小潜在备选方案范围。此外第三项规格——即**镜头有效焦距**，也通常被纳入筛选体系以约束光学系统的整体尺寸。**在多数设计任务中，这三项核心参数的确定远在设计工作启动前即已完成。**

### Field of View 视场

> 特定镜头所能记录的视场范围取决于其光学特性。举例而言，在棒球场内使用手持设备拍摄时，iPhone摄像头虽能记录相当范围的场地及看台区域，但其广角镜头无法清晰捕捉场地内的运动细节。相比之下，专业摄影师配备的窄角（长焦）镜头可在场边位置实现动作的特写拍摄，其成像细节表现卓越。这种**反映镜头场景覆盖角度的参数称为视场角。**

**视场角由全视场上下两条主光线之间的夹角进行表征。**

[![视场角表征视场示意图](https://free.picui.cn/free/2025/08/16/68a03bfb52e07.png)](https://free.picui.cn/free/2025/08/16/68a03bfb52e07.png)



仍以上文出现的空气隙双合透镜为例，可在**System Viewers>Cross-Section>Settings**中选择绘制光线数量为1即可看到全视场上下边缘对应的两条主光线。

[![视场角即为全视场上下两条主光线的夹角](https://free.picui.cn/free/2025/08/16/68a03bbfc2867.png)](https://free.picui.cn/free/2025/08/16/68a03bbfc2867.png)

对于一些光学系统，其视场范围取决于图像传感器的物理尺寸。在这种情况下，视场大小可被两个数据所表征。
- 近轴像高 paraxial image height
- 实际像高 real image height
- 二者的区别：在于是否考虑畸变的存在

对于理想光学系统，近轴像高可以用如下公式表示：
$$h'=f\tan{\theta}$$
在实践中，该方程**对验证一阶规格参数具有重要实用价值**。例如，在已知传感器尺寸及视场角的情况下，可基于物体空间至图像空间的映射关系计算所需镜头焦距。该方程亦能用于将传感器端的空间分辨率转换为观测目标的角分辨率。

在OpticStudio中，可以在FDE编辑器（Ctrl-F呼出）中，选择某一场点 点击Field x Properties，在Field Type中可以选择5种视场类型。

[![视场类型](https://free.picui.cn/free/2025/08/18/68a291ffef5cd.png)](https://free.picui.cn/free/2025/08/18/68a291ffef5cd.png)

由于大多数探测器呈矩形，只需同时输入x、y坐标即可定义位于探测器边角的像场点坐标。然而这种做法破坏了光学系统的圆形对称特性。更简捷高效的方式是：**计算探测器最小外接圆的半径，将其作为全视场y方向像高参数**。需特别注意，**视场尺寸与角度均以光轴与探测器中心的交点为基准进行测量**。

> 练习：The OSasdoubletSym is used to image an object at infinity onto a Canon APS-C sensor whose dimensions are 22.2 14.8 mm. Use Eq. (2.1) to find the three equal-area angular field points (axis, 0.7 field, and full field) that should be used to ensure that every point on the sensor is covered by the design.

分析：先寻找传感器的最小外接圆：
$$R=\sqrt{22.2^{2}+(14.8)^{2}}=26.7mm$$
则像点最大高度为：
$$h=\frac{R}{2}=13.3mm$$
由
$$h=f'\tan \theta$$
结合Zemax中$EFL=49.6$
则可得到：
$$\tan \theta=0.270$$
即：
$$\theta=15.0°$$
按照三点法取视场点，即可得到三个场点数值分别为0°，10.5°，15°。

### F-number and numerical aperture F数和数值孔径

上文提到入瞳直径EPD可以表征一个镜头的孔径大小。然而，更常见的用于表征镜头聚集光束能力的是其光圈数（F-number），该**数值定义为等效焦距（EFL）与入瞳直径（EPD）之比**。

$$F/\#=\frac{EFL}{EPD}$$


透镜的$F/\#$是EPD相对于焦距大小的量度。例如，对于$F/8$的镜头，表明该镜头的**有效孔径直径（EPD）等于该镜头等效焦距（EFL）的八分之一**。

一定注意，**F数数值大小即为$\#$的数值大小**，$/$没有任何含义，不要把$/$作为除号。

F值规格是镜头聚光能力的相对度量标准，其数值与镜头的特定有效焦距(EFL)无关。该分数值亦被称为镜头**速度**。速度反映了**F值越小，入瞳直径(EPD)相对于EFL越大**的物理特性。当聚光量增大时，捕捉高速运动物体变得更为容易。例如，**在相同EFL条件下，F/2镜头的EPD是F/8镜头的四倍**，能有效减少运动物体的成像模糊。这是因为F/2镜头可在更短的曝光时间内实现充分曝光，**此即摄影界将较小F值镜头称为"快速镜头"的学理依据**。

> 如何理解速度一词？
>1. **F值的本质：**  
   $F/\# = EFL / EPD$（即 **有效焦距 / 入瞳直径**）。  
   **F值越小，入瞳直径（EPD）相对于焦距（EFL）越大**，意味着镜头能捕获更多入射光线。
>2. **“速度”的由来 (光学层面)：**  
>   - **低F值（如 f/2）→ 大入瞳直径 → 单位时间进光量多 → 达到相同曝光所需的曝光时间更短**。  
>   - 曝光时间缩短 → **运动物体的位移在曝光期间减少 → 成像模糊度降低**。  
>   - 例：相同场景下，f/2镜头可能只需1/500秒曝光，而f/8镜头需1/60秒，前者更易冻结快速运动。
>3. **量化对比：**  
>   对于 **相同焦距** 的镜头：  
>   - F/2的EPD 是 F/4的 **2倍** → 进光面积是 **4倍**（光通量与EPD²成正比）。  
>   - F/2的EPD 是 F/8的 **4倍** → 进光量达到 **16倍**，故曝光时间可缩减为1/16。
>
>因此，摄影师称低F值镜头为"快速镜头"，本质是因其**能显著缩短曝光时间**，从而更高效地捕捉动态瞬间。这一特性在运动摄影、弱光摄影等场景中至关重要。

[![不同F数但视场均为40°的三种透镜](https://free.picui.cn/free/2025/08/17/68a1edb393467.png)](https://free.picui.cn/free/2025/08/17/68a1edb393467.png)

随着F/#值的减小，透镜元件数量增加，像面处的轴向边缘光线角增大，且表面曲率显著增强。大孔径短焦距透镜（如F/2镜头）通常属于高性能镜头，可呈现明亮清晰的成像效果，其成本可能较为昂贵。相比之下，图中另外两种镜头在相同视场尺寸下的性能表现较弱。若要满足高性能需求，需通过缩小视场尺寸或增加透镜元件来提升其光学表现。

下图展示了OpticStudio中六种不同的孔径设定选项（位于System Explorer > Aperture > Aperture Type）。除已阐述的入瞳直径（Entrance Pupil Diameter）与像方F数（Image Space F/#）外——此二者通常适用于物方位于无限远的光学系统——另有近轴工作F数（Paraxial Working F/#）和物方数值孔径（Object Space NA）更适用于有限物距透镜系统。其中工作F数作为F数的广义定义，该参数适用于有限物距场景，。其余两种孔径选项"浮动光阑尺寸"（Float by Stop Size）与"物方锥角"（Object Cone Angle）不在本文讨论范畴。

[![六种视场类型](https://free.picui.cn/free/2025/08/18/68a291ffef5cd.png)](https://free.picui.cn/free/2025/08/18/68a291ffef5cd.png)

| 序号 | 孔径类型 (Aperture Type)          | 使用场景                                                                 |
|------|----------------------------------|--------------------------------------------------------------------------|
| 1    | 入瞳直径 (Entrance Pupil Diameter) | 物方位于无限远的光学系统中的标准孔径定义                                           |
| 2    | 像方F数 (Image Space F/#)         | 物方位于无限远的光学系统（如天文望远镜）的设计场景                                      |
| 3    | 近轴工作F数 (Paraxial Working F/#) | **有限物距透镜系统**，作为F数的广义定义（适用于显微镜物镜等短物距设计）                     |
| 4    | 物方数值孔径 (Object Space NA)     | **有限物距透镜系统**（例如显微光学），直接关联物方光线收集能力                           |
| 5    | 浮动光阑尺寸 (Float by Stop Size)   | 特殊场景（文中未具体讨论）                                                     |
| 6    | 物方锥角 (Object Cone Angle)       | 特殊场景（文中未具体讨论）                                                     |

#### numerical aperture 数值孔径

数值孔径是衡量透镜聚光能力的另一个指标。

对于**无穷远处物点**，在**像空间**中，数值孔径定义为：
$$\mathrm{N}\mathrm{A}=n'\sin U'$$
其中，$U'$是轴上物体点在像空间中边缘光线的真实角度。

对于**有限的距离的物体**，在**物空间**中存在相应的数值孔径。物方数值孔径定义为
$$\mathrm{NA}=n\sin U$$
物体位于前焦点，光线被收集的角度范围（即光轴与入瞳直径边缘间的夹角范围）记为$U$。

> 注意，这里的$U$取绝对值

在OpticStudio软件中仅支持设置物空间数值孔径（Image Space F/#）；若需设定像空间指标，则应采用Image Space F/#（F数）或Paraxial Working F/#（工作F数）参数。

## Vignetting 渐晕

### 渐晕的定义

当指定场点时，只要通光孔径（CSD）设为自动模式，OpticStudio即可计算出确保该场点射线束通过透镜所需的透镜元件尺寸。然而当将实体透镜（其孔径由制造工艺及镜筒结构实际限定）输入程序进行分析时，**除轴上物点外，孔径光阑可能并非其他场点的实际限制孔径**。较大视场角的入射光线可能被某个组件阻挡，从而导致像面相应像点的光通量下降。这种**由元件尺寸引起的光通量衰减现象称为渐晕**。

> 解释：
> - 自动 CSDs 设置的作用：
>
>    - CSDs（Clear Semi-Diameters，净半直径）表示透镜的允许光线通过的范围。当设置为“自动”时,**软件会根据选定的场点（如轴向点）计算透镜尺寸——它确保该点发出的所有光线都能不被阻挡地穿过镜头。** 这类似于虚拟建模一个“完美系统”，**透镜会自动撑大以满足需求**。
例如：如果你指定一个物场中心点，软件就自动调整镜头直径，保证所有光线无阻碍地通过镜头，达到理想的传输效果。
>  - 实际镜头的限制与晕影（Vignetting）：
>       - 但当使用真实镜头（有固定尺寸，例如生产好的镜头装在镜筒里），孔径是预设的，不能像软件那样自动调整。
>       - 尽管系统有“孔径光阑”（限制光线的主要开口），但**其他镜片或镜筒会意外阻挡来自大角度入射的光线**。这导致像面边缘区域的亮度降低，称为“晕影”（vignetting）。它是由于固定大小的组件（如镜片外圆、镜筒接口）拦截了光线，本质是 光的渐晕效应（指照度随像点远离中心而下降的现象）。
> 
>       - **通俗类比：就像扩音喇叭安装在固定外壳中——理论上声音能传远，但外壳开口小了，边缘声音就被“吃掉”了**。在光学系统里，这会减少受影响点（image points）的光通量。

以上文出现的空气隙合对称透镜为例，设置12.5mm的CSD后，在FDE中增加一个14°的场点，在Cross-section>Settings中设置只绘制场点4（14°）的光线，且光线数量为7，则可得到下图：

[![光线截断](https://free.picui.cn/free/2025/08/18/68a32acabd773.png)](https://free.picui.cn/free/2025/08/18/68a32acabd773.png)

对于这个较大的场点，由于最底层的两条光线由于透镜边框的限制未能进入系统，所以透镜只传输五条光线。这就是一个简单的渐晕现象的例子，即物场边缘场点的光透射率的减少。

### Zemax分析渐晕

在光学系统设计中，为表征渐晕离轴视场的特性，需对**各视场建立渐晕光瞳模型以取代圆形入瞳**。该光瞳形貌可在OpticStudio软件中通过光斑图/足迹图（**Analyze > Rays & Spots > Footprint Diagram**）于孔径光阑面处观测。初启光斑图时显示所有四个场点在像面的光线分布，此时需切换至"Settings"选项卡，将"Surface"调整为4（即S4光阑面），同时确认"Ray Density"选项为"Ring"。点击确认后将呈现各视场点在光阑面的光线边界分布。、

[![FootprintDiagram](https://free.picui.cn/free/2025/08/18/68a332a969b75.png)](https://free.picui.cn/free/2025/08/18/68a332a969b75.png)

不难从上图看出，视场点123发出的光线均充满孔径光阑（入瞳），而视场点4的光线被截断。


将视场选项由"All"调整为"4"，单独分离16°视场研究渐晕效应的影响。随后将光线密度参数设定为50，点击OK后即可观测到16°视场内在孔径光阑面处50根光线构成的光线束光斑分布。rays through显示通过率仅80%。



[![视场点4光斑分布](https://free.picui.cn/free/2025/08/18/68a334761e6f7.png)](https://free.picui.cn/free/2025/08/18/68a334761e6f7.png)

**但是这种追踪光线的效率十分低下，为什么要追踪明知无法通过系统的那些光线呢？如何提高效率呢？**

可以在FDE中进行设置，设置每个视场的渐晕系数（VDX、VDY、VCX、VCY），点击设置渐晕系数后（图标如下），即可使得场点4的光线通过率100%，不再追踪其他无法通过的光线。

[![设置渐晕系数的图标](https://free.picui.cn/free/2025/08/18/68a33d0b98011.png)](https://free.picui.cn/free/2025/08/18/68a33d0b98011.png)

[![设置渐晕系数后的FDE](https://free.picui.cn/free/2025/08/18/68a33c9b4a12c.png)](https://free.picui.cn/free/2025/08/18/68a33c9b4a12c.png)

[![设置渐晕系数后通过率100%](https://free.picui.cn/free/2025/08/18/68a33b4be3d93.png)](https://free.picui.cn/free/2025/08/18/68a33b4be3d93.png)

在FDE中，每个视场点显示的四个渐晕参数（VDX、VDY、VCX、VCY）定义为：  

**VDX与VDY**分别表示渐晕光瞳在x和y方向的位移量。正值使光瞳向右（VDX）或向上（VDY）移动，负值则使光瞳向左（VDX）或向下（VDY）移动。  

**VCX与VCY**分别表征光瞳在x和y维度的压缩量（正值）或扩张量（负值）。  
所有参数值均进行了归一化处理（基准值为1）：  
- 位移参数值0.5表示光瞳实际尺寸的50%偏移（VDX/VDY）  
- 形变参数值0.5表示50%的压缩/扩张量（VCX/VCY）。  

[![四个参数示意图](https://free.picui.cn/free/2025/08/18/68a33f7a184e2.png)](https://free.picui.cn/free/2025/08/18/68a33f7a184e2.png)
