---
ai_assisted: true
review_status: ai_reviewed
last_reviewed: 2026-10-12
---

# 脑影像空间中的生物学指标图谱

本文按生物学指标整理主要人脑图谱：**有哪些指标、有哪些代表资源、反映什么，以及能否用于 MRI 空间分析**。这是代表性资源清单，按六类组织。

表中的“现成图”表示资源已提供参考空间中的图；“需映射/构建”表示还要处理组织样本、脑区数据或个体影像。两者都需要与自己的 MRI 数据对齐。

## 1. 基因表达图谱

**关注：哪些基因在不同脑区表达较多。**

| 指标 | 代表资源 | 反映什么 | MRI 空间中的形式 |
| --- | --- | --- | --- |
| 单个基因的 mRNA 表达 | [Allen Human Brain Atlas（AHBA）][ahba] + [abagen][abagen] | 采样脑组织的相对基因表达 | **需映射**：把离散组织样本汇总到 MRI 脑区，形成“脑区 × 基因”矩阵 |
| 基因表达的主要空间梯度 | [neuromaps 的 AHBA gene PC1 图][gene-pc1] | 多基因表达的第一主成分，概括主要空间变化 | **现成图**：fsaverage 表面；它是综合梯度，不是某个基因的表达图 |

AHBA 成人微阵列数据来自 6 位尸检供体，采样不均匀；表达量反映 mRNA，不直接等于蛋白水平。[数据说明][ahba]

补充资源：[BrainSpan][brainspan]适合研究发育阶段的脑区表达；[GTEx][gtex]提供组织表达与遗传调控信息。二者不能默认当作成人全脑连续 MRI 表达图。

## 2. 细胞类型图谱

**关注：不同脑区有哪些细胞类型，以及它们的相关表达特征。**

| 指标 | 代表资源 | 反映什么 | MRI 空间中的形式 |
| --- | --- | --- | --- |
| 转录定义的细胞类型 | [Allen Brain Cell Atlas：人类 WHB-10Xv3][abc] | 神经元、星形胶质细胞、少突胶质细胞、小胶质细胞等类型及采样脑区差异 | **需映射**：人类数据是单核转录组，不能直接当作逐体素细胞密度图 |
| 细胞类型相关表达 | AHBA + 细胞类型标记基因集合 | 某类细胞的标记基因在各脑区的表达特征 | **需构建**：按所用标记集合计算脑区指标；属于间接估计 |

ABC Atlas 包含不同物种和项目，应选择人脑数据。单核捕获比例、标记基因富集与单位体积的细胞数量是不同指标。[Siletti et al., 2023][cell-paper]

## 3. 神经递质受体与转运体图谱

**关注：某种受体或转运体的结合指标在脑内如何分布。**

常用入口是 [Hansen receptor atlas][hansen]、[neuromaps][map-list]和 [JuSpace][juspace]。Hansen 集合提供群体平均 PET 体积图及脑区数据；具体空间和适用脑区按所选图确认。[原研究][hansen-paper]

| 系统 | 指标示例 | 代表图谱或集合 |
| --- | --- | --- |
| 多巴胺 | D1、D2/3、DAT | Hansen 集合；JuSpace 的 DAT 模板中有 SPECT 来源 |
| 血清素 | 5-HT1A、5-HT1B、5-HT2A、SERT | [Beliveau 血清素图谱][serotonin]；Hansen 集合 |
| GABA | GABA-A 相关苯二氮䓬结合位点 | [Nørgaard flumazenil 图谱][gaba] |
| 谷氨酸 | mGluR5 | Hansen 集合中的 ABP688 等示踪剂图 |
| 乙酰胆碱 | α4β2、M1、VAChT | Hansen 集合 |
| 去甲肾上腺素 | NET | Hansen 集合 |
| 组胺 | H3 | Hansen 集合 |
| 大麻素 | CB1 | Hansen 集合 |
| 阿片 | μ 阿片受体（MOR） | Hansen 集合 |

**空间：**有 MNI152 体积图和部分表面图。对 neuromaps 收录的 Beliveau 与 Nørgaard 图，皮层分析应优先用提供的 fsaverage 版本，其 MNI152 版本仅用于皮层下数据。[逐图说明][map-list]

**含义：**通常是结合潜能等指标，部分图经标定提供位点密度估计。它们描述靶点分布，不直接测量神经递质释放或系统活动；GABA 位点图也不是兴奋/抑制比值。[PET 指标共识][pet-metrics]

## 4. 代谢与灌注图谱

**关注：不同脑区的葡萄糖利用、氧消耗和血流分布。**

| 指标 | 代表图谱/获取入口 | 反映什么 | MRI 空间中的形式 |
| --- | --- | --- | --- |
| 葡萄糖代谢（CMRglc） | neuromaps 的 **Raichle 系列 cmrglc 图** | 区域葡萄糖代谢分布 | **现成图**：fsLR 164k 表面 |
| 脑氧代谢（CMRO₂） | 同系列 **cmr02 图** | 区域氧消耗分布 | **现成图**：fsLR 164k 表面 |
| 脑血流（CBF） | 同系列 **cbf 图** | 区域血流/灌注分布 | **现成图**：fsLR 164k 表面 |
| 脑血容量（CBV） | 同系列 **cbv 图** | 区域血液容量分布 | **现成图**：fsLR 164k 表面 |

上述参考图来自健康青年 PET 研究；获取信息见 [neuromaps 目录][map-list]，测量依据见 [Vaishnavi et al., 2010][metabolism]。

其他 FDG-PET 或 ASL 数据也可构建代谢/灌注参考图，但 **FDG-PET、ASL 是测量方法，本身不是某一张图谱的名称**。静态 FDG 摄取比与绝对葡萄糖代谢率不同；CBF、CMRO₂ 与 BOLD 也不能互换。[FDG 测量说明][fdg]

## 5. 组织微结构与组织学图谱

**关注：髓鞘相关特征、突触标记和细胞构筑。**

| 指标 | 代表图谱/资源 | 反映什么 | MRI 空间中的形式 |
| --- | --- | --- | --- |
| 髓鞘相关对比（T1w/T2w） | HCP S1200 群体平均 myelin map | 与髓鞘相关的 MRI 强度对比 | **现成图**：如 fsLR 32k；不是髓鞘绝对含量 |
| 突触囊泡蛋白 SV2A | neuromaps 的 **finnema2016 / ucbj 图** | UCB-J PET 的 SV2A 结合，作为突触相关标记 | **现成图**：MNI152；不是组织学突触计数 |
| 细胞构筑脑区 | [Julich-Brain][julich] | 根据组织学特征划分的脑区及其个体间位置差异 | **现成图**：概率图/最大概率分区；不是连续神经元密度图 |
| 组织学结构与皮层层次 | [BigBrain][bigbrain] | 高分辨率细胞体染色重建及层相关数据 | 有原生空间及部分 MNI 配准产品；基于单个供体 |

HCP 与 SV2A 产品说明见 [neuromaps 目录][map-list]；T1w/T2w 的含义见[原始方法][myelin]。BigBrain 的空间版本见[官方数据说明][bigbrain-space]。

**可进一步构建的指标：**磁化转移（MT）可提供髓鞘相关信息；QSM 提供组织磁化率、对铁敏感。本表暂未指定二者的通用参考图，需选择具体研究产品或自行构建；QSM 不直接等于铁含量。[MT 验证][mt]、[QSM 共识][qsm]

## 6. 病理蛋白图谱

**关注：特定人群中的病理蛋白沉积分布。**

| 指标 | 代表数据来源 | 反映什么 | MRI 空间中的形式 |
| --- | --- | --- | --- |
| Aβ | Amyloid PET；如 [ADNI][adni]队列 | 示踪剂可结合的聚集性 Aβ 沉积 | 可配准到 MRI；队列扫描需选择人群并构建参考图 |
| Tau | Tau PET；如 ADNI 队列 | 特定示踪剂可结合的聚集 tau | 同上；需按示踪剂与疾病解释 |

Aβ 和 tau 的测量含义分别见 [AMYVID][amyloid]与 [TAUVID][tau]官方说明。这类图具有年龄、疾病及示踪剂依赖性，不是通用健康脑基线。

**研发中的补充：**α-synuclein 与 TDP-43 已有早期研究/人体评估进展，本笔记不将其列为成熟通用参考图谱。[α-synuclein 原研究][alpha-syn]、[TDP-43 临床前研究][tdp]与[早期人体进展][tdp-human]

## 获取入口与空间对应

- **找现成脑图：**[neuromaps 目录][map-list]；找受体图可查 [Hansen][hansen]、[JuSpace][juspace]。
- **从组织数据生成脑区图：**AHBA + abagen；细胞类型图需另外选择标记和映射方法。
- **空间与分区：**MNI152 是体积参考空间，fsaverage/fsLR 是表面参考体系；Schaefer/Glasser 是脑区分区。选好空间后，才能把 MRI 指标和生物学指标对应到相同位置。[空间说明][spaces]

使用时只需先记住三点：**确认指标含义；确认空间和覆盖一致；空间相关用于提出生物学假设，不能直接证明机制。**正式关联检验还应考虑空间自相关。[空间检验说明][nulls]

> 本文由 AI 辅助整理与文献核查，尚未经人工专家审定；未复算各图谱原始数据。

[ahba]: https://brain-map.org/support/documentation/human-brain-atlas-microarray-data-download
[abagen]: https://abagen.readthedocs.io/en/stable/user_guide/expression.html
[gene-pc1]: https://netneurolab.github.io/neuromaps/listofmaps.html#abagen-genepc1-fsaverage-10k
[brainspan]: https://www.brainspan.org/
[gtex]: https://www.gtexportal.org/home/aboutAdultGtex
[abc]: https://alleninstitute.github.io/abc_atlas_access/descriptions/WHB-10Xv3.html
[cell-paper]: https://pubmed.ncbi.nlm.nih.gov/37824663/
[hansen]: https://github.com/netneurolab/hansen_receptors
[hansen-paper]: https://www.nature.com/articles/s41593-022-01186-3
[map-list]: https://netneurolab.github.io/neuromaps/listofmaps.html
[juspace]: https://github.com/juryxy/JuSpace
[serotonin]: https://pubmed.ncbi.nlm.nih.gov/28053035/
[gaba]: https://www.sciencedirect.com/science/article/pii/S1053811921001555
[pet-metrics]: https://journals.sagepub.com/doi/pdf/10.1038/sj.jcbfm.9600493
[metabolism]: https://pubmed.ncbi.nlm.nih.gov/20837536/
[fdg]: https://snmmi.org/common/Uploaded%20files/Web/Clinical%20Practice/Procedure%20Standards/2024/SNMMI_EANM%20Brain%20F18%20FDG%20PET%20Imaging%202.0%20JNM.pdf
[julich]: https://julich-brain-atlas.de/atlas/probabilistic-maps
[bigbrain]: https://bigbrainproject.org/maps-and-models.html
[bigbrain-space]: https://ftp.bigbrainproject.org/bigbrain-ftp/FAQ.html
[myelin]: https://pubmed.ncbi.nlm.nih.gov/21832190/
[mt]: https://pubmed.ncbi.nlm.nih.gov/15349868/
[qsm]: https://pmc.ncbi.nlm.nih.gov/articles/PMC10950544/
[adni]: https://adni.loni.usc.edu/data-samples/adni-data/neuroimaging/pet/
[amyloid]: https://www.accessdata.fda.gov/drugsatfda_docs/label/2025/202008s046lbl.pdf
[tau]: https://dailymed.nlm.nih.gov/dailymed/drugInfo.cfm?setid=b483abad-5230-462a-adfb-1a65160f01d0
[alpha-syn]: https://www.nature.com/articles/s41467-023-42305-3
[tdp]: https://www.nature.com/articles/s41467-025-64540-6
[tdp-human]: https://ir.acimmune.com/news-releases/news-release-details/ac-immune-presents-first-vivo-images-brain-tdp-43-pathology
[spaces]: https://netneurolab.github.io/neuromaps/user_guide/atlases.html
[nulls]: https://netneurolab.github.io/neuromaps/user_guide/nulls.html