---
title: Aberrations Chapter1-Basic concepts in geometrical optics
tags: [Aberrations]
categories: [光学设计基础]
date: 2025-8-6
description: 本笔记参考《Introduction to aberrations in optical imaging systems》
articleGPT: 这是Introduction to aberrations in optical imaging systems的Basic concepts in geometrical optics一节笔记，主要介绍几何光学中的一些基础概念，例如光线、光路、波前、物像空间、光阑等等，是研究像差的理论基础
references:
  - title: Introduction to aberrations in optical imaging systems     $\text{Jos\'{e}\ Sasi\'{a}n}$
  - url: https://www.cambridge.org/core/books/introduction-to-aberrations-in-optical-imaging-systems/4541B166F94266355F024514C7185216
   
---
# Aberrations Chapter1-Basic concepts in geometrical optics

> **参考书目：**  
>**Introduction to aberrations in optical imaging systems**                &ensp;      $\text{Jos\'{e}\ Sasi\'{a}n}$
>
> **概述：**
>
> - Chapter 1 provides an introduction and a historical overview.(omit)
> - Chapter 2 provides **basic concepts** in geometrical optics.——介绍了几何光学的基本概念
> - Chapter 3 provides a basic and insightful discussion on **imaging with rays**.——对**射线成像**进行讨论
> - Chapter 4 provides a fresh and useful discussion on the fundamentals of **imaging with light waves**.——对**光波成像**的基本原理进行讨论。
> - Chapter 5 introduces and highlights the **wave aberration function**, which is central to the understanding of aberrations.——介绍并强调了**波像差函数**，这是理解像差的核心
> - Chapter 6 discusses **secondorder effects** which determine the location and size of an image.——讨论了决定图像位置和大小的**二阶效应**
> - Chapter 7 discusses the **primary aberrations**.——讨论主要像差
> - Chapter 8 discusses aberrations using the concept of light rays.——使用光线的概念讨论像差。

## 研究方法-建立光传播经过光学系统形成图像的模型

In order to develop a theory of aberrations it is necessary to **build a conceptual structure, a model, about how light propagates in an optical system and forms images.** For this we have the object and image spaces. In **<font color='red'>object space</font>** there is a **<font color='red'>coordinate system</font>**
 with the z-axis coinciding with the **<font color='red'>optical axis</font>**, the **<font color='red'>object plane</font>**, the **<font color='red'>entrance pupil</font>**, and the **<font color='red'>field vector</font>**. In **<font color='red'>image space</font>** there is also a coordinate system, the **<font color='red'>image plane</font>**, the **<font color='red'> exit pupil</font>**, and the **<font color='red'>aperture vector</font>**. We now assume that the optical system has **<font color='red'>axial symmetry</font>**; this simplifies the mathematical description and permits finding specific system attributes that are symmetry dependent. Two **<font color='red'>first-order rays</font>**, the **<font color='red'>chief and marginal rays</font>**, are traced. And, notably, from the tracing of these two rays a significant amount of information about an optical system can be extracted with minimum computational effort.

### 英文术语

- optical axis 光轴
- coordinate system 坐标系
- object space 物方空间
- object plane 物平面
- entrace pupil 入瞳
- field vector 场矢量
- image space 像方空间
- image plane 像平面
- exit pupil 出瞳
- aperture vector 孔径矢量
- axial symmetry 轴对称性
- first-order rays 一阶射线
- chief rays 主光线
- marginal rays 边缘光线
  
## Rays and wavefronts 光线与波前
光通过光学系统的传播是用光线和光波来模拟的。
### Rays 光线
光线就是光传播的路径，表示为一条线。在折射率恒定的光学均匀介质中，光线是直线。
光学系统是通过**追迹光线**来分析的，**实际系统的光学性能**是通过基于追迹光线的计算来预测的。
### wavefronts 波前
>The geometrical wavefront is defined as the surface of **equal optical path length (OPL)**. The optical path length is defined by
>$$OPL=\int_{a}^{b}n(s)ds$$
几何波前就是等光程面。光程即optical path length，可以被认为是光子从某点传递到某点的渡跃时间。因此波前在微观角度上也可以表示为具有相同渡跃时间的粒子组成的表面。如果光线是从均匀介质中的某点出发，那么根据波前的定义，几何波前就是以该点为中心的几何球体。
> As a wavefront propagates through a system its **shape changes** and **departs from a spherical form**. The change of wavefront shape from a spherical shape is considered a **wavefront deformation.** This wavefront deformation can explain image defects known as aberrations and it represents phase variations of a light wave that are used in physical calculations. The concepts of rays, optical path, and geometrical wavefront are key concepts in aberration theory.

当波前通过系统传播时，其形状会发生变化，并偏离球形。波前形状从球面波前形状的变化被认为是一种波前变形。**这种波前变形可以解释被称为像差的图像缺陷**，它代表了用于物理计算的光波的相位变化。光线、光路和几何波前是像差理论中的重要概念。

## Symmetry in optical imaging systems 光学成像系统中的对称性
### 光学系统是什么？
>An optical system reflects, refracts, or diffracts light emerging from an object to form an image.

光学系统就是将物体发出的光进行反射、折射、衍射，并进一步形成图像的一种系统

### 光学系统的组成
> The system may be built from lenses, mirrors, prisms, or diffractive optical elements. Structurally the optical system may have **some degree of symmetry** or have no symmetry at all.

光学系统一般可以由透镜、反射镜、棱镜、衍射光学元件构成，从结构上看，光学系统具有一定的对称性，但是也有可能没有对称性。

> A **glass sphere** has concentric symmetry about its center, and in particular an infinite number of axes of axial symmetry. A **glass cylinder** has axial symmetry about the axis of the cylinder, and in particular an infinite number of planes of symmetry.一个用来散射光的棱镜一样，只有一个对称面。 

对于对称性系统，玻璃球面具有同心对称性，有无穷多个对称轴；玻璃柱面具有关于圆柱体轴线的轴对称性，具有无穷多个对称面。对称面就是包含轴线并将系统分为两个对称半平面的面。双平面对称系统，例如眼镜，有两个对称面。单平面对称系统，例如用于色散的棱镜，只有一个对称面。

>Symmetry in optical systems is essential to describe and understand them. For every degree of symmetry there is a property of the system. We are concerned with describing **axially symmetric systems**; these systems have an **axis of rotational symmetry** in such a way that one cannot distinguish if the system has been rotated about its axis. In particular axially symmetric systems are easier to fabricate than systems with a lesser degree of symmetry. The axis of rotational symmetry, or axial symmetry, is defined as the optical axis.

主要研究的还是轴对称系统，系统有一根旋转轴，可以使得系统绕轴旋转，该轴即光轴。另外，对称系统相对于非对称系统来说，更容易制造

## The object and the image spaces 物空间和像空间

### 定义

> The space where the object resides is defined as the object space and is infinite in extent. Similarly, the space where the image resides is defined as the image space and is infinite in extent

物体所在空间为物空间，在范围上是无限的；同理，图像所在空间为像空间，范围依旧无限。每个空间都设定有笛卡尔坐标系和圆柱坐标系，其中笛卡尔坐标系主要用于研究物像关系，而圆柱坐标系主要用于研究像差。坐标系中的$z$轴与系统光轴重合。

> The field of view of an optical system is the intended region in object space that the system images. It can be specified in angular dimensions if the object is located at infinity or in linear dimensions if the object is at a finite distance.

光学系统的视场就是指系统在物方空间能够成像的预定区域，当物体位于无穷远处，可以利用角维度进行描述，即视场角范围；当物体位于有限远处，就可以用线性维度进行表示，例如物距长度等。

### 英文术语

- the field of view(Fov) 视场
