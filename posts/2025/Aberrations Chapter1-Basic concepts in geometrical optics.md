---
title: Aberrations Chapter1-Basic concepts in geometrical optics
tags: [Aberrations]
categories: [光设理论基础]
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

## The aperture stop, the pupils, and the field stop 孔径光阑、出入瞳、视场光阑

###  aperture stop 孔径光阑
>This aperture limits the amount of light through an optical system and creates a well-defined beam that reaches the image plane for every field point. The aperture stop is assumed to be circular, contained in a plane perpendicular to the optical axis and centered in the optical axis.

孔径光阑主要用于限制通过光学系统的进光量，并为每个场点创建限制完备的抵达像平面的光束，通常位于垂直于光轴的平面内，并以光轴为中心。
![A singlet lens system focusing rays arriving from two field points. The aperture stop limits the amount of light and defines the beams of light, and the field stop limits the field of view at an image location.](https://picui.cn/thumbnails/72faf0d87df30b595a262a5a01b5cd02.png)

### field stop 视场光阑
> The field stop is a limiting aperture located at an image plane that defines the extent of the field of view of the optical system. It contributes to well define how light propagates in an optical system by blocking unwanted light. Without the stop and field apertures an optical system is not well defined.

视场光阑是位于像平面上的一个限制孔径，定义了光学系统的视场范围，有助于定义光是如何通过光学系统进行传播，并阻止不需要的光。该光阑的作用是将光场限制在一个校正良好的或非渐晕的区域内。

### entrance pupil and exit pupil 入瞳与出瞳
> The image of the aperture stop in object space is defined as the entrance pupil, and the image of the stop in image space is defined as the exit pupil. 

将孔径光阑在物方空间的像定义为入瞳，将孔径光阑在像方空间的像定义为出瞳。

> The aperture stop, the entrance pupil, and the exit pupil are optically conjugated, meaning that they are images of each other. The location of the aperture stop may depend on the application of the optical system. Sometimes the system is required to be telecentric in image or object space, and to achieve this condition the stop aperture must be located at the front or rear focal point of the system. In some systems the position of the stop is a degree of freedom that impacts aberrations.

光阑、入瞳和出瞳是光学共轭的，意味着它们是彼此的像。光阑的位置可能取决于光学系统的应用。有时要求系统在像空间或物空间中远心，而要达到这一条件，光阑必须位于系统的前或后焦点处。在某些系统中，光阑的位置是影响像差的一个自由度。

## Significant planes and rays 重要平面与光线

### meridional plane 子午面
> In analogy with the earth meridians, any plane in an optical system that contains the optical axis is called a meridional plane.

类比地球子午线，光学系统中包含光轴的任意平面称为子午面

![The chief ray passes through the center of the aperture stop and through the edge of the image. The marginal ray passes through the edge of the stop and through the center of the image.](https://picui.cn/thumbnails/3de80a75d38a8df7acea1ba34c6fd27d.png)

上图为一个单透镜系统的子午面截图

### marginal ray
>The marginal ray starts at the axial object position, goes through the edge of the entrance pupil, and defines image locations and pupil sizes. It propagates to the edge of the stop and the edge of the exit pupil. The marginal ray height and ray angle are denoted by $y$ and $u$.

边缘光线从轴上物点位置开始，穿过入瞳边缘，并定义图像位置和入瞳大小。它传播到停止的边缘和出口光瞳的边缘。边缘射线高度和射线角度分别用$y$和$u$表示。

![边缘光线主光线示意图](https://picui.cn/thumbnails/e5d67ab8e1ed92d288625f552574ef29.png)

> The chief ray starts at the edge of the object, goes through the center of the entrance pupil, and defines image heights and pupil locations. It goes through the center of the stop and the center of the exit pupil. The chief ray height and ray angle are denoted by and $\overline{y}$ and $\overline{u}$

主光线起始于物体边缘，经过入瞳中心，定义了图像高度和入瞳位置。它经过孔径光阑中心和出瞳中心。主光线高度和光线角度分别用$\overline{y}$和$\overline{u}$表示。
![边缘光线主光线示意图](https://picui.cn/thumbnails/e5d67ab8e1ed92d288625f552574ef29.png)

## field and aperture 场和孔径矢量

> A propagating ray is uniquely defined by the field vector $\overrightarrow{H}$ and by the aperture vector $\overrightarrow{\rho}$. The field vector lies in the object plane and the aperture vector lies in the exit pupil plane as shown in Figure 2.7. These planes are perpendicular to the optical axis of the system. The field vector specifies the field point $\overline{y_{o}}\overrightarrow{H}$ from  which a ray originates. The point $y_{E}'\overrightarrow{\rho}$ defines the intersection of the ray with the exit pupil plane as shown also in Figure 2.7. Both vectors are normalized by the maximum aperture and maximum field respectively so that their magnitude ranges between zero and unity.

**一条光线可以由场矢量和孔径矢量唯一确定表示。**

![The aperture vector (scaled by the marginal ray height at the exit pupil) and the field vector (scaled by the chief ray height at the object plane).](https://picui.cn/thumbnails/383940a397cf5e0ed79aff2b52db13a6.png)

### field vector 场矢量

位于物面，物面垂直于系统光轴，场矢量指明了光线是从哪个场点发出的，并由最大场高$\overline{y_{o}}$进行归一化，使得其大小介于0与单位长度之间，场矢量用$\overrightarrow{H}$表示，其大小为$H$。

最大场高$\overline{y_{o}}$是指主光线在物面的投射高度。
![边缘光线主光线示意图](https://picui.cn/thumbnails/e5d67ab8e1ed92d288625f552574ef29.png)

### aperture vector 孔径矢量

位于系统出瞳面，出瞳面同样垂直于系统光轴，孔径矢量指明了光线到达出瞳面哪一点，并由最大孔径进行归一化，使得其大小介于0与单位长度之间，孔径矢量用$\overrightarrow{\rho}$表示，其大小为$\rho$。

最大孔径高度$y_{E}'$是边缘光线在出瞳面的投射高度。
![边缘光线主光线示意图](https://picui.cn/thumbnails/e5d67ab8e1ed92d288625f552574ef29.png)

>Using the field and aperture vectors we can define fans of rays in a meridional plane by setting the field vector H and the aperture vector ρ parallel to each other (φ = 0). We can define sagittal rays by setting the vectors perpendicularly to each other (φ = 90◦).

利用场矢量和孔径矢量，我们可以通过设置场矢量$\overrightarrow{H}$和孔径矢量$\overrightarrow{\rho}$相互平行( $\phi=0°$ )来定义子午面内的光束。我们可以通过设置相互垂直的向量( $\phi = 90 °$)来定弧矢面光束。

![The angle φ between the field and aperture vectors looking down the optical axis.](https://picui.cn/thumbnails/f75dc74f0c0c8ab86c7b299dc1270a55.png)

## Real, first-order, and paraxial rays

### First-order optics 一阶光学
> First-order optics is the study of perfect optical systems, or optical systems without aberrations. Analysis methods include **Gaussian optics** and **paraxial optics**. Results of these analyses include the imaging properties (image location and magnification) and the radiometric properties of the system.

一阶光学的研究对象是理想光学系统，即没有像差的光学系统。对一阶光学的分析方法有两种，一种为Gussian optics 高斯光学，另一种为paraxial optics 傍轴光学。对一阶光学的分析结果通常包含系统的成像特性，例如图像位置、图像放大倍数等。

### ray tracing 光线追迹
> Rays of light are traced through an optical system in an iterative manner. The initial data are the spatial coordinates of a point and the direction of the ray. The ray is traced by finding its intersection coordinates with the next surface. Then the direction of the ray after refraction is determined by applying Snell’s law. For spherical surfaces or conic surfaces the ray intersection is determined using closed-form equations. For other surfaces an iterative algorithm is used until the intersection point is found to a high degree of accuracy. This ray-tracing process is repeated until the image plane is reached.

光线以迭代的方式通过光学系统进行跟踪。初始数据是一个点的空间坐标和光线的传播方向。通过寻找光线与下一个曲面的交点坐标来追踪光线。然后应用斯涅耳定律确定光线折射后的方向。对于球面或圆锥曲线曲面，曲面方程已知，光线与曲面的交点用封闭形式的方程（将光线参数带入面型方程直接求得精确解）来确定。对于其他曲面，无法给出精确方程，只能使用迭代算法，直到找到交点具有高度的精度（计算误差然后减小误差，一直迭代，一般使用数值逼近方法）。这个光线跟踪过程重复进行，直到到达像平面。

### real rays 实际光线
对于实际光线的追踪则需要应用原本的斯涅尔定律，实现精确的追踪，光线可能不靠近光轴，斯涅尔定律（折反射定律）如下：
$$n\sin I =n' \sin I'$$

### first-order rays 一阶光线

一阶光线指的是对光线的一阶近似，故而使用的斯涅尔方程也是一阶线性近似：
$$n i = n' i'$$

### paraxial rays 傍轴光线
> By paraxial rays we mean rays extremely close to the optical axis that are also traced with the first-order ray equations. However, each paraxial ray height and slope is assumed to be multiplied by a small factor such as $10^{-25}$ to insure that the ray is very close to the optical axis. In actual calculations there is cancelation of these factors and the factors are not explicitly written down.

其实就是离光轴非常近的光线，也可以用一阶光线所对应的公式进行计算。
