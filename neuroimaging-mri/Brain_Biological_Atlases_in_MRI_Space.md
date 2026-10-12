---
ai_assisted: true
review_status: ai_reviewed
last_reviewed: 2026-10-12
---

# 脑影像空间中的生物学指标图谱：广泛检索与资源速查

**目的：整理能与脑 MRI 的体素、皮层顶点或脑区对应的生物学信息：指标是什么、有哪些图谱、在哪里获取。**

范围以人脑为主，兼顾分子、细胞、组织性质、生理活动，以及发育和疾病相关参考图。检索日期为 **2026-10-12**，依据原始研究、官方数据说明和资源库；这是广泛检索后的代表性目录，不是穷尽全部文献的系统综述。

## 概览

| 层面 | 可以查找的指标 | 代表资源 |
| --- | --- | --- |
| **分子与细胞** | 基因表达、空间转录组、细胞类型丰度、蛋白定位与合成、HDAC、受体/转运体、SV2A、TSPO/COX-1、线粒体表型 | AHBA、MAGICC、HMBA、CellMaps、HPA、Hansen/NRU、MitoBrainMap |
| **组织结构与材料性质** | 细胞构筑、皮层层厚、染色深度轮廓、髓鞘水、弛豫率、磁化率、纤维方向、水扩散、组织刚度与阻尼 | Julich、BigBrainWarp、NextBrain、AHEAD、χ-separation、HCP1065、MRE134 |
| **生理与活动** | 葡萄糖/氧代谢、灌注、血容量、血管分布、血管反应性、代谢物、电生理频谱与时间尺度 | Raichle 系列、Braincharter、动脉 atlas、CVRmap、MRS 参考研究、HCP MEG、MNI iEEG |
| **功能组织与空间变化** | 功能连接梯度、形态参照、发育扩张、跨物种差异、年龄轨迹、病理蛋白及疾病差异 | Margulies/HCP、Hill/Xu、Brain Charts、ADNI、ENIGMA |

下表用三个简单标记说明获取形式：

- **图**：已有体积图或表面图；仍需核对模板版本和覆盖。
- **表**：已有脑区、组织样本或连接矩阵数据，可按位置匹配。
- **数据**：个体影像、细胞点云或组织切片，需要进一步映射、选择或汇总。

“图”只表示有图文件，**不表示全脑每个位置均为直接实测，也不表示指标完全特异**。

## 一、分子与细胞

### 1. 基因表达、空间转录组与细胞组成

| 指标 | 具体资源/入口 | 反映什么 | 空间与获取形式 |
| --- | --- | --- | --- |
| 基因 mRNA 表达 | [AHBA][ahba] + [abagen][abagen] | 成人脑组织的相对基因表达 | **表/数据**：离散样本有 MRI/MNI 坐标，需汇总到脑区 |
| 密集皮层表达估计 | [MAGICC][magicc] | 单个基因表达及表达梯度 | **图/表**：原始 DEM 仅覆盖左皮层；AHBA 插值和平滑衍生，[NiSpace][nispace]另有整理版 |
| 全脑基因表达预测 | [Gryglewski mRNA atlas][gryglewski] | AHBA 衍生的空间插值预测 | **图**：官方支持按基因取 MNI 体积/FreeSurfer 表面数据；模板与覆盖按文件核对 |
| 基因表达主梯度 | [AHBA gene PC1][gene-pc1] | 多基因表达的主要空间变化 | **图**：fsaverage；不是某个基因的表达图 |
| 人类基底节空间表达与细胞分类 | [HMBA-BG][hmba] | 局部细胞的位置、基因表达与类型 | **数据**：切片/细胞点云；部分人类 CCF 坐标已对应 MRI 参考，[CCF 与 MNI 配准说明][hmba-ccf] |
| 单核转录定义的细胞类型 | [ABC Atlas：WHB-10Xv3][abc] | 已采样脑区的细胞类型及表达差异 | **表/数据**：解剖采样标签；不是现成逐体素细胞密度图 |
| 6 大类细胞相对丰度 | [Pak / CellMaps][cellmaps] | 神经元、星形胶质、内皮、小胶质、少突胶质及 OPC 的相对丰度估计 | **图**：作者 MNI 体积图；[NiSpace][nispace]提供其他 MNI/表面版本 |
| 24 类皮层细胞丰度 | [Zhang cellular connectome][zhang] | 兴奋性、抑制性及非神经元亚类的相对组成估计 | **表**：样本映射至 fsLR 32k，再按皮层分区汇总；并非每个顶点都有实测细胞 |

**必要区别：**MAGICC、Gryglewski、Pak 和 Zhang 都依赖 AHBA；后两者是反卷积估计，不能当作独立的组织学细胞计数。HMBA 人类空间数据的实测覆盖是基底节及邻近组织，不能因参考模板覆盖全脑就把表达覆盖也称为全脑。[MAGICC 原研究][magicc-paper]、[Gryglewski 原研究][gryglewski-paper]、[Pak 原研究][pak-paper]、[Zhang 原研究][zhang-paper]、[HMBA 官方说明][hmba]

补充背景资源：[BrainSpan][brainspan]面向人脑发育表达，[GTEx][gtex]提供多组织表达与遗传调控信息；使用时按年龄和解剖区域匹配，不能默认是成人全脑连续影像图。

### 2. 蛋白与表观遗传相关指标

| 指标 | 具体资源/入口 | 反映什么 | 空间与获取形式 |
| --- | --- | --- | --- |
| 蛋白定位/区域表达 | [Human Protein Atlas Brain][hpa] | 抗体染色等蛋白定位信息及配套 RNA 数据 | **表/数据**：脑区与组织切片；不是现成全脑 MNI 蛋白组图 |
| 区域脑蛋白合成率（rCPS） | [¹¹C-Leucine 数据与群体图][rcps] | 动力学模型估计的蛋白合成速率 | **图/数据**：有 fsaverage 群体表面图及个体动态 PET；须区分健康/FXS、清醒/镇静条件 |
| HDAC 相关结合 | [Wey / Martinostat 图][hdac] | class I HDAC 1–3 相关 PET 指标 | **图**：MNI152 2 mm，SUVR；不是全局组蛋白乙酰化或酶催化活性 |
| DNA 甲基化与染色质构象 | [人脑单核表观基因组 atlas][epigenome] | 细胞类型及脑区的甲基化/调控特征 | **表/数据**：解剖区标签；“3D genome”指核内染色质，不是 MRI 三维坐标 |

蛋白含量、蛋白合成速率、mRNA 和表观遗传调控是不同层级的指标。相应测量依据见 [HPA 原研究][hpa-paper]、[Leucine 原研究][rcps-paper]与 [HDAC 原研究][hdac-paper]。

### 3. 受体、转运体与突触相关蛋白

| 指标方向 | 具体图谱/入口 | 代表指标 | 空间与获取形式 |
| --- | --- | --- | --- |
| 多系统受体/转运体 | [Hansen receptor atlas][hansen]、[JuSpace][juspace] | D1、D2/3、DAT；5-HT1A/1B/2A、SERT；mGluR5；α4β2、M1、VAChT；NET、H3、CB1、MOR 等 | **图/表**：MNI 体积参考图和分区数据，按所选图确认覆盖与指标 |
| 血清素系统 | [Beliveau atlas][serotonin] | 多种 5-HT 受体与 SERT | **图**：皮层优先提供的 fsaverage；其 neuromaps MNI 版仅用于皮层下 |
| GABA-A 相关位点 | [Nørgaard flumazenil atlas][gaba] | 苯二氮䓬结合位点的估计密度 | **图**：同样区分皮层表面与皮层下 MNI 版本 |
| 囊泡单胺转运 | [VMAT2 / DTBZ][vmat2] | VMAT2 结合指标 | **图/数据**：NiSpace/JuSpace 整理图、OpenNeuro PET/MRI；具体空间查下载版本 |
| 突触相关蛋白 SV2A | [Johansen 2024 SV2A atlas][sv2a] | UCB-J PET 经标定的 SV2A 位点密度估计 | **图**：皮层用 fsaverage，皮层下用 MNI；官方 MNI 皮层图仅供可视化 |

PET 结合指标通常不是神经递质浓度或释放量；SV2A 是突触相关代理，不是逐突触计数。JuSpace 某些模板来自 **SPECT**，如部分 DAT 图，应按来源注明。[Hansen 原研究][hansen-paper]、[SV2A 原研究][sv2a-paper]、[PET 指标说明][pet-metrics]

### 4. 免疫/炎症相关分子与线粒体

| 指标 | 具体资源/入口 | 反映什么 | 空间与获取形式 |
| --- | --- | --- | --- |
| TSPO | [Lois / PBR28 图][tspo] | TSPO 相关示踪剂摄取比 | **图**：MNI152 2 mm；不是小胶质细胞数量或炎症活性的直接图 |
| COX-1 | [PS13 Molecular Imaging Brain Atlas][cox1] | COX-1 相关分布容积 | **图**：MNI 与 fsaverage，有均值/SD、部分容积校正等版本 |
| 线粒体表型 | [MitoBrainMap / NeuroVault 16418][mitobrain] | CI/CII/CIV 活性、MitoD（密度代理）、TRC（组织呼吸容量）、MRC（密度归一化呼吸容量） | **图**：MNI 全脑预测图；具体模板按文件版本确认 |

TSPO 解释需考虑配体、结合基因型和细胞来源；TSPO 并非只表达在小胶质细胞中。健康 COX-1 分布也不能直接表示疾病炎症程度。[TSPO 人体组织研究][tspo-cell]、[基因型研究][tspo-genotype]、[COX-1 原研究][cox1-paper]

MitoBrainMap 的全脑图由**单供体局部组织测量和多模态 MRI 特征模型外推**得到，不能称为全脑直接实测或群体均值。[原研究][mitobrain-paper]

## 二、组织结构与材料性质

### 5. 细胞构筑、皮层层次与显微纤维

| 指标/参照 | 具体资源/入口 | 反映什么 | 空间与获取形式 |
| --- | --- | --- | --- |
| 细胞构筑脑区 | [Julich-Brain][julich] | 组织学定义的区域及位置变异 | **图**：概率图/最大概率分区；不是连续细胞密度图 |
| 层厚、染色深度轮廓、微结构梯度 | [BigBrainWarp][bigbrainwarp] | 单供体皮层六层厚度、50 个深度的染色 profiles 等 | **图**：BigBrain、fsaverage、fsLR 等产品 |
| 密集组织学概率分区 | [NextBrain][nextbrain] | 组织学标签及 MRI 分割参照 | **图/数据**：配准组织学/ex vivo MRI、概率 atlas 与分割工具；不是通用 MNI 神经元密度图 |
| 尸检受体密度与层深特征 | [EBRAINS / siibra receptor features][receptor-hist] | 定量自显影的区域受体密度和层深 profiles | **表**：脑区锚定；不同于 PET，也不是全脑逐体素连续图 |
| 显微纤维方向 | [3D-PLI / Julich fibre architecture][pli] | 偏振光推断的纤维方向 | **数据/局部图**：按具体组织块及配准产品使用，不能默认全脑 MNI 覆盖 |

BigBrain 的染色强度不等于绝对细胞计数；其层厚与活体 MRI 层厚也不是同一种测量。[层厚原研究][layers-paper]、[NextBrain 原研究][nextbrain-paper]、[受体自显影原研究][receptor-hist-paper]

### 6. 髓鞘、弛豫、磁化率与水扩散

| 指标 | 具体资源/入口 | 反映什么 | 空间与获取形式 |
| --- | --- | --- | --- |
| T1w/T2w | [HCP S1200 myelin map][myelin-map] | 髓鞘相关 MRI 强度对比 | **图**：如 fsLR 32k；不是 T1/T2 弛豫时间比 |
| R1、R2*、QSM 及推导髓鞘/铁图 | [AHEAD quantitative templates][ahead] | 弛豫率、磁化率及模型估计的组织特征 | **图**：MNI2009b 群体中位数/IQR 图 |
| R1、R2、PD、MVF | [Synthetic qMRI atlas][synthetic] | 弛豫率、质子密度及模型髓鞘体积分数 | **图**：MNI 均值/SD；MVF 不等于髓鞘水分数 |
| 髓鞘水分数（MWF） | [UBC Myelin Water Atlas][mwf] | 多回波 T2 测得的短 T2 水信号分数 | **图**：MNI 均值/SD |
| 顺磁与抗磁磁化率 | [χ-separation atlas][chiseparation] | 分离的磁化率来源，作为铁/髓鞘相关代理 | **图**：MNI2009cAsym；不是化学浓度 |
| FA、MD、张量/纤维方向、QA/GFA | [HCP1065 templates][hcp1065] | 水扩散方向性、张量或方向分布特征 | **图**：MNI 体积模板；DTI 与 QSDR 产品需区分 |

R1/R2/R2*、T1w/T2w、MWF 和 MVF 含义不同；铁、髓鞘、水及序列参数也会共同影响部分指标。它们应按“组织敏感指标”解释，不能一概直接等于某一种组织含量。[AHEAD 原研究][ahead-paper]、[Synthetic qMRI 原研究][synthetic-paper]、[MWF 原研究][mwf-paper]、[χ-separation 原研究][chi-paper]

### 7. 组织力学与宏观纤维连接

| 指标 | 具体资源/入口 | 反映什么 | 空间与获取形式 |
| --- | --- | --- | --- |
| 剪切刚度与阻尼 | [MRE134][mre] | 组织粘弹性 | **图**：134 名健康青年、50 Hz MRE 的 MNI152 2 mm 群体图 |
| 纤维束/结构连接 | [HCP1065 及 tract-to-region connectome][hcp1065] | 扩散成像推断的纤维方向、路径或连接关系 | **图/矩阵**：模板方向数据、tractography 与脑区连接 |

MRE 数值依驱动频率和反演方法；tractography 不能直接作为轴突数或突触连接计数。[MRE 原研究][mre-paper]、[结构连接原研究][tract-paper]

## 三、生理与活动

### 8. 能量代谢、灌注与氧摄取

| 指标 | 具体资源/入口 | 反映什么 | 空间与获取形式 |
| --- | --- | --- | --- |
| 葡萄糖代谢、氧代谢、CBF、CBV | [Raichle / Vaishnavi 参考图][metabolism]；[neuromaps 产品目录][map-list] | 葡萄糖利用、氧消耗、血流与血容量分布 | **图**：Raichle 系列提供 fsLR 164k 等版本 |
| 氧摄取分数（OEF）、CMRO₂、CBF | [Driver 2024 校准 fMRI 参数图][oef] | 校准模型估计的氧摄取与氧代谢 | **数据**：作者声明公开已处理图；需核对文件空间和所需群体产品 |

FDG-PET、ASL 和 BOLD 是测量方法，不是具体图谱名称。静态 FDG 摄取比不等于绝对葡萄糖代谢率；普通 BOLD 也不直接给出 CMRO₂。Driver 参数图有[作者入口][oef-data]，本次未逐文件验证下载内容。

### 9. 血管结构与反应性

| 指标 | 具体资源/入口 | 反映什么 | 空间与获取形式 |
| --- | --- | --- | --- |
| 动脉/静脉分布与区域密度 | [Braincharter vascular atlas][braincharter] | TOF-MRA/SWI 可检出的血管分布 | **图/表**：MNI 模板与区域数据 |
| 动脉出现概率、半径及变异 | [Mouches–Forkert arterial atlas][arterial] | 多中心健康成人的大动脉几何与概率 | **图**：MNI 概率、半径及 SD 等 |
| 血管反应性（CVR）与延迟 | [CVRmap / ds004604][cvr] | 对 CO₂ 挑战的 BOLD 响应及血流动力学延迟 | **数据**：50 名健康成人开放队列与处理结果，按研究目的汇总 |

血管分布图不是毛细血管组织学密度，也不是灌注图；CVR 不是基础 CBF。[Braincharter 原研究][braincharter-paper]、[动脉 atlas 原研究][arterial-paper]、[CVRmap 原研究][cvr-paper]

### 10. 小分子代谢物：MRS 方向

| 指标方向 | 代表研究/资源 | 反映什么 | 本次确认的获取状态 |
| --- | --- | --- | --- |
| NAA、Cho、Cr 等 | [MIDAS/MRSI 正常脑参考研究][mrs] | 谱学估计的区域代谢物浓度或比值 | 已有标准空间参考研究；**本次未确认开放 NIfTI atlas 下载入口** |
| 更广的代谢物组合 | [9.4T、12 代谢物 MNI atlas 研究][mrs94] | 高场 MRSI 的代谢物分布 | 会议研究；未核实公开图文件 |

MRS 可以提供另一类生物化学信息；Glu、Glx 或 GABA 的可测性取决于采集与谱学方法，不能因某研究有多代谢物图，就假定所有代谢物或全脑区域均可用。

### 11. 电生理频谱与时间尺度

| 指标 | 具体资源/入口 | 反映什么 | 空间与获取形式 |
| --- | --- | --- | --- |
| MEG δ/θ/α/β/低γ/高γ 功率 | [HCP / Shafiei MEG 图][meg]；[neuromaps][map-list] | 源定位后不同频段的活动分布 | **图/表**：如 fsLR 4k 表面及分区产品 |
| MEG intrinsic timescale | 同系列 **megtimescale** | 活动自相关所反映的时间尺度 | **图**：fsLR 4k；不是分子或受体密度 |
| iEEG 频谱/状态参考 | [MNI Open iEEG Atlas 原研究][ieeg] | 颅内记录的区域频谱，含清醒/睡眠相关产品 | **数据/表**：有 MNI 电极坐标；患者中筛选的生理性活动，不是健康人全脑均匀采样 |

MEG 有源定位和空间泄漏限制；iEEG 空间覆盖依植入位置。原始 iEEG 资源入口见[官方 atlas][ieeg-data]，公开衍生数据另见 [NEMAR][ieeg-nemar]。

## 四、功能组织、发育与疾病：扩展参考图

这些资源可用于生物学背景解释，但其指标是功能组织、形态变化或疾病差异，不能直接当作分子测量。

| 方向 | 具体资源/入口 | 指标与含义 | 空间与获取形式 |
| --- | --- | --- | --- |
| 功能连接组织 | [Margulies 功能梯度][fcgradient] | 连接模式的连续组织轴 | **图**：如 fsLR 32k；梯度不是受体密度 |
| 形态参照 | [HCP thickness][thickness] | 皮层厚度分布 | **图**：fsLR 32k |
| 发育扩张 | [Hill developmental expansion][hill] | 婴儿到成人的局部皮层面积扩张 | **图**：neuromaps fsLR 164k 原产品仅右半球 |
| 跨物种形态/功能差异 | [Xu alignment 与 expansion][xu] | 人—猕猴对应后的扩张及功能相似性 | **图**：fsLR 32k 原产品仅右半球；不能直接作为进化原因 |
| 脑大小的异速生长 | [Reardon scaling maps][scaling] | 局部面积随总体脑大小变化的比例关系 | **图**：如 CIVET 41k；不等同于年龄增长率 |
| 年龄/性别参考轨迹 | [Brain Charts][braincharts] | MRI 形态指标的群体曲线与百分位 | **模型/表**：开放模型；不是一张适用于所有年龄的固定脑图 |
| Aβ、tau 病理蛋白 | [ADNI PET][adni]等队列 | 示踪剂可结合的病理蛋白沉积 | **数据**：个体 MRI/PET，访问及群体参考构建按队列要求 |
| 疾病结构差异 | [ENIGMA Toolbox][enigma] | 皮层厚度/面积、皮层下体积的病例—对照效应量 | **表**：脑区效应量；不是分子病理图 |

α-synuclein、TDP-43 已有早期人体研究进展，但本次未核实可直接列入的成熟通用公共群体 atlas。相关原研究与进展见 [α-synuclein][alpha-syn]、[TDP-43][tdp]及[人体进展][tdp-human]。

## 补充：研究性图与处理模板

| 资源 | 可获取形式 | 适合怎样理解 |
| --- | --- | --- |
| [GE-179 / NMDA 候选参考图][ge179] | MNI152 分布容积图 | 体内靶点特异性和激活依赖解释存在争议，不宜当作成熟 NMDA 密度图；见[药物挑战研究][ge179-validation]与[后续电刺激研究][ge179-support] |
| [FDOPA SPM 模板][fdopa] | 对称 MNI 归一化模板 | 辅助影像配准；本次未核实其为动力学 Ki 图，不能把模板强度直接当多巴胺合成率 |

## 获取时从哪些入口开始

| 入口 | 适合找什么 |
| --- | --- |
| [neuromaps][map-list] | 已整理的分子、微结构、代谢、电生理与功能/变化参考图 |
| [NiSpace datasets][nispace] | 基因表达、细胞估计、线粒体、PET、BigBrain 和分区数据；需区分作者原图与平台再处理版本 |
| [EBRAINS / siibra][ebrains] | 跨尺度组织学、区域受体特征、显微结构及相关空间参照 |
| [JuSpace][juspace]、[NRU atlases][sv2a] | PET/SPECT 模板集合和特定分子 atlas；逐图查看靶点和指标 |
| [NeuroVault][neurovault]、OpenNeuro、Figshare、Zenodo | 论文配套图或数据；以各行给出的具体项目链接为准 |

## 使用前只需先分清四件事

1. **测到什么**：基因、蛋白、结合参数、MRI 组织代理、功能量或概率标签不能互换。
2. **覆盖哪里**：皮层、皮层下、白质、小脑和局部切片的覆盖不同；另一物种的图不能直接当人脑图。
3. **如何进入 MRI 空间**：MNI 不同版本、fsaverage、fsLR、CIVET 需要正确对应；Schaefer/Glasser 是分区，不是坐标空间。
4. **数据是否独立**：AHBA 衍生图、镜像图及 MRI 模型预测图没有自动增加独立实测样本；空间关联检验还应考虑空间自相关。

图谱最适合帮助提出和比较生物学假设；空间相关本身不证明机制。[空间比较方法][nulls]

> 本文由 AI 辅助检索与整理，尚未经人工专家审定。本次核查了文献、官方产品说明和获取入口，未逐一下载/重建图谱，也未复算原始数据。对 MAO-A/B、AChE、腺苷受体、pH、脑温等方向，本次未核实到可与主表同样明确列出的开放标准空间参考图；这不代表领域中不存在相关资源。

[ahba]: https://brain-map.org/support/documentation/human-brain-atlas-microarray-data-download
[abagen]: https://abagen.readthedocs.io/en/stable/user_guide/expression.html
[magicc]: https://github.com/kwagstyl/MAGICC
[magicc-paper]: https://elifesciences.org/articles/86933
[gryglewski]: https://www.meduniwien.ac.at/neuroimaging/mRNA.html
[gryglewski-paper]: https://pubmed.ncbi.nlm.nih.gov/29723639/
[brainspan]: https://www.brainspan.org/
[gtex]: https://www.gtexportal.org/home/aboutAdultGtex
[gene-pc1]: https://netneurolab.github.io/neuromaps/listofmaps.html#abagen-genepc1-fsaverage-10k
[hmba]: https://alleninstitute.github.io/abc_atlas_access/notebooks/hmba_bg_spatial_genes.html
[hmba-ccf]: https://alleninstitute.github.io/CCF-MAP/descriptions/human_BG_ccf.html
[abc]: https://alleninstitute.github.io/abc_atlas_access/descriptions/WHB-10Xv3.html
[cellmaps]: https://github.com/neuropm-lab/cellmaps
[pak-paper]: https://elifesciences.org/articles/89368
[zhang]: https://github.com/XihanZhang/human-cellular-func-con
[zhang-paper]: https://doi.org/10.1038/s41593-024-01812-2
[nispace]: https://nispace.readthedocs.io/en/latest/datasets.html
[hpa]: https://www.proteinatlas.org/humanproteome/brain
[hpa-paper]: https://pubmed.ncbi.nlm.nih.gov/32139519/
[rcps]: https://github.com/OpenNeuroDatasets/ds004654
[rcps-paper]: https://doi.org/10.1177/0271678X221090997
[hdac]: https://netneurolab.github.io/neuromaps/listofmaps.html#wey2016-martinostat-mni152-2mm
[hdac-paper]: https://pmc.ncbi.nlm.nih.gov/articles/PMC5784409/
[epigenome]: https://pmc.ncbi.nlm.nih.gov/articles/PMC10572106/
[hansen]: https://github.com/netneurolab/hansen_receptors
[hansen-paper]: https://www.nature.com/articles/s41593-022-01186-3
[juspace]: https://github.com/juryxy/JuSpace
[serotonin]: https://pubmed.ncbi.nlm.nih.gov/28053035/
[gaba]: https://www.sciencedirect.com/science/article/pii/S1053811921001555
[vmat2]: https://openneuro.org/datasets/ds002385/versions/1.1.0
[sv2a]: https://xtra.nru.dk/SV2A-atlas/
[sv2a-paper]: https://pubmed.ncbi.nlm.nih.gov/38997157/
[pet-metrics]: https://journals.sagepub.com/doi/pdf/10.1038/sj.jcbfm.9600493
[tspo]: https://neuromaps-main.readthedocs.io/en/latest/listofmaps.html#lois2018-pbr28-mni152-2mm
[tspo-cell]: https://pubmed.ncbi.nlm.nih.gov/31276244/
[tspo-genotype]: https://pubmed.ncbi.nlm.nih.gov/22968319/
[cox1]: https://github.com/OpenNeuroDatasets/ds004401
[cox1-paper]: https://pmc.ncbi.nlm.nih.gov/articles/PMC8261645/
[mitobrain]: https://neurovault.org/collections/16418/
[mitobrain-paper]: https://www.nature.com/articles/s41586-025-08740-6
[julich]: https://julich-brain-atlas.de/atlas/probabilistic-maps
[bigbrainwarp]: https://bigbrainwarp.readthedocs.io/en/latest/pages/toolbox_contents.html
[layers-paper]: https://doi.org/10.1371/journal.pbio.3000678
[nextbrain]: https://github-pages.ucl.ac.uk/NextBrain/
[nextbrain-paper]: https://www.nature.com/articles/s41586-025-09708-2
[receptor-hist]: https://siibra-python.readthedocs.io/en/latest/autoapi/siibra/features/tabular/index.html
[receptor-hist-paper]: https://www.frontiersin.org/journals/neuroanatomy/articles/10.3389/fnana.2017.00078/full
[pli]: https://julich-brain-atlas.de/index.php/atlas/fibre-architecture
[myelin-map]: https://netneurolab.github.io/neuromaps/listofmaps.html#hcps1200-myelinmap-fslr-32k
[ahead]: https://uvaauas.figshare.com/articles/dataset/AHEAD_quantitative_MRI_templates_MNI2009b_/19646364
[ahead-paper]: https://pmc.ncbi.nlm.nih.gov/articles/PMC12319765/
[synthetic]: https://zenodo.org/records/15298434
[synthetic-paper]: https://pmc.ncbi.nlm.nih.gov/articles/PMC12356715/
[mwf]: https://sourceforge.net/projects/myelin-water-atlas/files/
[mwf-paper]: https://pubmed.ncbi.nlm.nih.gov/31347238/
[chiseparation]: https://github.com/SNU-LIST/chi-separation-atlas
[chi-paper]: https://doi.org/10.1002/nbm.5226
[hcp1065]: https://brain.labsolver.org/hcp_template.html
[mre]: https://github.com/mechneurolab/MRE134
[mre-paper]: https://pmc.ncbi.nlm.nih.gov/articles/PMC7670638/
[tract-paper]: https://www.nature.com/articles/s41467-022-32595-4
[metabolism]: https://pubmed.ncbi.nlm.nih.gov/20837536/
[map-list]: https://netneurolab.github.io/neuromaps/listofmaps.html
[oef]: https://pmc.ncbi.nlm.nih.gov/articles/PMC7616461/
[oef-data]: https://owncloud.cubric.cf.ac.uk/s/UtdmuMqU80rVRY7
[braincharter]: https://github.com/braincharter/vasculature/releases
[braincharter-paper]: https://pmc.ncbi.nlm.nih.gov/articles/PMC6866388/
[arterial]: https://springernature.figshare.com/collections/A_statistical_atlas_of_cerebral_arteries_generated_using_multi-center_MRA_datasets_from_healthy_subjects/4215089
[arterial-paper]: https://www.nature.com/articles/s41597-019-0034-5
[cvr]: https://openneuro.org/datasets/ds004604
[cvr-paper]: https://pmc.ncbi.nlm.nih.gov/articles/PMC10973431/
[mrs]: https://pmc.ncbi.nlm.nih.gov/articles/PMC2724718/
[mrs94]: https://archive.ismrm.org/2024/1842_POGXCpQnd.html
[meg]: https://github.com/netneurolab/shafiei_megfmrimapping
[ieeg]: https://pubmed.ncbi.nlm.nih.gov/29506200/
[ieeg-data]: https://mni-open-ieegatlas.research.mcgill.ca/
[ieeg-nemar]: https://www.nemar.org/dataset/nm000362
[fcgradient]: https://netneurolab.github.io/neuromaps/listofmaps.html#margulies2016-fcgradient01-fslr-32k
[thickness]: https://netneurolab.github.io/neuromaps/listofmaps.html#hcps1200-thickness-fslr-32k
[hill]: https://pubmed.ncbi.nlm.nih.gov/20624964/
[xu]: https://pubmed.ncbi.nlm.nih.gov/32916286/
[scaling]: https://pubmed.ncbi.nlm.nih.gov/29853553/
[braincharts]: https://github.com/brainchart/Lifespan
[adni]: https://adni.loni.usc.edu/data-samples/adni-data/neuroimaging/pet/
[enigma]: https://enigma-toolbox.readthedocs.io/en/latest/
[ge179]: https://netneurolab.github.io/neuromaps/listofmaps.html#galovic2021-ge179-mni152-1mm
[ge179-validation]: https://pmc.ncbi.nlm.nih.gov/articles/PMC5894869/
[ge179-support]: https://pmc.ncbi.nlm.nih.gov/articles/PMC8142139/
[fdopa]: https://www.nitrc.org/projects/spmtemplates/
[alpha-syn]: https://www.nature.com/articles/s41467-023-42305-3
[tdp]: https://www.nature.com/articles/s41467-025-64540-6
[tdp-human]: https://ir.acimmune.com/news-releases/news-release-details/ac-immune-presents-first-vivo-images-brain-tdp-43-pathology
[ebrains]: https://www.humanbrainproject.eu/en/science-development/focus-areas/brain-atlases/
[neurovault]: https://www.neurovault.org/
[nulls]: https://netneurolab.github.io/neuromaps/user_guide/nulls.html
