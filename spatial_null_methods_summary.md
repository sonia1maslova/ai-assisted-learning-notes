---
ai_assisted: true
review_status: unverified
last_reviewed:
---

# 空间替代脑图谱（Spatial Null Brain Maps）生成方法总结

## 1. 为什么需要空间替代脑图谱

脑图之间的相关性可能来自共同的空间结构，而不是实际生物学联系。由于皮层具有明显的空间自相关（spatial
autocorrelation），需要构造保持空间组织特征的零分布。

目标：

给定两个脑图：

-   神经多效性图谱 X
-   目标神经生物学图谱 Y

计算：

r_obs = cor(X, Y)

然后生成大量空间保持的替代图：

X_null

比较：

cor(X_null, Y)

判断真实相关是否超过空间结构预期。

------------------------------------------------------------------------

# 2. Moran spectral randomization

## 核心思想

Moran
方法基于空间统计学，不旋转脑图，而是利用空间邻接矩阵描述脑区之间的空间关系。

首先建立：

W = spatial weight matrix

其中邻近脑区具有更高权重。

随后进行空间谱分解：

X = Eβ

其中 E 为 Moran eigenvectors。

随机改变空间成分 β，生成：

X_null = Eβ_null

## 保留特征

保持：

-   Moran's I
-   空间自相关强度
-   邻接关系

不保持：

-   精确皮层几何位置
-   球面拓扑

## 适用场景

适合：

-   MNI volume
-   ROI空间矩阵
-   subcortical结构

------------------------------------------------------------------------

# 3. Alexander-Bloch spin test

## 核心思想

Spin test 专门用于皮层表面数据。

流程：

1.  将皮层表面球化（sphere mapping）。
2.  对球面进行随机三维旋转。
3.  将旋转后的坐标重新匹配到原始皮层位置。

旋转：

x' = R x

其中 R 为随机旋转矩阵。

## 保留特征

保持：

-   左右半球身份
-   cortical topology
-   空间连续性
-   大尺度梯度

不保持：

-   原始ROI精确位置
-   象限位置

例如额叶区域可以旋转到原来视觉区域附近。

------------------------------------------------------------------------

# 4. VASA parcel-spin

## 核心思想

VASA 是针对 parcel-level cortical map 的空间旋转方法。

区别：

Alexander-Bloch：

vertex-level rotation

VASA：

parcel-level rotation

## 流程

输入：

-   sphere surface
-   cortical parcellation

例如：

Glasser360：

ROI1 ... ROI360

步骤：

1.  获取每个parcel在球面上的位置。
2.  随机旋转球面。
3.  将旋转后的位置匹配到最近parcel。

生成：

Spin index matrix

例如：

360 × 10000

每一列代表一次空间旋转。

生成替代脑图：

X_null = X\[spin_indices\]

## 保留特征

保持：

-   hemisphere identity
-   parcel topology
-   cortical geometry

适合：

-   Glasser360
-   Schaefer400
-   fsLR surface atlas

------------------------------------------------------------------------

# 5. BrainSMASH

## 核心思想

BrainSMASH通过模拟空间距离结构生成替代脑图。

首先计算：

-   ROI之间空间距离 D
-   原始地图的空间变异结构

例如 variogram：

γ(d)

然后生成新的地图，使：

γ_null(d)

接近：

γ_original(d)

## 保留特征

保持：

-   distance-dependent similarity
-   spatial autocorrelation

不要求：

-   球面表面
-   特定atlas

------------------------------------------------------------------------

# 6. 四种方法比较

  方法                   空间基础         保留特征            常用场景
  ---------------------- ---------------- ------------------- ------------------
  Moran                  空间邻接矩阵     Moran's I           MNI/volume/ROI
  Alexander-Bloch spin   球面旋转         cortical topology   surface cortex
  VASA spin              parcel球面旋转   parcel空间结构      Glasser/Schaefer
  BrainSMASH             距离模型         variogram           通用空间地图

------------------------------------------------------------------------

# 7. 在皮层ROI研究中的选择

对于：

-   Glasser360
-   Schaefer400
-   cortical biological maps

通常：

首选：

VASA spin 或 Alexander-Bloch spin

原因：

它们直接利用皮层球面几何结构。

对于：

-   MNI volume
-   subcortex
-   cerebellum

通常：

Moran 或 BrainSMASH 更合适。

------------------------------------------------------------------------

# 8. 神经多效性分析中的应用

当前分析：

Neural pleiotropy map

↓

空间旋转生成10000个替代脑图

↓

分别与目标神经生物学图谱计算相关

↓

形成空间零分布

↓

计算spin-corrected p值

核心问题：

真实相关：

cor(X_NP,Y)

是否超过：

cor(X_null,Y)

产生的空间期望范围。
