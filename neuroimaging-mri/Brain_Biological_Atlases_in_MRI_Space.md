---
ai_assisted: true
review_status: ai_reviewed
last_reviewed: 2026-10-12
---

# Brain Biological Atlases in MRI Space

## 脑影像空间中的生物学图谱：测量含义、资源与解释边界

> 核查说明：本文经 AI 辅助核查，依据原始研究、官方数据说明与测量规范修订。核查日期为 2026-10-12；尚未经人工专家审定，未下载、重建或复算各资源的原始数据。文中链接支持相邻内容；新示踪剂的研发进展与已验证的测量用途分别说明。

## 1. 核心原则：先分清资源类型和测量对象

本文介绍转录组、细胞类型、分子 PET、代谢/生理、病理蛋白与组织性质资源。它们可能来自健康成人、发育人群、疾病队列、尸检组织或其他物种，不能一概称为“正常人脑图谱”。

需要区分三个层级：**FDG-PET、ASL 和 QSM 是测量方法；AHBA、ABC Atlas 和 ADNI 是数据资源；经过明确定义的采样、配准与汇总，才得到用于空间比较的具体参考图**。一项资源也可能同时提供多种数据产品。

在 MRI 研究中，参考图可以帮助提出生物学假设，但不能跳过下面的区别：

- 空间相关不等于因果关系。
- mRNA 表达不等于蛋白水平、转录速率或神经活动。
- 受体结合指标不等于神经递质浓度、释放量或“系统活性”。
- 细胞标记基因富集不等于细胞绝对数量，更不等于疾病状态。
- 健康参考图与疾病 MRI 模式的相关，不等于已测到患者相应分子的改变。

[neuromaps 原始论文][neuromaps-paper]提供了跨参考空间比较脑图的框架；具体分析仍须查阅每张图的来源、指标和适用范围。

## 2. 转录组图谱（Transcriptomic atlases）

### Allen Human Brain Atlas（AHBA）

常用 AHBA 数据是**成人尸检组织样本的批量微阵列 mRNA 表达信号**，反映采样组织中的相对基因表达。它不是单细胞测量，也不直接测量基因转录速率、蛋白含量或神经活动。

AHBA 的主要成人微阵列数据来自 6 位供体，空间采样离散且不均匀；6 位均有左半球采样，只有 2 位有右半球采样。样本有供体 MRI 与 MNI 坐标，但这不意味着原始数据已经是连续、完整的逐体素表达图。[官方微阵列数据说明][ahba]

与 MRI 分区整合时，需要明确探针选择、样本与脑区的匹配、归一化、供体汇总和缺失区域处理；镜像或插值不能当作新增的实测组织样本。处理流程会影响空间关联结果。[abagen 官方表达处理说明][abagen]、[abagen 原始论文][abagen-paper]

合理用途是考察 MRI 模式与某些基因或基因集合的空间共变，提出突触、免疫或髓鞘等分子背景假设。不能仅凭相关就认定基因被上调、蛋白活性改变或患者具有某种分子病理。基因类别富集还须考虑基因间共表达造成的偏差，不能只用普通随机基因集检验。[Fulcher et al., 2021][gene-enrichment]

### BrainSpan 与 GTEx

| 资源 | 主要信息 | 用于 MRI 解释时的边界 |
| --- | --- | --- |
| BrainSpan | 人脑发育过程中不同年龄与解剖结构的转录信息；项目还含胎儿脑区激光显微切割表达、原位杂交及解剖参考资源 | 要匹配发育阶段及具体数据产品，不能默认是成人 MNI 全脑连续表达图 |
| GTEx Adult | 多组织基因表达及遗传调控/eQTL 信息，脑组织按解剖部位采集 | 适合组织表达与遗传调控背景分析，不是密集的逐体素 MNI 脑图 |

来源：[BrainSpan 官方项目][brainspan]、[GTEx Adult 官方说明][gtex]与[GTEx 原始图谱论文][gtex-paper]。

## 3. 细胞类型图谱（Cellular atlases）

### Allen Brain Cell Atlas（ABC Atlas）

ABC Atlas 是整合不同物种、测序方式及研究项目的平台，不能把其中的小鼠空间图直接当成人脑 MRI 图。

例如，人类全脑代表性数据 **WHB-10Xv3** 使用单核 RNA 测序（snRNA-seq），来自 3 位成人尸检供体、约 100 个解剖采样位置。它主要支持转录定义的细胞分类与采样脑区间差异；这与完整的人脑逐体素细胞密度图有区别。[WHB-10Xv3 官方说明][abc-human]、[Siletti et al., 2023][siletti]

常见大类包括兴奋性神经元、抑制性神经元、星形胶质细胞、少突胶质细胞和小胶质细胞，但具体分类通常更细，还包含其他非神经元类型。使用时要区分：

- **单细胞/单核转录组**：记录捕获的细胞或细胞核表达，分类和捕获比例会受解离、富集与测序偏差影响。
- **空间转录组**：提供特定组织切片或参考空间中的位置，覆盖和分辨率依方法而异。
- **基于标记基因的富集/反卷积**：是模型估计，需要验证，不能直接称为组织学细胞计数。

因此，“细胞组成”应限定为具体采样与模型条件下的组成信息；捕获核比例不是单位体积的绝对细胞数。用于人脑 MRI 前，应核实物种、解剖标签、坐标与映射依据。例如，ABC 的小鼠全脑细胞项目使用小鼠 CCF 参考体系，不是人脑 MNI 空间。[小鼠全脑项目说明][abc-mouse]

## 4. 受体与转运体图谱（Molecular PET atlases）

### 4.1 PET 指标的含义

受体/转运体 PET 通过示踪剂信号和动力学或参考区模型，估计结合潜能、分布容积等量；某些图使用摄取比。**具体数值的含义取决于示踪剂和定量方法**，不能全部称为绝对受体密度。

对于适用的可逆结合模型，非可置换结合潜能为：

```math
BP_{\mathrm{ND}}=f_{\mathrm{ND}}\frac{B_{\mathrm{avail}}}{K_D}
```

这里， $B_{\mathrm{avail}}$ 是可供示踪剂结合的位点浓度， $K_D$ 是平衡解离常数， $f_{\mathrm{ND}}$ 是非可置换组织组分中的游离比例。这个关系说明，结合潜能还受亲和力、游离比例与占据状态影响，不能直接等同于绝对受体数量或神经递质释放量。[Innis et al., 2007 共识命名][pet-nomenclature]

部分图谱将 PET 与尸检自显影标定结合，提供估计的最大结合位点密度，如 Beliveau 血清素图谱和 Nørgaard 苯二氮䓬位点图谱。它们与未经密度标定的结合潜能图仍应区分。[Beliveau et al., 2017][serotonin]、[Nørgaard et al., 2021][gaba-atlas]

### 4.2 常见靶点与可支持的解释

| 系统 | 靶点示例 | 测量与解释边界 |
| --- | --- | --- |
| 多巴胺 | D1、D2/3、DAT | 受体或转运体结合指标的空间分布；不是多巴胺释放或某个人的奖赏、运动、认知能力 |
| 血清素 | 5-HT1A、5-HT2A、SERT | 特定受体/转运体分布；不能直接表示情绪状态或血清素调节强度 |
| GABA | 常见 flumazenil 图 | 主要反映 GABA-A 受体相关苯二氮䓬结合位点；不涵盖全部 GABA-A 亚型，不是 GABA 浓度或兴奋/抑制比值 |
| 谷氨酸 | mGluR5 | 特定代谢型受体的结合指标；ABP688 等示踪剂结合变构位点，不代表全部谷氨酸受体、谷氨酸浓度或突触可塑性本身 |

靶点概况见 [Hansen et al., 2022][hansen-paper]；GABA 位点与 mGluR5 的测量依据分别见 [Nørgaard 原研究][gaba-atlas]和 [ABP688 人体 PET 原研究][mglur5]。常被简称为“D2”的示踪剂可能同时涉及 D2/3；例如 raclopride 在高信号纹状体与低密度皮层中的定量适用性不同，不能忽略信噪比和原研究限制。[Hansen 原论文][hansen-paper]

Hansen 2022 图谱整合不同健康队列的群体平均图，并非同一批参与者完成所有示踪剂扫描。跨靶点比较通常关注标准化后的相对空间模式；不同示踪剂/指标的绝对数值不能直接横向比较。[原研究数据与代码][hansen-data]

## 5. 代谢与生理图谱（Metabolic and physiological maps）

### FDG-PET：葡萄糖代谢相关信号

FDG 是葡萄糖类似物；PET 记录其摄取、磷酸化及组织内滞留相关信号，常用于表征区域葡萄糖代谢。**静态 SUV/SUVR 不等于绝对脑葡萄糖代谢率 CMRglc**；绝对定量通常采用动态采集，并结合输入函数、血糖及动力学模型，具体要求以所用定量方案为准。

FDG 信号涉及神经元与胶质细胞的代谢，且受血糖、摄取期状态、炎症和处理方法等影响。它不是神经元放电率的直接测量。[SNMMI/EANM 脑 FDG-PET 测量规范，Version 2.0][fdg]

### CBF：脑血流/灌注

CBF 表示单位时间、单位脑组织的血流量，常用单位为 mL/100 g/min，可由 ASL MRI 或水示踪剂 PET 等估计。应记录采集和定量方法；ASL 结果受动脉通过时间、标记效率等因素影响。灌注与神经活动有关，但不是氧消耗或神经活动的直接测量。[ASL 共识测量说明][asl]

### CMRO₂：脑氧代谢率

CMRO₂ 表示单位时间、单位脑组织消耗的氧量。经典方法包括氧-15 PET；MRI 估计依赖特定氧合测量、模型及校准。[氧-15 PET/MRI 原研究][oxygen-pet]、[校准 MRI 原研究][oxygen-mri]

按稳态质量守恒关系：

```math
\mathrm{CMRO}_2=\mathrm{CBF}\times\mathrm{OEF}\times C_{\mathrm{a}O_2}
```

OEF 是氧摄取分数， $C_{\mathrm{a}O_2}$ 是动脉血氧含量。例如，CBF 用 mL blood/100 g tissue/min，氧含量用 μmol O₂/mL blood，OEF 用 0–1 分数时，CMRO₂ 的单位为 μmol O₂/100 g tissue/min。CBF、OEF 与氧含量必须对应同一生理条件。[校准 MRI 原研究][oxygen-mri]

因此，CBF 增加不能单独证明 CMRO₂ 增加；普通 BOLD 信号也不是 CMRO₂ 图，定量氧代谢需要额外测量与模型。[校准 MRI 原研究][oxygen-mri]

## 6. 病理蛋白图谱（Pathological biomarker maps）

这些图通常研究特定年龄或疾病人群的病理分布，不能直接归入“正常人脑生物属性”。

### Amyloid PET

常用示踪剂主要结合聚集性/纤维性 Aβ 沉积，临床示踪剂的验证目标包括 Aβ 神经突性斑块（neuritic plaques）负荷。它不是总 Aβ 或可溶性寡聚体的测量；阳性本身也不证明认知症状一定由阿尔茨海默病导致。[FDA AMYVID 标签][amyloid-label]

### Tau PET

测量的是特定示踪剂可结合的聚集 tau。不同 tau 构象、疾病和示踪剂的适用性不同。例如 flortaucipir 主要针对 AD 相关成对螺旋丝 tau；部分脉络丛、纹状体与脑干核团信号可能来自非靶点结合，不能把所有摄取都解释为 tau。[TAUVID 官方标签][tau-label]

### α-synuclein 与 TDP-43：区分研发进展与成熟参考图谱

截至本次核查，二者均已有研究进展，不能写成“完全没有人体研究”；本文也不把早期试验图像视为通用、成熟的全脑参考图谱。

- **α-synuclein**：ACI-12589 的 2023 年原研究已包含人体 PET，在多系统萎缩（MSA）显示明显结合，而帕金森病（PD）的结合有限。不同疾病间结果不能直接推广，也不能把该示踪剂当作所有突触核蛋白病的统一测量工具。[Smith et al., 2023][alpha-syn]
- **TDP-43**：ACI-19626 已有 2025 年发表的临床前同行评议研究，主要是组织、细胞及非人灵长类验证，并已进入早期人体评估。公司于 2026-03-19 公布一期人体影像进展，并于 2026-05-22 公布 ALS 队列的初步结果。**公司/会议披露与同行评议的广泛人体验证不是同一证据层级**，不能据此宣称已建立成熟通用图谱。[临床前原研究][tdp-paper]、[3 月公司公告][tdp-march]、[5 月公司公告][tdp-may]

新示踪剂进展较快；实际使用前需再次检查公开论文、验证人群与定量方法。

## 7. 组织性质与组织学图谱（Tissue properties and histology）

### 7.1 髓鞘相关 MRI 指标

**T1w/T2w ratio 是 T1 加权与 T2 加权图像的强度比，不是 T1/T2 弛豫时间比。** 经配准和适当偏置校正后，它可作为皮层髓鞘相关对比的代理指标，但不是髓鞘含量的直接定量，也不能直接推断神经传导速度。[Glasser & Van Essen, 2011][myelin]

其结果受扫描序列、射频场、部分容积与非髓鞘组织成分影响；在疾病中不能直接把强度比改变称为脱髓鞘。[B1+ 偏置原研究][myelin-bias]、[MS 尸检皮层验证研究][myelin-histology]

**磁化转移（MT）**通过自由水与大分子相关质子池之间的磁化交换产生对比。MTR、MTsat 与定量 MT 参数不同，可提供髓鞘相关信息，但并非对髓鞘绝对特异，不能与 T1w/T2w 数值互换。[MTR 尸检验证研究][mt]、[MT 与髓鞘水原研究][mt-water]

### 7.2 QSM：磁化率图，不是直接铁含量图

QSM 利用梯度回波相位数据估计组织相对于参考区域的磁化率。在富铁深部灰质中，磁化率与铁浓度有尸检验证关系；但髓鞘、钙化、血液与组织取向等也会影响信号。[Langkammer et al., 2012][qsm-iron]、[ISMRM QSM 共识][qsm-consensus]

因此宜称“磁化率图”或有明确验证条件的“铁敏感代理图”，并报告参考区域与处理流程。不能直接把 QSM 值解释为铁代谢速率、氧化应激或疾病原因。

### 7.3 Julich-Brain：细胞构筑概率分区

Julich-Brain 基于尸检切片中的细胞体分布和层状组织特征识别脑区边界，重建后配准到参考空间。常用输出是**脑区概率图与最大概率分区图**，反映对齐后的区域位置及供体间差异，而不是下载后即可得到的全脑神经元密度或皮层层厚度图。[Amunts et al., 2020][julich-paper]

应注明版本、参考空间与覆盖；尚未完成显微定界的部分可能以 gap maps 标示。概率分区不能代替特定个体的组织学测量。[Julich 官方概率图说明][julich]

## 8. 坐标模板、皮层分区与文件格式必须分开

| 名称 | 类型 | 需要记录的信息 |
| --- | --- | --- |
| MNI152 | 体积参考模板/空间家族 | 具体模板版本、对称性、体素大小、坐标变换与覆盖 |
| FreeSurfer fsaverage | 皮层表面参考体系 | 网格密度、半球顺序、顶点对应及 medial wall 掩膜 |
| HCP fs_LR / fsLR | 皮层表面参考体系 | 例如 32k/164k 网格；不能与 fsaverage 同尺寸数组直接按索引比较 |
| Schaefer atlas | 基于静息态功能连接的皮层分区 | 分区数、网络版本及其在 MNI/fsaverage/fsLR 中的具体表示 |
| Glasser / HCP-MMP1.0 | 多模态 MRI 皮层分区 | 每半球 180 区、共 360 区；它不是坐标空间，也不是尸检细胞构筑图 |
| NIfTI、GIFTI、CIFTI | 文件格式 | 格式或数组尺寸相同，不证明空间已经对齐 |

参考：[neuromaps 坐标体系说明][spaces]、[Schaefer 原作者资源][schaefer]、[Glasser et al., 2016][glasser]。Schaefer 与 HCP-MMP1.0 的上述皮层版本不提供完整的皮层下或小脑分区。

**操作限制：**重采样不能修复错误配准，也不会增加独立的生物学采样信息。连续图可按方法要求插值；离散脑区标签通常采用最近邻等保留标签的方式。PET 体积图直接投影至表面可能放大部分容积效应并引入曲率偏差，需查看原图处理和验证。[neuromaps 变换说明][transforms]

具体例子：neuromaps 对 Beliveau 2017 血清素图与 Nørgaard 2021 flumazenil 图建议优先使用所提供的 fsaverage 版本，其 MNI152 版本仅用于皮层下数据。不能仅因文件标为 MNI152，就默认它适合皮层逐体素分析。[官方图谱目录与逐图警告][map-list]

## 9. 查找资源时：数据集、工具箱和具体参考图的区别

| 资源 | 定位与使用提醒 |
| --- | --- |
| AHBA / ABC Atlas / BrainSpan / GTEx | 见前文；分别检查物种、年龄、测量方式、采样位置及是否存在经过验证的 MRI 映射 |
| Hansen receptor atlas | 原研究整理的受体/结合位点/转运体参考图及分析数据；检查示踪剂、指标、原始队列与版本 |
| JuSpace | 空间关联分析工具及 PET/SPECT 模板集合；应引用所用模板的原始研究，不能把全部模板称为 PET，例如原始 DAT 模板来自 SPECT |
| neuromaps | 整理脑参考图、跨空间转换及空间统计的工具；每张图有独立来源、指标、许可与使用限制 |
| ADNI | AD 相关纵向多模态队列；提供个体扫描、区域指标与质控数据，不是单一健康脑规范图谱 |
| Human Connectome Project（HCP） | 多模态人脑数据项目；群体平均 T1w/T2w 图是 MRI 代理图，需注明数据发布与处理版本 |
| Julich-Brain | 组织学驱动的概率脑区分区；检查版本、空间和覆盖 |

数据/工具依据：[Hansen 仓库][hansen-data]、[JuSpace 原论文][juspace-paper]与[官方仓库][juspace]、[neuromaps 原论文][neuromaps-paper]、[ADNI PET 官方说明][adni]、[HCP 群体平均数据说明][hcp]。

## 10. 不用统一“高/中/低可靠性”替代具体评价

原稿的类别排行榜没有定义可靠性的含义，因此删除。下面是**本文建议的阅读与选图维度**，不是新的统一科学评级：

| 评价维度 | 要检查什么 |
| --- | --- |
| 测量对象与特异性 | 指标反映哪种信号？有无非靶点结合或其他组织成分影响？ |
| 定量方法 | 绝对量、相对摄取、标准化表达还是模型估计？单位和参考区是什么？ |
| 样本与覆盖 | 物种、年龄、健康/疾病状态、供体数、半球及脑区覆盖是否匹配？ |
| 验证与复现 | 是否有重测、组织学或独立队列验证？结论能否跨处理流程复现？ |
| 空间质量 | 配准、平滑、分区、部分容积与缺失区域如何处理？ |
| 推断层级 | 结果是描述性共变、统计关联，还是经过独立干预验证的机制？ |

经过靶点验证的测量，并不会自动把 MRI—图谱相关变成因果证据。反过来，转录组的间接性也不意味着它没有研究价值；关键是推断是否与证据相称。

## 11. 从 MRI 空间模式到可检验的生物学假设

1. **先定义问题。** 明确 MRI 指标、研究人群与希望检验的生物学假设，再选择参考图，避免只挑显著结果来解释。
2. **核对图的含义。** 保存原研究、数据版本、样本、示踪剂/测量模型、单位和许可；确认该图适用于当前脑区和人群。
3. **统一空间与覆盖。** 验证配准、半球、脑区顺序、medial wall 和共同有效掩膜；缺失不能默认补为零。选择适合模态的体积或表面表示。
4. **估计空间关联并检验。** 报告相关系数/效应量；显著性检验应考虑空间自相关，不能把相邻体素或顶点当作完全独立样本。选择与几何和采样匹配的空间零模型；皮层球面旋转不能直接套用到皮层下体素。空间零模型本身也需适用性检查。[空间零模型比较原研究][spatialnull-paper]、[neuromaps 零模型说明][nulls]
5. **检查稳健性和选择偏差。** 处理多重比较；比较合理的分区尺度、平滑及预处理方案。对转录组还应检查供体差异、归一化和基因集合共表达；对 PET 检查示踪剂/参考区和跨队列一致性。
6. **把结果写成假设。** 例如“该 MRI 模式与某受体参考分布空间相关，提示值得检验的关联”，不能写成“该受体异常导致了此 MRI 改变”。
7. **用独立证据推进机制解释。** 可结合患者自身的分子测量、纵向数据、组织验证或干预研究，按其研究设计分别评价证据。

这是建议的分析流程；其中的空间检验和基因富集要求有方法研究支持，但不构成一套适用于所有研究的固定操作标准。

## 12. 本次核查修订记录

- 将“全部是正常人脑分布”改为明确物种、人群与资源类型。
- 将 AHBA 的“直接转录水平”改为批量 mRNA 表达信号，并补充离散采样和供体限制。
- 区分细胞分类、捕获比例、标记富集和组织绝对细胞密度。
- 区分 PET 结合参数、密度标定和神经递质活动；收紧 GABA-A 与 mGluR5 的解释。
- 补充 FDG、CBF 和 CMRO₂ 的测量条件，更新 α-synuclein/TDP-43 研发信息并注明证据层级。
- 修正 T1w/T2w 命名、QSM 铁特异性及 Julich 输出类型。
- 分开坐标模板、分区图谱和文件格式，加入 PET 表面/体积版本限制。
- 删除无依据的统一可靠性排序，补充空间零模型与机制推断边界。

<!-- 以下为正文引用链接，使用前仍应核对具体数据产品及版本。 -->
[neuromaps-paper]: https://www.nature.com/articles/s41592-022-01625-w
[ahba]: https://brain-map.org/support/documentation/human-brain-atlas-microarray-data-download
[abagen]: https://abagen.readthedocs.io/en/stable/user_guide/expression.html
[abagen-paper]: https://pmc.ncbi.nlm.nih.gov/articles/PMC8660024/
[gene-enrichment]: https://www.nature.com/articles/s41467-021-22862-1
[brainspan]: https://www.brainspan.org/
[gtex]: https://www.gtexportal.org/home/aboutAdultGtex
[gtex-paper]: https://pmc.ncbi.nlm.nih.gov/articles/PMC7737656/
[abc-human]: https://alleninstitute.github.io/abc_atlas_access/descriptions/WHB-10Xv3.html
[siletti]: https://pubmed.ncbi.nlm.nih.gov/37824663/
[abc-mouse]: https://alleninstitute.github.io/abc_atlas_access/descriptions/WMB-taxonomy.html
[pet-nomenclature]: https://journals.sagepub.com/doi/pdf/10.1038/sj.jcbfm.9600493
[serotonin]: https://pubmed.ncbi.nlm.nih.gov/28053035/
[gaba-atlas]: https://www.sciencedirect.com/science/article/pii/S1053811921001555
[hansen-paper]: https://www.nature.com/articles/s41593-022-01186-3
[mglur5]: https://pubmed.ncbi.nlm.nih.gov/17268022/
[hansen-data]: https://github.com/netneurolab/hansen_receptors
[fdg]: https://snmmi.org/common/Uploaded%20files/Web/Clinical%20Practice/Procedure%20Standards/2024/SNMMI_EANM%20Brain%20F18%20FDG%20PET%20Imaging%202.0%20JNM.pdf
[asl]: https://pmc.ncbi.nlm.nih.gov/articles/PMC4190138/
[oxygen-pet]: https://pubmed.ncbi.nlm.nih.gov/33502738/
[oxygen-mri]: https://pubmed.ncbi.nlm.nih.gov/22227047/
[amyloid-label]: https://www.accessdata.fda.gov/drugsatfda_docs/label/2025/202008s046lbl.pdf
[tau-label]: https://dailymed.nlm.nih.gov/dailymed/drugInfo.cfm?setid=b483abad-5230-462a-adfb-1a65160f01d0
[alpha-syn]: https://www.nature.com/articles/s41467-023-42305-3
[tdp-paper]: https://www.nature.com/articles/s41467-025-64540-6
[tdp-march]: https://ir.acimmune.com/news-releases/news-release-details/ac-immune-presents-first-vivo-images-brain-tdp-43-pathology
[tdp-may]: https://www.globenewswire.com/news-release/2026/05/22/3300024/0/en/ac-immune-presents-new-phase-1-data-indicating-higher-uptake-of-tdp-43-pet-tracer-aci-19626-in-patients-with-als.html
[myelin]: https://pubmed.ncbi.nlm.nih.gov/21832190/
[myelin-bias]: https://pubmed.ncbi.nlm.nih.gov/35697132/
[myelin-histology]: https://pubmed.ncbi.nlm.nih.gov/28833433/
[mt]: https://pubmed.ncbi.nlm.nih.gov/15349868/
[mt-water]: https://pubmed.ncbi.nlm.nih.gov/15906291/
[qsm-iron]: https://pubmed.ncbi.nlm.nih.gov/22634862/
[qsm-consensus]: https://pmc.ncbi.nlm.nih.gov/articles/PMC10950544/
[julich-paper]: https://pubmed.ncbi.nlm.nih.gov/32732281/
[julich]: https://julich-brain-atlas.de/atlas/probabilistic-maps
[spaces]: https://netneurolab.github.io/neuromaps/user_guide/atlases.html
[schaefer]: https://github.com/ThomasYeoLab/CBIG/blob/master/stable_projects/brain_parcellation/Schaefer2018_LocalGlobal/README.md
[glasser]: https://www.nature.com/articles/nature18933
[transforms]: https://netneurolab.github.io/neuromaps/user_guide/transformations.html
[map-list]: https://netneurolab.github.io/neuromaps/listofmaps.html
[juspace-paper]: https://pmc.ncbi.nlm.nih.gov/articles/PMC7814756/
[juspace]: https://github.com/juryxy/JuSpace
[adni]: https://adni.loni.usc.edu/data-samples/adni-data/neuroimaging/pet/
[hcp]: https://hcpx-demo.humanconnectome.org/study/hcp-young-adult/article/s1200-group-average-data-release
[spatialnull-paper]: https://doi.org/10.1016/j.neuroimage.2021.118052
[nulls]: https://netneurolab.github.io/neuromaps/user_guide/nulls.html
