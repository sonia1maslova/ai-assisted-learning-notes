---
ai_assisted: true
review_status: ai_reviewed
last_reviewed: 2026-10-06
---

# Applied Multilevel Models：逐页中文翻译与简要解读

> 原始材料：Ryan W. Walters, PhD，*Applied Multilevel Models*，University of Michigan workshop，2022-11-30。
>
> 整理原则：按原 PDF 页码逐页翻译，并在每页后加入简短解释。解释尽量只帮助理解原页，不额外扩展成完整教材。原课件中个别公式或符号若存在明显不一致，会单独标注“注意”，不静默改写原文。

> 本次核查：已对照[工作坊原始课件][slides]检查主要概念与公式，并统一为 GitHub 支持的公式格式。文中的“核查补充”区别于课件译文；本次是 AI 辅助核查，尚未经人工逐页审定，也未运行配套数据和软件示例。本文以文字整理为主，不完整复刻课件图表。

## 阅读前的符号约定

- Level 1：组内/个体层面，例如学生、患者、同一被试的重复观测。
- Level 2：组层面，例如学校、医生、被试。
- BG（between-group）：组间。
- WG（within-group）：组内。
- fixed effect：固定效应，描述总体平均规律。
- random effect：随机效应，描述各组相对总体规律的偏离及其变异。
- residual / error：课件有时混用；严格地说，模型中的随机误差项常写作 $e$ 或 $\varepsilon$，拟合后得到的具体偏差叫 residual。

---

# Part 1：Introducing that Multilevel Model

## 第 1 页｜封面

### 翻译

**应用多层模型（Applied Multilevel Models）**

为密歇根大学 Institute for Social Research、Population Dynamics and Health Program 准备的工作坊。

讲者：Ryan W. Walters, PhD；日期：2022 年 11 月 30 日。

### 简要解读

本资料是一份应用导向的 multilevel model / mixed-effects model 工作坊课件。

## 第 2 页｜讲者介绍

### 翻译

Ryan W. Walters, PhD；副教授；临床研究副主席；统计与信息学主任；Creighton University，Department of Clinical Research and Public Health。

### 简要解读

本页为讲者信息，无新增统计内容。

## 第 3 页｜Part 1 标题

### 翻译

**第 1 部分（共 12 部分）：引入多层模型。**

### 简要解读

这一部分主要回答：什么是 multilevel model、为什么需要它、它和普通 ANOVA / regression 的核心区别是什么。

## 第 4 页｜什么是多层模型（MLM）？

### 翻译

多层模型有一些近似同义名称：

- Generalized Linear Mixed Model（广义线性混合模型，统计学术语）。“Mixed”表示同时包含固定效应和随机效应。
- Random Coefficient Model（随机系数模型）。随机系数 = 随机效应 = 潜变量。
- Hierarchical Linear Model（分层线性模型，教育学中常见），注意它不是 hierarchical regression（分层回归）。

聚类设计中的 MLM 包括：

- 随机效应 ANOVA；
- 聚类/嵌套观测模型，例如学生嵌套在学校中；
- 交叉分类模型；
- 心理测量模型，例如因子分析和 IRT。

纵向设计中的 MLM 包括：

- 重复测量 ANOVA；
- （潜变量）增长曲线模型；
- 个体内波动模型，例如日记研究。

### 简要解读

MLM 不是某一个单独公式，而是一类能够处理“数据存在层级或重复测量依赖”的模型。课件今天主要关注聚类数据。

## 第 5 页｜任何统计模型都有两面

### 翻译

**均值模型（结构部分）**：

- 对应 fixed effects；
- 是假设检验通常最关注的部分；
- 描述某个观测的期望结果如何随预测变量变化。

**方差模型（随机部分）**：

- 对应 random effects 和 residuals；
- 是我们通常对误差结构做假设的部分；
- 描述误差如何分布在观测、个体或群体之间；
- 这些关系通常称为 dependency（依赖性），这是 MLM 与普通 regression / ANOVA 的主要区别之一。

### 简要解读

理解 MLM 的关键不是只看“均值怎么变”，还要看“变异从哪里来、哪些观测彼此相关”。固定效应主要管平均规律，随机效应和残差主要管方差/依赖结构。

## 第 6 页｜组织模型的两个维度

### 翻译

组织统计模型时可考虑两个维度：

1. outcome 类型：条件正态还是非正态；
2. sampling dimension：一个还是多个抽样层级。

Generalized Linear Model（GLM）：

- 可处理不同条件分布；
- 通过 link function 建模 fixed effects；
- 只有一个 sampling dimension。

Generalized Linear Mixed Model（GLMM）：

- 可处理不同条件分布；
- fixed effects 和 random effects 都进入模型；
- 有多个 sampling dimensions。

注：General Linear Model 是 identity link + normal distribution；最小二乘只适用于 General Linear Model。

### 简要解读

“mixed”关键在于引入随机效应，“generalized”关键在于 outcome 不必是正态连续变量。

### 核查补充

这里的“最小二乘只适用于 General Linear Model”是课件的教学简化。普通最小二乘求解本身不要求误差正态；误差正态主要用于经典有限样本推断。非线性最小二乘也可以拟合非线性均值模型，而部分 GLM 的拟合算法会使用迭代加权最小二乘。因此不能把这句话理解为最小二乘在其他模型中完全不可用。[参考：R 的非线性最小二乘文档][r-nls]、[GLM 拟合文档][r-glm]。

## 第 7 页｜MLM 能做什么？

### 翻译

1. 建模观测之间的依赖性：聚类或交叉分类数据都可以处理。
2. 在任何层级加入预测变量：可以是个体层或组层变量；不仅控制依赖，还能研究依赖为什么存在。
3. 不要求每个组拥有完全相同的数据结构：可以处理不平衡和缺失数据，但有前提条件。
4. 如果已经理解 ANOVA / regression，那么很多基础概念已经具备，例如 intercept、slope 和 variance component。

### 简要解读

MLM 的优势不是“更高级”，而是把层级结构直接写进模型，同时允许不同层级的 predictor 共存。

## 第 8 页｜1. 建模依赖性

### 翻译

依赖性的来源取决于抽样设计产生的变异来源。

- 来自同一个 clustering unit 的 outcome residual 很可能相关，从而违反独立性假设。
- dependency 的层级与 random effects 的层级相对应。
- sampling dimensions 可以嵌套，例如人嵌套在组中。
- 如果没有清晰嵌套结构，可能属于 crossed sampling design，例如儿童居住在不同社区、同时又就读于不同学校。
- 要形成一个随机层级，在加入 fixed effects 后，该层级仍应存在由抽样带来的随机 outcome variation。

### 简要解读

random effect 不是因为“变量看起来像组变量”就必须加入，而是因为这一层级确实产生了未被 fixed effects 解释掉的随机变异。

## 第 9 页｜依赖性是怎样产生的？

### 翻译

依赖性可能来自：

1. 高层级组之间的均值差异：形成相对恒定的组内相关，由 random intercept 表示。
2. 个体层 predictor 的效应在组之间不同：固定效应大小在各组不一致，由 random slope 表示。
3. 组内相关随位置/时间变化但原因未知，例如 AR(1) 自相关结构。对于普通聚类数据，Level-1 个体通常假定可交换，因此这一类结构不一定适用。

### 简要解读

random intercept 允许“基线不同”，random slope 允许“X 对 Y 的效应不同”，残差相关结构则处理 random effects 之外仍存在的相关。

## 第 10 页｜依赖性需要在意吗？

### 翻译

如果方差模型设错了，例如错误地假设观测独立：

- predictor coefficient 的点估计通常可能仍大致可用；
- 但标准误会有偏，从而 p 值也可能有偏。

outcome 的变异来源决定了什么 predictor 最有用：

- Level 2 的组间变异需要组层 predictor；
- Level 1 的组内变异需要组内 predictor。

### 简要解读

忽略聚类结构最直接的问题通常不是回归系数一定错，而是标准误和推断可能错。

### 核查补充

“点估计通常仍可用”还依赖均值模型正确及相应外生性等条件。如果未观测的组层因素与 predictor 相关，系数也可能有偏；加入随机截距本身不会自动消除所有混杂。

## 第 11 页｜2. 在不同分析层级加入 predictor

### 翻译

ANOVA 主要检验离散自变量的组别/条件差异，也可加入连续协变量形成 ANCOVA。

Regression 主要检验 predictor 与 outcome 的 slope 是否不同于 0。

如果 predictor 在 Level 1 个体之间连续变化，而且不能简单用实验条件描述，例如年龄，就需要使用 multilevel modeling framework 来同时处理个体差异与组结构。

### 简要解读

MLM 可以看成 regression 的扩展：仍然估计截距和斜率，但允许这些参数和误差结构存在层级。

## 第 12 页｜谈谈 predictor

### 翻译

- 有些变量在一个 Level-2 group 内恒定，例如某州某年度是否为 right-to-work state。
- 有些变量在同一组内的 Level-1 个体之间变化，例如年龄、出生性别。
- 有些 predictor 只在高层级测量，例如个人是否失业 vs 州失业率。
- 还可以建立跨层级 interaction，例如：年龄的效应是否随着州年中失业率而变化？

### 简要解读

不要只问“这个 predictor 是 Level 1 还是 Level 2”，还要问它的数值在哪个层级发生变化。

## 第 13 页｜3. 各组不需要相同的数据结构

### 翻译

MLM 使用 stacked / long format 数据。

- 含缺失值的行会被排除。
- 示例 outcome 为 Disability，predictors 为 Male 和 Unemployment。
- 若模型只用 Male，则 State 2 中 Male 缺失的 person 4 被排除。
- 若模型只用 Unemployment，则 State 3 因组层失业率缺失而整个州被排除。

### 简要解读

Level-1 predictor 缺失通常影响某一条 observation；Level-2 predictor 缺失可能导致整个 group 都无法进入对应模型。

### 核查补充

这里描述的是示例中常规软件的按行排除行为，不是 MLM 对所有缺失情形的保证。若只有部分重复 outcome 缺失，基于似然的混合模型可以利用其余观测；有效推断通常依赖条件 MAR（随机缺失）、可忽略的缺失机制及模型设定正确等条件。预测变量缺失一般不会由普通混合模型似然自动处理，可能需要多重插补或联合模型；MNAR（非随机缺失）需要进一步建模或敏感性分析。[参考：SAS MIXED 的缺失数据说明][missing-data]。

## 第 14 页｜4. 其实你已经会很多了

### 翻译

如果会 ANOVA / regression，就已经具备理解 multilevel model 的基础。

示例：

```math
\mathrm{Weight}_i = 150 - 2\mathrm{Age}_i + 50\mathrm{Male}_i + e_i
```

需要理解：

- intercept；
- 连续 predictor Age 的 slope；
- 分类 predictor Sex 的 coefficient；
- residual；
- residual variance / variance component。

### 简要解读

混合模型不是推翻普通回归，而是在回归模型上进一步拆分“不同层级的变异”。

---

# Part 2：Statistical Approaches for Clustered Data

## 第 15 页｜Part 2 标题

### 翻译

**第 2 部分：聚类数据的统计处理方法。**

### 简要解读

开始比较用固定效应和随机效应处理组间差异的不同思路。

## 第 16 页｜关于 fixed-effects model 的简短说明

### 翻译

可以用 fixed effects 或 random effects 来“处理”组间相关。

fixed-effects approach：

- 加入 $n_{group}-1$ 个组别 dummy variables；
- 用这些组别 fixed effects 控制抽样/依赖；
- 可以直接推断各组差异。

问题：

- 不能再加入额外 group-level predictor；
- group dummy 已经把组间差异全部吸收；
- 不再剩余 between-group variance。

如果 group 少于约 10 个，有时会考虑 fixed-effects approach，因为随机效应方差在组数太少时估计精度可能不足。

### 简要解读

把 group 当 fixed effect，重点是“每个具体 group 与基准组差多少”；把 group 当 random effect，重点是“group 总体上有多大变异”。

## 第 17 页｜Example Time

### 翻译

进入配套示例：*Example - Fixed Effects.pdf*，介绍工作示例及模型 1–3。

### 简要解读

本页只是跳转到配套示例文件；当前主 PDF 没有展开该示例数据的全部内容。

## 第 18 页｜进入 Multilevel Model

### 翻译

MLM 建立在 ANOVA / regression 框架之上。

- 通过 random effects **量化**组间差异：直接测量 outcome variance 中有多少来自 between-group differences。
- 通过 fixed effects **预测/解释**组间差异：可加入任何层级的 predictor fixed effect。
- random effects 为 dependency 提供可建模的控制方式。

### 简要解读

random effect 回答“还剩多少组间差异”；group-level fixed predictor 回答“这些组间差异能否被某个变量系统解释”。

## 第 19 页｜Multilevel Model 的数据要求

### 翻译

- 同一个 sampling unit 应有多个 outcomes / observations；更多数据通常更好，但边际收益递减。
- 只要选择合适的 link function 和条件 response distribution，各种 measurement scale 都可分析。
- 本课程主要关注 interval scale、条件正态的 outcome。
- 分数在所有 observations 中应保持相同含义，即 measurement invariance，也包括 construct 本身含义的一致性。
- 再复杂的统计模型也无法挽救测量糟糕的变量或研究设计。

### 简要解读

这里的 multiple outcomes 指同一高层级抽样单位内有多条观测：可来自同一个人的重复测量，也可来自同一学校的多个学生；不是说一个模型必须有多个因变量。

## 第 20 页｜Multilevel Data 的推断层级

### 翻译

- Between-group（BG）relationship：Level 2 / group level / 组间差异。
- Within-group（WG）relationship：Level 1 / person level / 组内变异。
- Multilevel model 可以同时研究两类关系。
- 很多 person-level predictors 同时包含 Level-1 和 Level-2 两种变异来源。

### 简要解读

一个 Level-1 predictor $X_{ij}$ 往往既包含“组平均值不同”，也包含“个体相对自己组平均值不同”。两种关系不一定相同，后面中心化部分就是在解决这个问题。

---
# Part 3：Visualizing the Multilevel Model

## 第 21 页｜Part 3 标题

### 翻译

**第 3 部分：多层模型的可视化。**

### 简要解读

这一部分通过图示把“总体均值—组均值—个体观测”的关系拆开。

## 第 22 页｜一个简单的 Between-group Model

### 翻译

模型：

```math
y_j=\beta_0+\beta_1X_j+\beta_2Z_j+\beta_3X_jZ_j+e_j
```

**均值模型：**

- outcome $y_j$ 对每个 group 只测量一次；下标 $j$ 表示 group。
- 每个 group 的期望 outcome 由 $X_j$、 $Z_j$ 及 interaction $X_jZ_j$ 的线性组合决定。
- $\beta_0,\beta_1,\beta_2,\beta_3$ 是 fixed effects，因为它们对样本中的所有 group 都采用同一套系数。

**方差模型：**

- 每个 group 有一个 residual $e_j$。
- 不同 group 的 $e_j$ 假设相互独立、均值为 0、正态分布且方差恒定：

```math
e_j\sim N(0,\sigma_e^2)
```

- 在这个纯 between-group model 中， $\sigma_e^2$ 是唯一的 variance component。

### 简要解读

这仍然是普通回归：一个 group 对应一条 observation，因此还没有“组内重复观测”这一层。

## 第 23 页｜无条件 Between-group Model

### 翻译

无 predictor 时：

```math
y_j=\beta_0+e_j
```

课件示例总体均值为 89.55。某个 group 的观测值为 32，因此它相对总体均值有一个很大的负偏差。

总体标准差为 15.114，因此 residual variance：

```math
\sigma_e^2=(15.114)^2=228.43
```

### 简要解读

“unconditional”表示没有 predictor。此时模型对每个 group 的最佳预测就是总体均值，所有组间差异都塞在 residual 中。

## 第 24 页｜加入组内信息

### 翻译

从完整样本分布转向“3 个 group，每组 5 个人”的结构。记号从：

```math
y_j
```

扩展为：

```math
y_{i,j}
```

其中 $i$ 表示组内个体， $j$ 表示 group。

### 简要解读

一旦一个 group 中有多个 observation，模型就可以区分“组与组不同”和“同一组内部的人不同”。

## 第 25 页｜无条件 Between- & Within-group Model

### 翻译

- 先用所有 observations 的 grand mean 作为最佳猜测，即 fixed intercept $\beta_0$。
- 如果知道一个人属于哪个 group，可以用该 group mean $\beta_{0,j}$ 得到更好的预测。
- group mean 与 grand mean 的差：

```math
\beta_{0,j}-\beta_0
```

称为 random intercept $U_{0,j}$。
- 个体 observation 与其 group mean 的差：

```math
y_{i,j}-\beta_{0,j}
```

称为 residual $e_{i,j}$。

### 简要解读

这是 random-intercept model 最核心的图像：总偏差被拆成“组平均偏离总体平均”以及“个人偏离自己组平均”。

### 核查补充

课件用样本组均值作图帮助理解。实际混合模型中的组特异性截距是潜在参数，估计时通常会向总体均值收缩（部分汇聚）；其预测值不一定等于该组样本均值。组样本较少或组内噪声较大时，通常收缩更多。在不平衡设计中，固定截距估计也不必等于所有观测的简单平均或各组样本均值的简单平均。[参考：lme4 方法论文][lme4-paper]。

## 第 26 页｜总方差的两个来源

### 翻译

 $y_{i,j}$ 的总方差现在有两个 variance components：

1. **between-group variance** $\tau_{U0}^2$：由 group-specific mean 相对 fixed intercept 的偏离产生，对应 random intercepts $U_{0,j}$。
2. **within-group variance** $\sigma_e^2$：由个体 observation 相对自己 group mean 的偏离产生，对应 residuals $e_{i,j}$。

### 简要解读

多层模型并不是凭空增加方差，而是把原本混在一起的总变异拆成两个层级。

## 第 27 页｜六个 group 的数据

### 翻译

图中展示六个 group，各自在不同 Age 值上有 outcome Y。

### 简要解读

每条不同颜色/位置的轨迹代表一个 group。图的重点是直观看到：各组整体水平不同，同时组内也存在波动。

## 第 28 页｜只使用 Between-group Model 看单个 group

### 翻译

如果仍用一个共同均值预测 group $j$ 中所有个体，那么：

```math
e_{i,j}=y_{i,j}-\beta_0
```

这个偏差包含尚未分开的组间与组内变异；“全部变异”描述的是误差结构，并不是一个能与观测值直接相等的数值量。

### 简要解读

此时组间差异和组内差异都被混在同一个 residual 中，因此 residual 承担了过多结构。

## 第 29 页｜对单个 group 拆分 Between 与 Within

### 翻译

- $U_{0,j}$：与 between-group variation 有关；
- $e_{i,j}$：与 within-group variation 有关。

课件强调： $U_{0,j}$ 表示由 group mean differences 带来的 dependency / correlation。

### 简要解读

同一 group 的人共享同一个 $U_{0,j}$，所以他们的 outcome 会天然更相似。这就是 random intercept 产生组内相关的机制。

## 第 30 页｜六个 group 的 Between- & Within-group Model

### 翻译

图中同时显示六组数据、各组自己的平均水平以及组内偏离。

### 简要解读

这页主要把前一页对单个 group 的分解推广到所有 group：每组有自己的随机截距，但仍共享总体 fixed intercept。

## 第 31 页｜无条件 Between- & Within-person Model

### 翻译

总方差包括两个 variance components：

- Level-2 random intercept variance：

```math
\mathrm{Var}(U_{0,j})=\tau_{U0}^2
```

表示 between-group variance； $U_{0,j}$ 是各组相对 fixed intercept 的偏离。

- Level-1 residual variance：

```math
\mathrm{Var}(e_{i,j})=\sigma_e^2
```

表示 within-group variance； $e_{i,j}$ 是个体相对 group mean 的偏离。

### 简要解读

这里开始从“某个具体偏离值”转向“这些偏离在所有组/所有个体中有多大变异”。

---

# Part 4：The Intraclass Correlation

## 第 32 页｜Part 4 标题

### 翻译

**第 4 部分：组内相关系数（Intraclass Correlation, ICC）。**

### 简要解读

ICC 用一个比例描述总方差中有多少属于组间层级。

## 第 33 页｜Multilevel Model 如何处理 dependency

### 翻译

多层模型通过把相关数据中的一部分 residual variance 分离为新的 variance component 来处理 dependency。

注意：

> partitioning variance ≠ explaining variance。

也就是说，把方差拆开不等于解释了方差。只有 predictor variables（fixed effects）才是在解释系统性变异。

### 简要解读

random effect 的第一步是“重新分类变异来源”；加入 predictor 才是在解释为什么这些变异存在。

## 第 34 页｜Empty Means, Random Intercept Model

### 翻译

普通空模型：

```math
y_i=\beta_0+e_i
```

多层空模型：

Level 1：

```math
y_{i,j}=\beta_{0,j}+e_{i,j}
```

Level 2：

```math
\beta_{0,j}=\gamma_{0,0}+U_{0,j}
```

合并后：

```math
y_{i,j}=\gamma_{0,0}+U_{0,j}+e_{i,j}
```

其中：

- fixed intercept $\gamma_{0,0}$：没有 predictor 时，各组均值的总体平均；
- random intercept $U_{0,j}$：组特异性偏离；
- residual $e_{i,j}$：个体相对所属组预测值的偏离。

### 简要解读

这是最基础的 random-intercept model，也是后面所有更复杂模型的骨架。

## 第 35 页｜无条件 ICC

### 翻译

```math
\mathrm{ICC}=\frac{\text{between-group variance}}{\text{between-group variance}+\text{within-group variance}}
```

即：

```math
\mathrm{ICC}=\frac{\tau_{U0}^2}{\tau_{U0}^2+\sigma_e^2}
```

ICC 可理解为：

- 总方差中 between-group variance 的比例；
- 同组个体平均相关程度的一种表达；
- 恒定 group dependency 的 effect size。

ICC 可以大致告诉我们：如果忽略 clustering，可能会有多严重。

### 简要解读

ICC 越大，说明同组个体越相似，group membership 对 outcome 的结构越重要。

### 核查补充

上述公式适用于具有独立、同方差 Level-1 误差的随机截距线性混合模型；在这个设定下，同组任意两个不同观测的相关系数就是该 ICC。随机斜率、额外残差相关或非高斯响应需要相应修改，不能无条件沿用简单公式；第 84 页给出了随机斜率模型的协方差。忽略聚类的影响还与组大小和 predictor 的层级等因素有关。[参考：ICC 与混合模型方差的研究论文][icc-r2]。

## 第 36 页｜大 ICC 与小 ICC

### 翻译

- ICC 较大：random intercept variance 相对 residual variance 更大。
- ICC 较小：residual variance 相对 random intercept variance 更大。

### 简要解读

ICC 是相对比例，不是单独看 $\tau_{U0}^2$ 大不大。

## 第 37 页｜如果 ICC≈0，可以忽略 clustering 吗？

### 翻译

课件认为没有一个 ICC 阈值能够在所有情况下保证“可以安全忽略 clustering”。

原因包括：

- unconditional ICC 和 conditional ICC 会不同；
- conditional 指加入 predictors 后；
- predictor 会改变 variance components，因此也会改变 ICC；
- residual variance 的变化也可能改变 random intercept variance 的估计。

结论：如果数据设计本身是 multilevel，倾向于直接使用 multilevel model。

### 简要解读

ICC 不是一个“一次计算、永久决定模型类型”的绝对门槛。

## 第 38 页｜是否需要 MLM？使用模型比较

### 翻译

检验 ICC 是否大于 0，需要比较模型。

- relative model fit 可用 deviance = $-2LL$ 衡量；越小越好。
- 两种估计方式：ML 和 REML。
- 若用 REML 比较模型，两模型的 fixed predictors 必须相同。
- 显著性可用 likelihood ratio test / deviance difference test：
  1. 计算 $-2\Delta LL$；
  2. 计算参数数量差 $\Delta df$；
  3. 与相应自由度的 $\chi^2$ 分布比较。
- 比较模型时样本量应相同。

### 简要解读

核心思想是：加入 random effect 后，模型是否显著改善拟合；而不是只看某个 ICC 数字。

### 核查补充

比较应使用嵌套模型、同一批观测和可比较的似然；固定效应不同的模型通常要使用 ML，而不能直接比较其 REML 似然。随机效应方差的零值位于参数空间边界，因此“参数差为几就直接用几自由度的普通 $\chi^2$”不是普遍有效的检验。最简单的单一方差分量检验在适用条件下会涉及混合 $\chi^2$ 分布；随机截距加随机斜率及协方差的检验更复杂，可使用相应的边界校正方法或参数自助法。详见 [SAS MIXED 的似然比检验说明][sas-lrt]。

## 第 39 页｜量化 Random Effect Variance

### 翻译

ICC 告诉我们 Level 2 方差占比，但仅知道 random-effect variance 显著并不直观。

课件提出 95% random effects confidence interval（RECI），用于给出大多数 group-specific effects 围绕 fixed effect 的范围。

课件示例：fixed intercept = 1.966，random-intercept variance = 0.005，给出区间约为 [1.827, 2.105]。

### 简要解读

目标是把“方差 0.005”转换成 outcome 原始尺度上更容易解释的 group-specific intercept 范围。

### 注意

原页文字写作：

```math
95\%\ \mathrm{RECI} = \text{fixed effect} \pm 1.96\times \text{random effect variance}
```

但其数值区间 [1.827, 2.105] 实际与使用随机效应**标准差** $\sqrt{0.005}$ 更一致，而不是直接使用 variance 0.005。因此这里应视为课件公式表述与示例计算之间存在不一致；本整理保留原意并明确标注。

### 核查补充

在随机截距服从正态分布的假设下，较合适的组特异性截距分布参考区间是：

```math
\hat\gamma_{0,0}\pm 1.96\sqrt{\hat\tau_{U0}^{2}}
```

代入课件的舍入值可得约 $1.966\pm0.139$，即 $[1.827,2.105]$。它描述估计的组间分布中大约 95% 的截距范围，忽略了总体截距和方差估计的不确定性；它不是固定截距参数的 95% 置信区间，也不是某个具体组截距的置信区间。[对应原课件第 39 页][slides]。

## 第 40 页｜Part 5 标题

### 翻译

**第 5 部分：用矩阵表示模型假设。**

### 简要解读

后面开始把前面的标量公式写成矩阵形式，重点是 $R$、 $G$ 和总体协方差矩阵 $V$。

---
# Part 5：Model Assumptions via Matrices

## 第 41 页｜矩阵形式的 Conditional MLM

### 翻译

标量形式：

```math
y_{i,j}=\beta_0+\beta_1X_j+\beta_2Z_j+\cdots+U_{0,j}+e_{i,j}
```

矩阵形式：

```math
\mathbf Y_j=\mathbf X_j\boldsymbol\beta+\mathbf Z_j\mathbf U_j+\mathbf e_j
```

其中：

- $\mathbf Y_j$：group $j$ 的 outcome 向量；
- $\mathbf X_j$：group $j$ 的 fixed-effect design matrix；
- $\boldsymbol\beta$：fixed-effects vector，不带 group 下标；
- $\mathbf Z_j$：与 random effects 对应的 design matrix；
- $\mathbf U_j$：group $j$ 的 random-effects vector；
- $\mathbf e_j$：group $j$ 的 residual/error 项。

 $X_j$ 和 $Z_j$ 第一列通常都是 1，用来表示 intercept。

### 简要解读

 $X\beta$ 是总体固定规律， $ZU$ 是各 group 对总体规律的随机偏离， $e$ 是剩余误差。 $Z$ 的作用是把每条 observation 与相应 random effect 对应起来。

### 注意

原页把 $\mathbf e_j$ 写成 $n_i\times n_i$ “matrix of residuals”，但从模型维度及后页写法看， $\mathbf e_j$ 应当作为长度为 $n_j$ 的 residual vector；这里很可能是原课件笔误。

## 第 42 页｜矩阵形式的模型假设

### 翻译

条件 outcome 分布：

```math
\mathbf Y_j\mid \mathbf U_j\sim N_{n_j}(\boldsymbol\mu_j,\mathbf R),
\qquad \mathbf R=\sigma_e^2\mathbf I_{n_j}
```

其中 $I_{n_j}$ 是单位矩阵：对角线为 1，非对角线为 0。

Residual assumptions：

```math
\mathbf e_j\sim N_{n_j}(\mathbf 0,\mathbf R)
```

Random-effect assumptions：

```math
\mathbf U_j\sim N_q(\mathbf 0,\mathbf G)
```

### 简要解读

这里有两个 covariance structures： $R$ 描述 observation-level residuals， $G$ 描述 group-level random effects。

### 核查补充

上面的条件均值应明确写为 $\boldsymbol\mu_j=\mathbf X_j\boldsymbol\beta+\mathbf Z_j\mathbf U_j$。标准线性混合模型还假定随机效应与观测层误差独立，不同组的随机效应彼此独立；$\mathbf R=\sigma_e^2\mathbf I_{n_j}$ 是本例的同方差、条件独立误差设定，而不是所有混合模型都必须使用的残差结构。

## 第 43 页｜聚类数据中典型的 R、G 与 V

### 翻译

假设一个 group 有 4 个人，模型只有 random intercept。

Residual covariance matrix：

```math
\mathbf R=\sigma_e^2\mathbf I
```

因此对角线上都是 $\sigma_e^2$，非对角线为 0。

Random-effect covariance structure：

```math
\mathbf G=\tau_{U0}^2
```

总体 outcome covariance matrix：

```math
\mathbf V=\mathbf Z\mathbf G\mathbf Z^T+\mathbf R
```

其对角线为：

```math
\sigma_e^2+\tau_{U0}^2
```

同一 group 中不同 observation 的非对角线 covariance 为：

```math
\tau_{U0}^2
```

只有 random intercept 时， $V$ 具有 compound symmetry；把 $V$ 转成 correlation matrix 后，非对角线对应 ICC。

### 简要解读

这是前面“同组观测共享 random intercept，所以相关”的矩阵表达。真正决定 observed outcomes 彼此 covariance 的是 $V$，它同时包含 random effects 与 residuals 的贡献。

## 第 44 页｜Example Time

### 翻译

配套示例：*Example - Grand-mean-centering.pdf / .xlsx*，Model 1。

### 简要解读

本页为练习/示例跳转，无新增理论内容。

---

# Part 6：Adding Level-2, Group-level Predictors

## 第 45 页｜Part 6 标题

### 翻译

**第 6 部分：加入 Level-2 / group-level predictors。**

### 简要解读

开始研究高层级变量如何解释 random-intercept variance。

## 第 46 页｜Group-level Predictors

### 翻译

组层 predictor 在没有 interaction 时主要作用于 intercept。

- 同一 group 内它的值保持恒定。
- 如果 group-level predictor 缺失，该 group 可能整体被排除（listwise deletion）。

示例数据中 Unemployment 对同一 State 内所有人都是相同值。

### 简要解读

group-level predictor 不能解释同一 group 内“人与人为什么不同”，它解释的是“不同 group 为什么平均水平不同”。

## 第 47 页｜把 Unemployment 作为 Level-2 Predictor

### 翻译

考虑州年中失业率，并以 2% 为中心：

```math
\mathrm{SMue2}_j=\mathrm{Unemployment}_j-2
```

因此 $\mathrm{SMue2}_j=0$ 代表失业率 2%。

Level 1：

```math
y_{i,j}=\beta_{0,j}+e_{i,j}
```

Level 2：

```math
\beta_{0,j}=\gamma_{0,0}+\gamma_{0,1}\mathrm{SMue2}_j+U_{0,j}
```

合并：

```math
y_{i,j}=\gamma_{0,0}+\gamma_{0,1}\mathrm{SMue2}_j+U_{0,j}+e_{i,j}
```

其中：

- $\gamma_{0,0}$：失业率为 2% 的州的预测 outcome；
- $\gamma_{0,1}$：州失业率每高 1 个百分点，group average outcome 的平均差异。

### 简要解读

这是“Level-2 predictor 解释 random intercept”的标准形式：州失业率解释各州平均 outcome 为什么系统性不同， $U_{0,j}$ 则是解释后仍剩余的州间差异。

## 第 48 页｜Level-2 Predictor 解释了多少方差？

### 翻译

可使用 pseudo-$R^2$ 描述 variance component 的减少：

```math
\mathrm{Pseudo}\text{-}R^2_{\tau_{U0}}
=
\frac{\text{random intercept variance}_1-\text{random intercept variance}_2}
{\text{random intercept variance}_1}
```

问题：variance components 可能随着模型变化而重新分配，因此 pseudo-$R^2$ 有时会为负，REML 下更常见。

另一种指标是 Total $R^2$：

1. 只根据 fixed effects 得到 model-predicted outcome；
2. 计算 predicted 与 observed outcome 的 Pearson correlation；
3. 将该相关平方。

### 简要解读

Level-2 predictor 主要应减少 between-group random-intercept variance。pseudo-$R^2$ 比普通线性回归的 $R^2$ 更依赖具体定义。

### 核查补充

这里的 Total $R^2$ 是课件采用的“固定效应预测与观测值的相关平方”，不是混合模型 $R^2$ 的统一定义，也不一般等于基于残差平方和的解释比例。它应与 marginal/conditional $R^2$ 等方差分解指标区分；只含固定截距时，预测值为常数，Pearson 相关无定义。计算前后模型的指标时还需保证观测样本一致。[参考：混合模型的 $R^2$ 与 ICC 定义][icc-r2]。

## 第 49 页｜Example Time

### 翻译

配套 Grand-mean-centering 示例，Models 2a–2b。

### 简要解读

本页为示例跳转。

---

# Part 7：(the complexity of) Adding Level-1, Person-level Predictors

## 第 50 页｜Part 7 标题

### 翻译

**第 7 部分：加入 Level-1 / person-level predictors——它们为什么复杂。**

### 简要解读

这一部分是整份课件非常核心的一段：Level-1 predictor 往往同时包含 within-group 和 between-group 信息。

## 第 51 页｜Level-1 Predictor 的复杂性

### 翻译

Level-1 predictor 往往聚合了两种 variation：

- BG：有些 groups 的 predictor 平均值高于其他 groups；
- WG：同一 group 内有些人 predictor 值高于其他人。

outcome 与 Level-1 predictor 在概念上没有本质区别：一个研究里的 outcome，也可能是另一个研究的 covariate。

可用 predictor 自身的 ICC 描述其 BG/WG variation：

```math
\mathrm{ICC}=\frac{between}{between+within}
```

- ICC > 0：predictor 存在 between-group variation；
- ICC < 1：predictor 存在 within-group variation。

### 简要解读

“Age 是 person-level predictor”不等于 Age 只有 Level-1 information。不同州的平均年龄也可能不同，因此 Age 同时有 Level-2 component。

## 第 52 页｜Between-group vs Within-group Effects

### 翻译

以 SES 与 achievement 为例：

- BG：富裕学生比例更高的学校，平均 achievement 是否更高？
- WG：同一学校内，富裕学生是否比贫困学生 achievement 更高？

同一变量在不同层级的表达尺度还可以不同，例如：

- Level 1：学生 sex，0/1；
- Level 2：学校中 female students 的百分比，0%–100%。

拆分 Level-1 与 Level-2 effects 有两种中心化方案：

- grand-mean-centering；
- group-mean-centering。

### 简要解读

同一个 predictor 的组内效应和组间效应不是同一个科学问题，因此不能默认只有一个 slope。

## 第 53 页｜如何建模 Level-1 Predictor

### 翻译

考虑 people clustered in states，Level-1 predictor 为 $\mathrm{Age}_{i,j}$。

Level-2 / between-group age effect：用州平均年龄表示：

```math
SMage_j=\overline{\mathrm{Age}}_j
```

并可中心化到 65 岁：

```math
\mathrm{SMage65}_j=SMage_j-65
```

Level-1 / within-group effect 的表达依赖中心化方式：

**Grand-mean-centering：**

```math
\mathrm{Age65}_{i,j}=\mathrm{Age}_{i,j}-65
```

它仍保留 WG 和 BG variation。

**Group-mean-centering：**

```math
\mathrm{WSage}_{i,j}=\mathrm{Age}_{i,j}-SMage_j
```

它只保留纯粹 WG variation，相当于减去了 Level-2 age component。

### 简要解读

中心化不只是“让 intercept 好解释”；在 multilevel model 中，它还决定 Level-1 coefficient 到底包含哪些层级的信息。

### 核查补充

课件把减去 65 岁放在 grand-mean-centering 的章节中，但严格说，$\mathrm{Age}-65$ 是**固定参照值中心化**；只有 65 恰好等于所用样本总体平均年龄时，它才是字面意义上的总体均值中心化。减去任何共同常数都保留 WG 和 BG 变异；要分别估计两种关系，仍需同时加入组均值，或使用“组内偏差 + 组均值”的参数化。后文沿用课件章节名称，不代表 65 一定是样本均值。

## 第 54 页｜Level-1 Predictor 包含三种 Effect

### 翻译

1. **Level-1 within-group effect**：一个人的 predictor 高于同组其他人时，他的 outcome 是否也更高？主要对应 Level-1 residual variance。
2. **Level-2 between-group effect**：平均 predictor 更高的 groups 是否也有更高的平均 outcome？主要对应 random-intercept variance。
3. **Level-2 contextual effect**：控制个人 predictor 值后，一个人生活在平均 predictor 更高的 group 中，是否还有额外贡献？它也可理解为 BG effect 与 WG effect 是否不同。

如果 contextual effect = 0，则 BG = WG，课件称之为 convergence。

### 简要解读

三种效应中，任何一种中心化参数化通常只会直接给出其中两种，第三种需要线性组合得到。

---

# Part 8：Grand-mean-centering

## 第 55 页｜Part 8 标题

### 翻译

**第 8 部分：总体均值中心化（Grand-mean-centering）。**

### 简要解读

课件以年龄为例，说明为什么只放一个原始/总体中心化 Level-1 predictor 可能把 BG 与 WG 混在一起。

## 第 56 页｜为什么不能只放一个 Level-1 Predictor？

### 翻译

考虑：

```math
\mathrm{Age65}_{i,j}=\mathrm{Age}_{i,j}-65
```

并只把它放入模型：

```math
y_{i,j}=\beta_{0,j}+\beta_{1,j}\mathrm{Age65}_{i,j}+e_{i,j}
```

Level 2：

```math
\beta_{0,j}=\gamma_{0,0}+U_{0,j}
```

```math
\beta_{1,j}=\gamma_{1,0}
```

由于 $\mathrm{Age65}_{i,j}$ 仍同时包含 BG 与 WG variation，一个 fixed effect $\gamma_{1,0}$ 被迫代表两类关系。课件称其为 combined / smushed / conflated / composite effect，并指出这隐含假设 Level-1 effect = Level-2 effect（convergence）。

### 简要解读

如果 BG 和 WG 真正不同，一个 slope 同时承担两种关系就会造成解释混淆。

## 第 57 页｜单独加入 Level-1 Predictor 的图示

### 翻译

outcome 的 variance 已经被模型拆成 Level 2 BG random-intercept variance 和 Level 1 WG residual variance；但 predictor $\mathrm{Age65}_{i,j}$ 本身没有被拆开，因此只有一个 fixed effect $\gamma_{1,0}$ 同时连接两层 variation。

只要 Level-1 predictor 的 ICC 非零，就可能出现这种情况。由于 Level 1 observations 通常数量更多，combined effect 往往更接近 WG effect。

### 简要解读

outcome 被分层了，但 predictor 没被分层，这就是问题的本质。

## 第 58 页｜Level-1 Predictor 解释的方差

### 翻译

Level-1 predictor 的 fixed main effect / interaction 通常解释 Level-1 residual variance：

```math
\mathrm{Pseudo}\text{-}R^2_{\sigma_e^2}
=
\frac{\text{residual variance}_1-\text{residual variance}_2}
{\text{residual variance}_1}
```

如果 Level-1 predictor 同时保留 Level-1 和 Level-2 variability，它可能同时减少：

- $\sigma_e^2$；
- $\tau_{U0}^2$。

一个单独 predictor 同时降低多个层级的 variance component，可能提示需要拆分该 predictor 的 BG/WG effects。

### 简要解读

这是一个诊断思路：predictor 究竟在解释组内差异、组间差异，还是两者都混在一起？

## 第 59 页｜拆分 Level 1 与 Level 2

### 翻译

要分别估计 within- 与 between-related information，需要同时放入：

- Level-1 $\mathrm{Age65}_{i,j}$；
- Level-2 州平均年龄 $\mathrm{SMage65}_j$。

Level 1：

```math
y_{i,j}=\beta_{0,j}+\beta_{1,j}\mathrm{Age65}_{i,j}+e_{i,j}
```

Level 2：

```math
\beta_{0,j}=\gamma_{0,0}+\gamma_{0,1}\mathrm{SMage65}_j+U_{0,j}
```

```math
\beta_{1,j}=\gamma_{1,0}
```

课件解释：

- $\gamma_{1,0}$：控制州平均年龄后的 unique within-group effect；
- $\gamma_{0,1}$：控制个人年龄后的 contextual / unique Level-2 contribution。

### 简要解读

在 grand-mean-centering 参数化中，加入 group mean 是为了统计控制 Level-1 predictor 中携带的 Level-2 component。

## 第 60 页｜拆分 Level 1 与 Level 2：图示

### 翻译

 $\mathrm{Age65}_{i,j}$ 自身仍含 BG variation，但把 $\mathrm{SMage65}_j$ 一并放入模型后，模型可以把共享的 Level-2 variation 从 Level-1 coefficient 中统计控制掉。

### 简要解读

这里不是把 $\mathrm{Age65}_{i,j}$ 在数据层面直接改成纯 WG 变量，而是通过同时加入 group mean，在回归中得到其“控制 Level 2 后”的 unique WG effect。

---
## 第 61 页｜为什么需要 statistical control？

### 翻译

在 grand-mean-centering 中，Level-1 predictor 仍保留 Level-1 与 Level-2 variation，因此 $\mathrm{Age65}_{i,j}$ 与 $\mathrm{SMage65}_j$ 相关。

普通多元回归中：

```math
y_i=\beta_0+\beta_1X_{1,i}+\beta_2X_{2,i}+e_i
```

如果 $X_1$ 与 $X_2$ 相关，则：

- $\beta_1$ 是控制 $X_2$ 后 $X_1$ 的 unique effect；
- $\beta_2$ 是控制 $X_1$ 后 $X_2$ 的 unique effect。

对应到 grand-mean-centering：

- fixed effect of $\mathrm{Age65}_{i,j}$：控制 $\mathrm{SMage65}_j$ 后的 unique Level-1 / WG effect；
- fixed effect of $\mathrm{SMage65}_j$：控制个人 $\mathrm{Age65}_{i,j}$ 后的 unique Level-2 / contextual effect。

### 简要解读

这里的“control”就是普通多元回归的控制逻辑，并不是 multilevel model 特有的新数学操作。

## 第 62 页｜Grand-mean-centering：三种 effect

### 翻译

课件指出 grand-mean-centering 对 clustered data 很有用，因为它可以直接得到 Level-2 contextual effect。

直接由模型得到：

- Level-1 within-group： $\gamma_{1,0}$；
- Level-2 contextual： $\gamma_{0,1}$。

未直接给出的第三个 effect 是 Level-2 between-group effect，可由：

```math
\mathrm{Between}=\mathrm{Contextual}+\mathrm{Within}
=\gamma_{0,1}+\gamma_{1,0}
```

得到。

可以使用 lincom / ESTIMATE / TEST / contrast1D 等线性组合语句获得缺失的第三个效应，也可以改用 group-mean-centering 直接得到 between-group effect。

### 简要解读

grand-mean-centering 的参数化最自然地回答：组内 effect 是多少，以及 group mean 在控制个体值后是否还有 contextual contribution。

### 注意

原页“Effects not estimated directly”下面的符号排版存在重复/歧义：文字逻辑和后面的公式明确说明，未直接估计的是 between-group effect，而它应由 contextual + within 得到。

## 第 63 页｜Example Time

### 翻译

Grand-mean-centering 配套示例：Age 的 interim analyses，Models 3a–3b。

### 简要解读

本页为示例跳转。

---

# Part 9：Random Effects of Level-1, Person-level Predictors

## 第 64 页｜Part 9 标题

### 翻译

**第 9 部分：Level-1 / person-level predictor 的 random effects。**

### 简要解读

前面主要讨论“平均 slope 是多少”；现在开始问“这个 slope 是否因 group 不同而不同”。

## 第 65 页｜Fixed Effect 与 Random Effect 是两个问题

### 翻译

对于一个 Level-1 predictor，需要分别问：

1. **平均而言，它是否有 effect？**
   - slope 是否非零；
   - fixed effect 是否显著。
2. **这个平均 effect 是否足以描述样本中的所有 groups？**
   - 不同 group 是否需要自己的 slope；
   - random slope variation 是否显著。

### 简要解读

fixed slope 回答“平均关系”；random slope 回答“不同 group 的关系是否异质”。两者不是二选一。

## 第 66 页｜Fixed 与 Random Effect 的四种组合

### 翻译

图中展示四种可能：

A. 无 fixed effect、无 random effect；
B. 有 fixed effect、无 random effect；
C. 无 fixed effect、有 random effect；
D. 有 fixed effect、有 random effect。

粗黑线表示 fixed effect，细黑线表示各 group-specific effects。

### 简要解读

平均 slope 可以接近 0，但不同 group 仍可能有明显正负 slope；反过来也可能有稳定的总体 slope，却几乎没有 group 间 slope variation。

## 第 67 页｜Level-1 Predictor 的 Random Effect

### 翻译

Level 1：

```math
y_{i,j}=\beta_{0,j}+\beta_{1,j}\mathrm{Age65}_{i,j}+e_{i,j}
```

Level 2：

```math
\beta_{0,j}=\gamma_{0,0}+\gamma_{0,1}\mathrm{SMage65}_j+U_{0,j}
```

```math
\beta_{1,j}=\gamma_{1,0}+U_{1,j}
```

其中：

- $\gamma_{0,0}$：固定截距；
- $\gamma_{0,1}$：contextual effect；
- $\gamma_{1,0}$：控制 group mean 后的平均 within-group age effect；
- $U_{0,j}$：group-specific random-intercept deviation，方差 $\tau_{U0}^2$；
- $U_{1,j}$：group-specific random age-slope deviation，方差 $\tau_{U1}^2$；
- 还存在 random intercept 与 random slope 的 covariance $\tau_{U0,U1}$。

### 简要解读

此时每个 group 都有自己的 intercept 和 age slope：

```math
\text{group }j\text{ slope}=\gamma_{1,0}+U_{1,j}
```

## 第 68 页｜Level-1 Age 的 Random Effect 图示

### 翻译

图中用一个具体 group 展示：

- fixed intercept $\gamma_{0,0}=10$；
- group-specific random intercept $U_{0,j}=-4$；
- fixed age slope $\gamma_{1,0}=6$；
- group-specific random slope deviation $U_{1,j}=+2$。

因此这个 group 的实际 intercept 和 slope 都是总体固定值加上自己的 random deviation。

### 简要解读

可以把 random intercept / slope 想成“在 population line 上为每个 group 做自己的上下平移与倾斜修正”。

## 第 69 页｜Random Effect 的进一步说明

### 翻译

random slope variance 放在 $G$ matrix 中。通常 $G$ 使用 unstructured 形式，即估计所有 random-effect variances 与 covariances。

新增 random effect 可通过 likelihood ratio test 比较模型：

- random-intercept model：1 个 random variance component；
- random-intercept + random-age-slope model：random intercept variance、random slope variance、二者 covariance，共 3 个参数；
- 因此该比较中参数差为 2。

若使用 REML，比较模型必须拥有相同 fixed predictors。

random slope variance 也可转为 outcome 尺度上的 random-effects interval 进行解释。

### 简要解读

加入 random slope 不只是“多一个 variance”，通常还会同时增加它与 random intercept 的 covariance 参数。

### 核查补充

这里的“新增 2 个参数”是非结构化随机截距—随机斜率模型的参数计数；它不自动意味着 LRT 可以使用普通 $\chi^2_2$ 参考分布。零斜率方差及相应协方差涉及边界问题，检验方法需按第 38 页补充说明选择。

## 第 70 页｜加入 Random Slope 后如何处理 dependency

### 翻译

加入 random slope 后：

- 一部分原来归入 residual variance 的结构会被划分到 random-slope variance；
- random intercept variance 的含义变为：在 random-slope predictor = 0 时，不同 group 的 intercept variance；
- Level-2 variance structure 中同时包含 random-intercept variance、random-slope variance 以及二者 covariance。

### 简要解读

这就是为什么中心化很重要：predictor 的“0”在哪里，会直接影响 random intercept 的解释。

## 第 71 页｜关于 Random Effects 的进一步评论

### 翻译

课件指出，在 grand-mean-centering 下，random slope 的解释存在一个技术性难点：即使 fixed effects 已经把 age 的 Level-1 与 Level-2 components 拆开，Level-1 age 的 random effect 仍可能对应一个混合/convergence 结构。

从概念上说，若要完全拆开 Level-1 random slope，也应考虑 Level-2 component 的 random effect；但在二层模型中，Level-2 effect 已没有更高一层可供其变化，作者也说明这种模型实际很难估计。

### 简要解读

这是课件自己的方法学提醒，不是理解基础 LMM 的核心。现阶段只需要知道：fixed-effect decomposition 与 random-slope decomposition 并不总是完全对称。

### 核查补充

不要把这一段理解成“组层效应必须在二层模型中再加一个随机斜率”。改变中心化会改变随机截距的参照点及随机截距—随机斜率协方差结构；保留相同固定效应并不保证不同随机结构下的模型等价。这是作者在该课件设定中的提醒，具体随机结构仍应由设计、组内变异和可识别性决定。

## 第 72 页｜Example Time

### 翻译

Grand-mean-centering 配套示例：Models 3c–3d。

### 简要解读

本页为示例跳转。

---

# Part 10：Explaining Random Slope Variance

## 第 73 页｜Part 10 标题

### 翻译

**第 10 部分：解释 Random Slope Variance。**

### 简要解读

既然不同 group 的 slope 不同，下一步自然要问：什么 Level-2 variable 能解释这些 slope differences？

## 第 74 页｜解释 Random Slope Variance

### 翻译

random effects 表示 Level-2 between-group differences，因此 random-effect variances 只能由 Level-2 variables 来解释。

- Level-2 main effects / interactions 可以解释 random-intercept variance。
- random-slope variance 要通过 fixed cross-level interaction 来解释，即 Level-2 variable × random Level-1 predictor。

可用 pseudo-$R^2$ 表示 random-slope variance 的减少：

```math
\mathrm{Pseudo}\text{-}R^2_{\tau_{U1}}
=
\frac{\text{random slope variance}_1-\text{random slope variance}_2}
{\text{random slope variance}_1}
```

### 简要解读

random slope 告诉我们“不同 group 的 slope 不同”；cross-level interaction 尝试解释“为什么不同”。

## 第 75 页｜涉及 Level-1 Predictor 的 Interaction

### 翻译

在 grand-mean-centering 下，Level-1 variable 同时含 WG 与 BG variability，因此 interaction 也必须考虑这种混合结构。

示例：Level-2 state unemployment 是否调节 Level-1 person age effect。

如果关注：

```math
\mathrm{SMue2}_j\times \mathrm{Age65}_{i,j}
```

课件提醒，不应忽略对应的 group-mean age × unemployment interaction，因为 age 的 WG 与 BG components 彼此相关。

### 简要解读

主效应如果需要拆 Level 1 / Level 2，interaction 往往也需要相应地拆，不能只拆主效应却让 interaction 又把两层信息混回去。

## 第 76 页｜Example Time

### 翻译

Grand-mean-centering 配套示例：Models 4a–4b。

### 简要解读

本页为示例跳转。

---

# Part 11：Group-mean-centering

## 第 77 页｜Part 11 标题

### 翻译

**第 11 部分：组均值中心化（Group-mean-centering）。**

### 简要解读

与 grand-mean-centering 不同，这种方法直接在变量层面把 Level-1 predictor 分成纯 WG 与纯 BG 两部分。

## 第 78 页｜Group-mean-centering 的定义

### 翻译

Group-mean-centering 把 Level-1 predictor 分解成两个 variables，分别直接代表 BG 与 WG sources of variation。

以 Age 为例：

Level-2 group-mean predictor：

```math
\mathrm{SMage65}_j=\overline{\mathrm{Age}}_j-65
```

Level-1 within-group predictor：

```math
\mathrm{WSage}_{i,j}=\mathrm{Age65}_{i,j}-\mathrm{SMage65}_j
```

即个体年龄相对自己州平均年龄的 deviation。

- $\mathrm{WSage}>0$：比所在州平均年龄更大；
- $\mathrm{WSage}<0$：比所在州平均年龄更小。

### 简要解读

这里的中心不是一个固定常数，而是每个 group 自己的 mean，因此得到的 $\mathrm{WSage}$ 在每个 group 内平均为 0。

## 第 79 页｜Group-mean-centering 的模型

### 翻译

通过两个 predictors 分别表示 within 与 between：

Level 1：

```math
y_{i,j}=\beta_{0,j}+\beta_{1,j}\mathrm{WSage}_{i,j}+e_{i,j}
```

Level 2：

```math
\beta_{0,j}=\gamma_{0,0}+\gamma_{0,1}\mathrm{SMage65}_j+U_{0,j}
```

```math
\beta_{1,j}=\gamma_{1,0}
```

此时：

- $\mathrm{WSage}$ 只包含 within-group variation；
- $\mathrm{SMage65}$ 只包含 between-group variation；
- 二者不相关，因此各自 coefficient 可以直接表示各自层级的 total effect。

 $\gamma_{1,0}$：within-group age effect；
 $\gamma_{0,1}$：between-group mean-age effect。

### 简要解读

这比 grand-mean-centering 更“显式”：不是靠统计控制来分离，而是在 predictor 构造时就直接拆开。

## 第 80 页｜拆分 Level 1 与 Level 2：Group-mean-centering 图示

### 翻译

模型一边把 outcome variance 分成 Level-2 random-intercept variance 和 Level-1 residual variance；另一边也把 Age predictor 强制拆成：

- Level-2 group-mean variation $\mathrm{SMage65}_j$；
- Level-1 within-group deviation $\mathrm{WSage}_{i,j}$。

因为 $\mathrm{WSage}$ 不含 BG variance，所以无需额外 statistical control 来从中剥离 Level-2 component。

课件认为这种参数化更不容易产生解释错误。

### 简要解读

一句话：grand-mean-centering 是“同时放入个人值和 group mean 后统计拆分”；group-mean-centering 是“先把个人值减去 group mean，再直接得到纯 WG predictor”。

---
## 第 81 页｜Group-mean-centering：为什么不需要额外 statistical control

### 翻译

在 group-mean-centering 中，Level-1 variable 只包含 Level-1 information。

 $\mathrm{WSage}_{i,j}$ 与 $\mathrm{SMage65}_j$ 的相关为 0；课件进一步指出， $\mathrm{WSage}_{i,j}$ 与所有 Level-2 variables 都不相关。

回到普通多元回归：

```math
y_i=\beta_0+\beta_1X_{1,i}+\beta_2X_{2,i}+e_i
```

如果 $X_1$ 与 $X_2$ 不相关，那么一个 predictor 的 coefficient 不需要通过另一个 predictor 来“剥离”共享变异。

因此 group-mean-centering 可直接得到：

- WG： $\mathrm{WSage}_{i,j}$ 的 fixed effect；
- BG： $\mathrm{SMage65}_j$ 的 fixed effect。

### 简要解读

由于 within-group deviation 在每个 group 内总和为 0，它与任何只在 group 层变化的变量正交，因此 Level-1 和 Level-2 information 被结构性分开。

### 核查补充

这个零协方差结论针对用**同一分析样本**计算组均值的、未加权的组内偏差；还要求变量有非零方差才能讨论相关系数。如果先用全体样本求组均值、再因其他变量缺失删掉部分观测，或使用不匹配的权重，保留样本中的组内偏差和未必仍为 0。这里的 WG/BG “effect”是模型中的条件关联，不会仅因中心化而成为因果效应。

## 第 82 页｜Group-mean-centering：三种 effect

### 翻译

模型直接给出：

- Level-1 within-group effect： $\gamma_{1,0}$；
- Level-2 between-group effect： $\gamma_{0,1}$。

未直接给出的是 contextual effect，可由：

```math
\mathrm{Contextual}=\mathrm{Between}-\mathrm{Within}
=\gamma_{0,1}-\gamma_{1,0}
```

得到。

可以通过 lincom / ESTIMATE / TEST / contrast1D 得到该线性组合；也可以改用 grand-mean-centering，让 contextual effect 成为直接系数。

### 简要解读

两种中心化不是谁“更正确”，而是直接参数化不同：

- grand-mean-centering：直接给 WG + contextual；
- group-mean-centering：直接给 WG + BG。

### 注意

原页在“Effects not given directly”下的符号排版同样有重复，真正未直接给出的量由后面的公式清楚定义为 contextual = between − within。

## 第 83 页｜Group-mean-centering 下的 Random Level-1 Effect

### 翻译

Level 1：

```math
y_{i,j}=\beta_{0,j}+\beta_{1,j}\mathrm{WSage}_{i,j}+e_{i,j}
```

Level 2：

```math
\beta_{0,j}=\gamma_{0,0}+\gamma_{0,1}\mathrm{SMage65}_j+U_{0,j}
```

```math
\beta_{1,j}=\gamma_{1,0}+U_{1,j}
```

其中：

- $\gamma_{0,1}$：平均年龄更高的州与平均 outcome 的 BG 关系；
- $\gamma_{1,0}$：同州内部“比本州平均年龄更大”的 WG effect；
- $U_{0,j}$：random intercept；
- $U_{1,j}$：random within-group age slope；
- 还估计 random intercept 与 random slope 的 covariance。

### 简要解读

group-mean-centering 后 random slope 的含义更清楚：它描述“纯粹的 within-group slope 是否在不同 groups 中变化”。

## 第 84 页｜Random Slopes

### 翻译

random slope variance 进入 unstructured $G$ matrix：

```math
G=
\begin{bmatrix}
\tau_{U0}^2 & \tau_{U0,U1}\\
\tau_{U1,U0} & \tau_{U1}^2
\end{bmatrix}
```

新增 random effects 通过 likelihood ratio test 检验；使用 REML 时，比较模型必须拥有相同 predictors。

random-slope variation 可以用 95% random-effects interval 在 outcome/slope 原始尺度上进行描述。

加入 random slopes 后，pseudo-$R^2$ 的基线也应重新设定。

### 简要解读

一旦 random-effect structure 改变，各 variance components 的定义也随之改变，所以比较“解释了多少方差”时不能机械沿用加入 random slope 之前的基线。

### 核查补充

LRT 的边界问题参见第 38、69 页；random-effects interval 的含义参见第 39 页。加入随机斜率后，同组两条观测的协方差会随 predictor 值变化，不能再用一个固定 ICC 概括所有配对的相关性：

```math
\mathrm{Cov}(y_{i,j},y_{k,j}\mid\mathbf X_j)
=\tau_{U0}^2+(x_{i,j}+x_{k,j})\tau_{U0,U1}
+x_{i,j}x_{k,j}\tau_{U1}^2,\qquad i\ne k
```

这里假定观测层误差彼此独立，$x$ 为随机斜率所对应的 predictor；相关系数还需除以两条观测各自条件于预测变量的标准差。

## 第 85 页｜解释 Random Slope Variance

### 翻译

由于 random effects 表示 Level-2 differences：

- Level-2 main effect 可以解释 random-intercept variance；
- Level-2 × Level-1 cross-level interaction 可以解释 random-slope variance。

可比较加入 interaction 前后的 random slope variance，计算 pseudo-$R^2$。

### 简要解读

逻辑是：先发现“不同 group 的 slope 不一样”，再用 group-level characteristic 去解释这些 slope differences。

## 第 86 页｜Group-mean-centering 下的 Cross-level Interaction

### 翻译

在 group-mean-centering 下，Level-1 variable 只含 WG variation，因此 interactions 相对更简单。

示例：州失业率 $\mathrm{SMue2}_j$ 是否调节个人相对州平均年龄 $\mathrm{WSage}_{i,j}$ 的 effect：

```math
\mathrm{SMue2}_j\times \mathrm{WSage}_{i,j}
```

表示：不同州失业率下，WG age effect 是否不同。

课件指出，此时可以在技术上不加入 $SMage_j\times \mathrm{SMue2}_j$，因为 WG 与 BG age 已经分离；但从理论上是否遗漏 BG interaction，仍需由研究问题决定。

### 简要解读

group-mean-centering 最大的便利之一，就是 cross-level interaction 的含义更直接。

## 第 87 页｜Example Time

### 翻译

Group-mean-centering 配套示例：Models 3a–4b。课件说明 Models 1–2b 与前面的 group-mean-centering 设定一致。

### 简要解读

本页为示例跳转。

---

# Part 12：Overarching Summary and Model Building Advice

## 第 88 页｜Part 12 标题

### 翻译

**第 12 部分：总体总结与模型构建建议。**

### 简要解读

最后三页把整份课件的建模顺序压缩成实操流程。

## 第 89 页｜总体总结

### 翻译

对于 clustered data，multilevel models 可分为：

- empty model；
- conditional model。

在 two-level model 中，Level-1 predictor 至少包含两种 effect：

- Level-2 BG：有些 groups 的 predictor 平均更高/更低；
- Level-1 WG：同一 group 内有些人高于/低于其他人。

BG 与 WG effects 通常需要两个或更多参数表示，可以通过：

- group-mean-centering：直接问 WG 是否 $\neq0$、BG 是否 $\neq0$；
- grand-mean-centering：直接问 WG 是否 $\neq0$、BG 是否与 WG 不同（contextual effect）。

课件认为，对 clustered data 而言，若研究兴趣集中在 contextual effect，grand-mean-centering 往往更有吸引力。

### 简要解读

这页强调全课件最重要的观点：Level-1 predictor 的“一个 coefficient”往往不够，必须区分它的组内和组间含义。

## 第 90 页｜Model Building Strategies

### 翻译

建议的 bottom-up 流程：

1. 计算 ICC，并考虑 fixed intercept 周围的 random-effect interval。
2. 加入 Level-2 / group-level predictors：
   - 用 p 值评估 fixed effects；
   - 计算 pseudo-$R^2$ 或 total $R^2$。
3. 加入 Level-1 / person-level predictors：
   - 先看 predictor 自身 ICC；
   - 若 ICC > 0，用 grand-mean-centering 或 group-mean-centering 拆分 fixed effects；
   - 检验显著性；
   - 明确区分 WG、BG、contextual interpretations。
4. 评估 Level-1 predictor 的 random slopes：
   - 用 likelihood ratio test 判断是否需要 random slope；
   - 描述 random slope variation；
   - 用 cross-level interactions 解释 random slope variance；
   - 再计算相应 pseudo-$R^2$ / total $R^2$。

### 简要解读

这页可以直接当作整份课件的“建模路线图”。

## 第 91 页｜Model-Building Strategies – Part Deux

### 翻译

本工作坊采用 bottom-up model-building approach。

- 可以先分别检查 predictor effects，例如：age 是否有作用？
- 再分层组合 predictors，考察 unique contribution 和 interactions，例如：控制 sex 后 age 是否仍然有作用？
- predictor 进入模型的顺序应由理论和研究问题指导。
- 未必存在唯一的“最佳模型”。
- 对一个研究者而言是 control variable 的东西，对另一个研究者可能正是核心研究问题。
- predictor 加入顺序不同，最后可能得到不同的模型路径。

### 简要解读

统计模型的构建不能只靠自动筛选。层级结构、中心化方式、random-effect structure 和 predictor 顺序都应由研究问题与设计共同决定。

---

# 一页式复习框架

整份 PDF 可以压缩为下面这条逻辑链：

1. **普通回归假设 observations 独立；多层数据往往不独立。**
2. **random intercept** 把总方差拆成 between-group 与 within-group 两部分。
3. **ICC** 描述总方差中有多少来自 between-group differences。
4. **Level-2 predictors** 用 fixed effects 解释 random-intercept variance。
5. **Level-1 predictors** 常同时含 WG 和 BG information，不能默认一个 slope 就足够。
6. **Grand-mean-centering** 与 **group-mean-centering** 是拆分 WG/BG/contextual effects 的两种参数化方式。
7. **Random slope** 检验 Level-1 effect 是否在不同 groups 中变化。
8. **Cross-level interaction** 尝试解释为什么不同 groups 的 slope 不一样。
9. 模型构建可从 empty random-intercept model 出发，再逐步加入 Level-2 predictors、Level-1 predictors、centering、random slopes 和 interactions。

## 最核心的几个公式

### Random-intercept empty model

```math
y_{i,j}=\gamma_{0,0}+U_{0,j}+e_{i,j}
```

### ICC

```math
\mathrm{ICC}=\frac{\tau_{U0}^2}{\tau_{U0}^2+\sigma_e^2}
```

### Random intercept + random slope

```math
y_{i,j}=(\gamma_{0,0}+U_{0,j})+(\gamma_{1,0}+U_{1,j})X_{i,j}+e_{i,j}
```

### Group-mean decomposition

```math
X_{i,j}=\overline X_j+(X_{i,j}-\overline X_j)
```

其中：

- $\overline X_j$：between-group information；
- $X_{i,j}-\overline X_j$：within-group information。

### Matrix form

```math
\mathbf Y=\mathbf X\boldsymbol\beta+\mathbf Z\mathbf U+\mathbf e
```

```math
\mathrm{Var}(\mathbf U)=\mathbf G,
\qquad
\mathrm{Var}(\mathbf e)=\mathbf R,
\qquad
\mathrm{Var}(\mathbf Y)=\mathbf V=\mathbf Z\mathbf G\mathbf Z^T+\mathbf R
```

---

# 建议的复习顺序

如果后续要真正把这份课件学懂，建议按以下顺序回看：

1. 第 25–35 页：random intercept、variance decomposition、ICC；
2. 第 41–43 页：矩阵形式中的 $G$、 $R$、 $V$；
3. 第 51–54 页：为什么 Level-1 predictor 同时包含 BG / WG information；
4. 第 56–62 页：grand-mean-centering；
5. 第 78–82 页：group-mean-centering；
6. 第 65–70、83–86 页：random slope 与 cross-level interaction；
7. 第 90–91 页：完整 model-building workflow。

---

# 核查来源与适用范围

- [Ryan W. Walters：Applied Multilevel Models 原始课件（91 页）][slides]；[工作坊介绍与配套材料][workshop]。
- [SAS MIXED：混合模型理论与似然比检验][sas-lrt]；[lme4：模型比较与 REML/ML][lme4-compare]。
- [lme4：模型拟合和缺失值处理][lmer-doc]；[SAS MIXED 官方说明][missing-data]。
- [R：非线性最小二乘][r-nls]；[R：GLM 拟合][r-glm]。
- [Bates 等（2015）：Fitting Linear Mixed-Effects Models Using lme4][lme4-paper]。
- [Nakagawa、Johnson 与 Schielzeth（2017）：混合模型的 $R^2$ 与 ICC][icc-r2]。

上述来源用于核查主要统计表述；配套数据、软件例程和全部示例结果未重新运行。课件建议的建模顺序是应用示范，不应把显著性筛选或 ICC 阈值当作所有研究的固定规则。

[slides]: https://pdhp.isr.umich.edu/wp-content/uploads/2022/11/Lecture-Applied-Multilevel-Models.pdf
[workshop]: https://pdhp.isr.umich.edu/workshops/applied-multilevel-models/
[sas-lrt]: https://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/statug_mixed_details01.htm
[lme4-compare]: https://lme4.github.io/lme4/reference/merMod-class.html
[lmer-doc]: https://lme4.github.io/lme4/reference/lmer.html
[missing-data]: https://documentation.sas.com/api/docsets/statug/15.1/content/mixed.pdf?locale=en
[r-nls]: https://stat.ethz.ch/R-manual/R-devel/library/stats/html/nls.html
[r-glm]: https://stat.ethz.ch/R-manual/R-devel/library/stats/html/glm.html
[lme4-paper]: https://lme4.github.io/lme4/articles/lmer.pdf
[icc-r2]: https://doi.org/10.1098/rsif.2017.0213
