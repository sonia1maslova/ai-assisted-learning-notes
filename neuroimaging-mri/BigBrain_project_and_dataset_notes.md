---
ai_assisted: true
review_status: unverified
last_reviewed:
---

# BigBrain 项目与数据集：背景、数据结构及其在皮层研究中的应用

## 1. BigBrain 是什么？

BigBrain 是一个开放获取的、超高分辨率的三维人脑组织学数字模型（3D histological model of the human brain）。

原始代表性论文：
Amunts K, Lepage C, Borgeat L, et al.
BigBrain: An ultrahigh-resolution 3D human brain model.
Science. 2013;340(6139):1472–1475.
DOI: 10.1126/science.1235381

BigBrain 的核心不是“大样本人脑数据库”，而是把一颗完整的人类尸检脑经过连续组织学切片、细胞体染色、高分辨率扫描和三维重建，重新构造成一个完整的 3D 人脑组织学模型。

它的重要作用，是在显微组织学与宏观神经影像之间建立桥梁。

---

## 2. 原始脑样本

BigBrain 来自一名 65 岁男性供体的尸检脑。

BigBrain 官方资料指出，该供体临床记录中没有已知的神经系统或精神疾病。

需要特别强调：

BigBrain 本质上只有一个个体。

因此它和 HCP、UK Biobank 这样的多人 MRI 数据库完全不同。

BigBrain 的核心优势是极高空间分辨率和完整的三维组织学信息；它的核心局限则是单个个体不能直接代表人群差异。

---

## 3. BigBrain 是怎样制作出来的？

基本流程：

尸检人脑
→ 固定（fixation）
→ MRI 扫描
→ 石蜡包埋
→ 连续组织学切片
→ 细胞体染色
→ 高分辨率数字扫描
→ 图像修复和配准
→ 三维重建
→ BigBrain 3D histological volume

### 3.1 组织学切片

脑组织被切成约 7,404 张冠状位（coronal）组织学切片。

每张切片厚度约 20 μm。

20 μm = 0.02 mm。

### 3.2 染色

切片采用 Merker cell-body staining 进行细胞体染色。

因此图像中的强度差异与神经元细胞体分布、细胞密度和皮层细胞构筑（cytoarchitecture）密切相关。

### 3.3 数字化

切片经过高分辨率扫描后形成极大的数字组织学数据，完整数据量超过 1 TB。

### 3.4 三维重建

组织切片不可避免会产生撕裂、折叠、局部形变和切片间错位，因此不能简单地把二维切片直接堆叠起来。

研究团队进行了人工修复、自动修复、图像配准、强度校正和三维重建，最终把数千张切片重新组合成一个连续的三维人脑模型。

---

## 4. 最重要的特点：20 μm isotropic resolution

BigBrain 经典完整模型的空间分辨率是：

20 μm × 20 μm × 20 μm isotropic resolution

也就是说，三维空间中三个方向的采样尺度都是 20 μm。

粗略比较：

常规结构 MRI：约 1 mm
高分辨率 MRI：亚毫米级
BigBrain：20 μm = 0.02 mm

在线性尺度上，20 μm 比 1 mm 细约 50 倍。

但要注意：

20 μm resolution 并不等于在整个三维数据中都能稳定识别每一个单独神经元。Wagstyl et al. (2020) 也指出，完整 20 μm BigBrain 数据并不能在所有位置可靠解析单个 neuronal cell bodies。

---

## 5. BigBrain dataset 到底包括什么？

“BigBrain dataset”并不是一个单独的 NIfTI 文件，而是一整套围绕同一个组织学脑建立的数据资源。

主要包括：

### 5.1 Histological sections
二维组织学切片图像。

### 5.2 3D histological volumes
由组织切片重建得到的三维 volume。

官方也提供多个降采样版本，例如：
100 μm
200 μm
300 μm
400 μm

常见格式包括：
MINC
NIfTI

### 5.3 Cortical surfaces
例如：
pial surface
gray/white matter surface
cortical meshes

这些 surface 可以用于 surface-based analysis。

### 5.4 Cytoarchitectonic maps
在 BigBrain 上建立的细胞构筑脑区图谱。

### 5.5 Cortical layer maps
后续研究在 BigBrain 上建立的六层皮层结构：
Layer I
Layer II
Layer III
Layer IV
Layer V
Layer VI

Wagstyl et al. (2020) 的工作就属于这一类衍生数据。

---

## 6. 为什么 BigBrain 很重要？

传统组织学研究有一个基本问题：

真实脑是三维结构，但传统测量常常发生在二维切片中。

由于大脑皮层高度折叠，同一个二维切片里，不同 cortical columns 与切片平面的夹角不同。

这会产生两个重要问题。

### Oblique slicing artifact
如果皮层被斜着切开，测得的 cortical thickness 可能偏大或不准确。

### Stereological sampling bias
某些 cortical areas 因为走向不适合当前切片平面，不能被可靠测量，因此被排除，造成取样偏倚。

BigBrain 把组织学切片重新重建成完整 3D volume，因此研究者可以在三维空间里沿更接近真实 cortical-column direction 的路径进行分析，而不必受原始二维切片方向限制。

---

## 7. BigBrain 和普通 MRI 的区别

MRI：
- 活体测量
- 可以研究大量被试
- 可以研究个体差异和纵向变化
- 空间分辨率相对较低
- cortical layers 很难直接观察

BigBrain：
- 尸检组织学
- 单个个体
- 极高空间分辨率
- 可以研究细胞构筑和 cortical layers
- 不能直接研究该个体的活体功能

二者不是替代关系，而是互补关系。

BigBrain 可以为 MRI 中观察到的宏观结构提供组织学解释和 biological ground truth。

---

## 8. BigBrain 和 HCP 的区别

Human Connectome Project（HCP）：
- 多被试
- 活体
- structural MRI
- diffusion MRI
- resting-state fMRI
- task fMRI
- 关注连接、功能和个体差异

BigBrain：
- 一个尸检脑
- histology
- 20 μm 级别
- 细胞构筑
- cortical layers
- 3D microscopic anatomy

可以简化为：

HCP：
多人 × 活体 × 宏观影像/功能

BigBrain：
单脑 × 尸检 × 超高分辨率组织学

---

## 9. BigBrain 和普通 atlas 的区别

AAL、Schaefer 等 atlas 主要是把 cortex 分成若干离散脑区。

BigBrain 首先是一个连续的高分辨率 3D histological reference brain。

然后研究者可以在这个参考脑上进一步建立：
- cortical area maps
- cytoarchitectonic maps
- cortical layer maps
- subcortical nuclei maps

所以 BigBrain 本身更接近：

high-resolution anatomical reference space / histological brain model

而不仅仅是一个 parcellation。

---

## 10. Wagstyl et al. (2020) 在 BigBrain 上做了什么？

论文：

Wagstyl K, Larocque S, Cucurull G, et al.
BigBrain 3D atlas of cortical layers: Cortical and laminar thickness gradients diverge in sensory and motor cortices.
PLOS Biology. 2020;18(4):e3000678.
DOI: 10.1371/journal.pbio.3000678

这篇文章不是 BigBrain 原始项目本身。

它利用 BigBrain 原始 3D histological volume，进一步建立了一个全脑 cortical layer atlas。

---

## 11. Wagstyl 2020 的分析流程

### Step 1：人工标注训练数据

研究者在部分高分辨率组织学切片上人工标注：
Layer I
Layer II
Layer III
Layer IV
Layer V
Layer VI

共使用 51 个 cortical regions，来自 13 个 BigBrain histological sections。

这些标注由神经解剖专家检查。

### Step 2：提取 cortical intensity profiles

研究者在 BigBrain 的 3D volume 中，沿接近 cortical-column direction 的路径提取 histological intensity profile。

大致方向是：

pia
↓
Layer I
↓
Layer II
↓
Layer III
↓
Layer IV
↓
Layer V
↓
Layer VI
↓
white matter

### Step 3：训练 1D convolutional neural network

输入：
histological intensity profile

输出：
每个深度位置属于哪个类别：
background
Layer I
Layer II
Layer III
Layer IV
Layer V
Layer VI
white matter

### Step 4：建立三维 cortical layer surfaces

通过每个 cortical vertex 的 layer boundaries，重建：
I/II boundary
II/III boundary
III/IV boundary
IV/V boundary
V/VI boundary
VI/white-matter boundary

最终形成三维 mesh surfaces。

### Step 5：计算 thickness

Total cortical thickness：
pial surface → gray/white boundary

Laminar thickness：
相邻 cortical layer boundaries 之间的距离。

---

## 12. 为什么重新定义 white matter surface？

原始 BigBrain surface 和许多 MRI cortical reconstruction 方法一样，使用 gray matter 与 white matter 之间的 maximum intensity gradient 来定义 white surface。

Wagstyl 等发现：

maximum intensity gradient 并不总是真正的组织学 gray/white boundary。

原始 maximum-gradient surface 在很多位置更接近：

Layer VIa / VIb boundary

而不是真正的：

Layer VI / white matter boundary

原因是 VIa 与 VIb 之间的 neuronal-density change 有时比真正 gray matter → white matter 的变化更陡。

因此：

maximum image gradient ≠ true anatomical boundary

新的神经网络由于以人工标注和 cortical neuron 的存在为依据，更接近真正的组织学 gray/white boundary。

这也说明：

图像上最明显的 intensity edge 不一定就是 biological boundary。

---

## 13. BigBrain 如何用于研究 cortical hierarchy？

Wagstyl et al. (2020) 研究了：

visual hierarchy
auditory hierarchy
somatosensory hierarchy
motor-frontal hierarchy

首先确定：
primary visual cortex
primary auditory cortex
primary somatosensory cortex
primary motor cortex

然后计算每个 cortical vertex 到对应 primary area 的 geodesic surface distance。

Geodesic distance 指：

沿弯曲 cortical surface 的最短路径距离。

这个距离被当作 hierarchical progression 的一个空间 proxy。

---

## 14. 两个完全不同的空间方向

这篇文章里有两个容易混淆的方向。

### 沿 cortical surface 的方向

用于：
geodesic distance

例如：
V1 → V2/V3 → higher-order visual cortex → association cortex

这个方向反映 cortical hierarchy 的空间推进。

### 穿过 cortical depth 的方向

用于：
cortical thickness / laminar thickness

例如：
pia
↓
I
↓
II
↓
III
↓
IV
↓
V
↓
VI
↓
white matter

所以论文真正研究的是：

当沿 cortical surface 从 primary area 向 higher-order cortex 前进时，垂直于 cortical surface 的总皮层厚度和各 cortical layer thickness 如何变化？

---

## 15. Wagstyl 2020 的主要结果

在：
visual cortex
somatosensory cortex
auditory cortex

中，随着距离 primary sensory area 的 geodesic distance 增大：

cortical thickness 总体增加。

这种 thickness gradient 主要由：
Layer III
Layer V
Layer VI
驱动。

---

## 16. Motor-frontal cortex 是重要例外

motor-frontal cortex 出现相反趋势：

从 primary motor cortex 向 higher-order frontal cortex：

cortical thickness 下降。

同样主要由 Layer III、V、VI 驱动。

因此，cortical hierarchy 并不意味着所有系统、所有结构指标都沿完全相同的方向变化。

---

## 17. BigBrain 的主要优势

1. 极高空间分辨率  
可以研究普通 MRI 难以直接观察的 mesoscale / laminar structure。

2. 全脑三维  
不像传统二维 histology 只能依赖有限切片。

3. 可以沿真实 cortical geometry 测量  
减少 oblique slicing artifact 和 stereological sampling bias。

4. 可以连接多个尺度  

single-neuron morphology
→ cortical layers
→ cortical thickness
→ MRI anatomy
→ functional organization

---

## 18. BigBrain 的主要局限

### 18.1 只有一个个体
无法直接估计 population variability、sex differences、age effects 和 interindividual variability。

### 18.2 Postmortem tissue distortion
固定、包埋和切片会造成 shrinkage、tearing、deformation 和 local displacement。

### 18.3 Shrinkage
组织处理会导致组织收缩，而且 x、y、z 方向的收缩程度不完全一致，因此 thickness 需要进行尺度校正。

### 18.4 20 μm 仍不等于完整单细胞分辨率
可以观察精细细胞构筑，但不能在整个 3D volume 中稳定识别每一个单独神经元。

### 18.5 无法直接研究活体功能
BigBrain 本身没有 resting-state fMRI、task fMRI、electrophysiology 或 behavior。

功能解释通常需要与其他数据集进行跨模态比较。

---

## 19. 如何理解 BigBrain 在神经科学中的位置？

BigBrain 最独特的价值，是位于微观组织学和宏观神经影像之间：

单细胞 / 神经元形态
↓
细胞构筑
↓
cortical layers
↓
BigBrain
↓
mesoscale anatomy
↓
MRI cortical structure
↓
functional networks
↓
cognition / behavior

它提供了一座连接 microscopic histology 和 macroscale neuroimaging 的桥梁。

---

## 20. 一句话定义

英文：

BigBrain is an openly accessible ultrahigh-resolution three-dimensional histological model of the human brain, reconstructed from thousands of cell-body-stained postmortem sections at 20-μm isotropic resolution.

中文：

BigBrain 是一个开放获取的超高分辨率三维人脑组织学模型，由数千张尸检脑细胞体染色切片重建而成，其经典完整模型具有 20 μm 各向同性空间分辨率。

---

## 21. 需要特别区分的几个概念

BigBrain：
原始三维组织学人脑模型。

BigBrain dataset：
围绕 BigBrain 发布的一整套 histological sections、volumes、surfaces、registrations 和 maps。

BigBrain atlas：
泛指基于 BigBrain 建立的各种高分辨率 anatomical / cytoarchitectonic maps。

BigBrain cortical layer atlas：
Wagstyl 等基于 BigBrain 建立的 cortical-layer segmentation，是后续衍生产品，不是 2013 年 BigBrain 原始数据本身。

---

## 22. 核心参考文献

Amunts K, Lepage C, Borgeat L, et al.
BigBrain: An ultrahigh-resolution 3D human brain model.
Science. 2013;340(6139):1472–1475.
DOI: 10.1126/science.1235381

Wagstyl K, Larocque S, Cucurull G, et al.
BigBrain 3D atlas of cortical layers: Cortical and laminar thickness gradients diverge in sensory and motor cortices.
PLOS Biology. 2020;18(4):e3000678.
DOI: 10.1371/journal.pbio.3000678

---

## 23. 官方资源

BigBrain Project:
https://bigbrainproject.org/

BigBrain Maps & Models:
https://bigbrainproject.org/maps-and-models.html

BigBrain Data FAQ:
https://ftp.bigbrainproject.org/bigbrain-ftp/FAQ.html

BigBrain 数据也可以通过 EBRAINS / siibra 等平台浏览和访问。

---

## 24. 整个逻辑的极简总结

真实尸检人脑
→ 7,404 张组织学切片
→ 细胞体染色
→ 高分辨率数字扫描
→ 3D reconstruction
→ 20 μm BigBrain
→ cortical surfaces / cytoarchitecture
→ cortical layer segmentation
→ thickness / microstructural analysis
→ 与 MRI 和 cortical hierarchy 建立联系
