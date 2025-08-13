---
title: 《Designing Optics Using Zemax》 Chapter5 Stops and Pupils and Windows
tags: [Zemax]
categories: [光学设计软件基础-Zemax]
date: 2025-8-13
description: 本笔记参考 Donald O’Shea and Julie Bentley的《Designing Optics Using Zemax》一书，主要讲述光学设计基础知识和Zemax的使用，该书从第5章开始系统按照光阑、像差、像质评价等顺序并结合Zemax进行说明，系统介绍了Zemax的各种功能与操作。
articleGPT: 在将镜头输入 OpticStudio® 后通过近轴像面厚度求解确定轴上物点的像平面位置后，需进一步评估该镜头离轴物点的成像表现。首先在物平面选取少量代表扩展物体的视场点，随后引入孔径光阑、视场光阑、入/出瞳及入/出窗等核心概念以分析光线在系统中的传播路径。这些定义看似繁琐，但需明确：镜头的本质功能是实现物体至像面的辐射能传输。若成像亮度不足或物体未能完整成像，即使轴上分辨率表现再佳，该设计仍为失败。初学者首次接触光学系统的光瞳与光阑概念时往往感到困惑——此亦本章标题的由来。本章目标在于清晰阐释光阑、光瞳及视场窗等概念原理，使学习者能在光学系统构建与评估中游刃有余地运用这些核心要素。
references:
  - title: 《Designing Optics Using Zemax OpticStudio》
  - url: https://ebooks.spiedigitallibrary.org/ebooks/PM/designing-optics-using-zemax-opticstudio/eISBN-9781510668577/10.1117/3.100004
   
---


# 《Designing Optics Using Zemax》 Chapter5 Stops and Pupils and Windows（光阑、入瞳出瞳、入射出射窗）

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


## Zemax输入镜头参数

**5mm thick NBK-7 equiconvex singlet lens（5mm厚N-BK7等凸单透镜）**

- 厚度（thick）：$d=5mm$
- 材质：$N-BK7$
- 半径（radius）：$R_{1}=-R_{2}=60mm$
- 物距：$120mm$
- 入瞳直径（entrance aperture）: $20mm$
- 工作波长（wavelength）：$d-line \space\space 0.5876nm$

### 设定入瞳直径 System Explorer>Aperture
[![入瞳直径设定](https://free.picui.cn/free/2025/08/13/689c4665294bf.png)](https://free.picui.cn/free/2025/08/13/689c4665294bf.png)

### 设定视场System Explorer>Fields

> Note: **For finite object distances (like this one), it is important to change the object field specification in the System Explorer (System Explorer > Fields > Settings > Type) from Angle to Object Height as angular fields of view only make sense for objects at infinity.**

注意：对于有限远的物距，需要将视场类型由**Angle**改变为**Object Height**，因为角视场只对于无限远处物体才有意义。

[![修改视场类型，Object Height](https://free.picui.cn/free/2025/08/13/689c46646aff1.png)](https://free.picui.cn/free/2025/08/13/689c46646aff1.png)

### 设定工作波长 System Explorer>Wavelengths
[![波长设定.png](https://free.picui.cn/free/2025/08/13/689c467582244.png)](https://free.picui.cn/free/2025/08/13/689c467582244.png)

### 输入镜头数据 Lens Data

[![chapter5LDE数据.png](https://free.picui.cn/free/2025/08/13/689c4675b4d16.png)](https://free.picui.cn/free/2025/08/13/689c4675b4d16.png)

### 查看切面图 Layout 
[![Layout.png](https://free.picui.cn/free/2025/08/13/689c4b5c03677.png)](https://free.picui.cn/free/2025/08/13/689c4b5c03677.png)

## 分析离轴性能

### 分析方法-三点法

对于离轴性能分析，我们可以在离轴处增加物方点进行分析。但是问题是**选多少个物方点？** **如何选取物方点？**

一般采取**三点法**，将中点设置为全视场高度$h$的$0.707$倍，即$(1/\sqrt{2})h$处，这样一来，以中点距离为半径的圆形区域面积恰好等于全视场总面积的一半。这种取点方式，赋予三个视场点等面积加权性质，能够有效表征整个物方视场的性能。3个视场点分表标记为：**$Full(F3)、Mid(F2)、Axis(F1)$**，即轴心、中场、全视场。
[![三点示意图](https://free.picui.cn/free/2025/08/13/689c5406cbb2d.png)](https://free.picui.cn/free/2025/08/13/689c5406cbb2d.png)

### 在Zemax中设置三点 Field Data Editor

[![Setup-Editors-Field Data Editor](https://free.picui.cn/free/2025/08/13/689c603205008.png)](https://free.picui.cn/free/2025/08/13/689c603205008.png)

FDE操作和LDE（镜头数据编辑器）操作相同，insert插入行，delete删除列，按照三点法以及原始设置的镜头数据，在FDE内依次输入$Y$坐标，大小分别为0，14（取0.7即可），20。FDE右侧即为视场点图像。
[![屏幕截图 2025-08-13 180512.png](https://free.picui.cn/free/2025/08/13/689c635c60cde.png)](https://free.picui.cn/free/2025/08/13/689c635c60cde.png)

设置完成后打开Layout查看截面图：
[![Layout3.png](https://free.picui.cn/free/2025/08/13/689c6aa1d9bc9.png)](https://free.picui.cn/free/2025/08/13/689c6aa1d9bc9.png)

可以明显发现，**离轴点离轴程度越高，成像质量越差，体现在像面弥散斑越大**。

可以使用3D视图查看3D图像，**Setup>System Viewers>3D Viewer**
[![3DLayout.png](https://free.picui.cn/free/2025/08/13/689c6db46a6dc.png)](https://free.picui.cn/free/2025/08/13/689c6db46a6dc.png)
