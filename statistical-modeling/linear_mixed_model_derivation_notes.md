# 线性混合效应模型中的公式推导：从随机截距到似然函数

本文从最简单的随机截距线性混合效应模型出发，逐步推导：

- 随机截距模型的基本结构
- 随机截距与残差的分布假设
- 单个观测的期望与方差
- 同组观测之间为什么会有协方差
- ICC 与随机截距方差的关系
- 方差—协方差矩阵 $V$ 的来源
- 一般矩阵形式 $Y=X\beta+Zu+\varepsilon$
- 为什么 $V=ZGZ^\top+R$
- 为什么 $Y\sim N(X\beta,V)$
- 多元正态密度如何变成似然函数
- 为什么要取对数得到 log-likelihood
- GLS 固定效应估计公式的来源
- 随机效应方差如何通过 ML / REML 估计
- 每个 group 的随机截距如何通过 BLUP 得到
- shrinkage / partial pooling 的来源

---

## 1. 从最简单的随机截距模型开始

最简单的随机截距模型写作：

```math
Y_{ij}=\beta_0+u_j+\varepsilon_{ij}
```

其中：

- $i$：第 $j$ 个 group 内的第 $i$ 个 observation；
- $j$：group 的编号；
- $Y_{ij}$：第 $j$ 个 group 中第 $i$ 个 observation；
- $\beta_0$：所有 group 共享的总体截距；
- $u_j$：第 $j$ 个 group 相对于总体截距的额外偏移，即随机截距；
- $\varepsilon_{ij}$：第 $j$ 个 group 中第 $i$ 个 observation 自身的残差。

因此，第 $j$ 个 group 自己的截距为：

```math
\beta_0+u_j
```

这就是“随机截距”的基本含义。

---

## 2. 随机截距和残差的分布假设

通常假设：

```math
u_j\sim N(0,\sigma_u^2)
```

以及：

```math
\varepsilon_{ij}\sim N(0,\sigma_\varepsilon^2)
```

还通常假设不同 group 的随机截距彼此独立，且随机截距与所有 residual 独立；最简单的随机截距模型还假设 residual 之间彼此独立。

符号

```math
\sim
```

表示“服从……分布”。

所以：

```math
u_j\sim N(0,\sigma_u^2)
```

表示：

- 所有 group 的随机截距围绕 0 分布；
- 随机截距之间的总体差异由 $\sigma_u^2$ 描述。

其中：

```math
\sigma_u^2=\mathrm{Var}(u_j)
```

可以理解为：

> group 之间的基线差异有多大。

而：

```math
\sigma_\varepsilon^2=\mathrm{Var}(\varepsilon_{ij})
```

可以理解为：

> 在同一个 group 内，每个 observation 围绕该 group 的理论值上下波动有多大。

之所以令：

```math
E(u_j)=0
```

是因为总体平均水平已经由 $\beta_0$ 表示，$u_j$ 只负责描述每个 group 相对总体均值的偏移。

---

# 3. 单个 observation 的期望

从：

```math
Y_{ij}=\beta_0+u_j+\varepsilon_{ij}
```

两边取期望：

```math
E(Y_{ij})
=
E(\beta_0+u_j+\varepsilon_{ij})
```

利用期望的线性性质：

```math
E(Y_{ij})
=
\beta_0+E(u_j)+E(\varepsilon_{ij})
```

因为：

```math
E(u_j)=0
```

且：

```math
E(\varepsilon_{ij})=0
```

所以：

```math
\boxed{
E(Y_{ij})=\beta_0
}
```

也就是说，从整个 group population 的角度看，一个 observation 的总体期望就是总体截距 $\beta_0$。

---

# 4. 单个 observation 的方差

仍然从：

```math
Y_{ij}=\beta_0+u_j+\varepsilon_{ij}
```

出发。

由于 $\beta_0$ 是常数：

```math
\mathrm{Var}(\beta_0)=0
```

因此：

```math
\mathrm{Var}(Y_{ij})
=
\mathrm{Var}(u_j+\varepsilon_{ij})
```

使用：

```math
\mathrm{Var}(X+Y)
=
\mathrm{Var}(X)
+
\mathrm{Var}(Y)
+
2\mathrm{Cov}(X,Y)
```

得到：

```math
\mathrm{Var}(Y_{ij})
=
\mathrm{Var}(u_j)
+
\mathrm{Var}(\varepsilon_{ij})
+
2\mathrm{Cov}(u_j,\varepsilon_{ij})
```

随机截距与 residual 通常假设独立：

```math
\mathrm{Cov}(u_j,\varepsilon_{ij})=0
```

因此：

```math
\boxed{
\mathrm{Var}(Y_{ij})
=
\sigma_u^2+\sigma_\varepsilon^2
}
```

也就是说：

```math
\boxed{
\text{总变异}
=
\text{group-level 变异}
+
\text{observation-level 变异}
}
```

---

# 5. 同一个 group 的两个 observation 为什么会相关？

考虑同一个 group $j$ 中两个 observation：

```math
Y_{1j}
=
\beta_0+u_j+\varepsilon_{1j}
```

```math
Y_{2j}
=
\beta_0+u_j+\varepsilon_{2j}
```

它们都共享同一个：

```math
u_j
```

所以当某个 group 的 $u_j$ 较高时：

```math
Y_{1j}
```

和：

```math
Y_{2j}
```

都会被同时往上推。

当某个 group 的 $u_j$ 较低时，它们又会一起被往下拉。

因此，同一 group 内的 observation 会产生相关性。

---

# 6. $Y_{1j}$ 和 $Y_{2j}$ 中的 $j$ 到底是什么意思？

这里：

```math
Y_{1j}
```

表示第 $j$ 个 group 的第 1 个 observation，

而：

```math
Y_{2j}
```

表示同一个第 $j$ 个 group 的第 2 个 observation。

所以一对里面的 $j$ 一定相同。

例如：

```math
(Y_{11},Y_{21})
```

来自 Group 1；

```math
(Y_{12},Y_{22})
```

来自 Group 2；

```math
(Y_{13},Y_{23})
```

来自 Group 3。

如果把很多 group 排成表：

| Group $j$ | $Y_{1j}$ | $Y_{2j}$ |
|---|---:|---:|
| 1 | $Y_{11}$ | $Y_{21}$ |
| 2 | $Y_{12}$ | $Y_{22}$ |
| 3 | $Y_{13}$ | $Y_{23}$ |
| ... | ... | ... |

那么可以把它直观理解成两列配对数据：

```math
Y_{11},Y_{12},Y_{13},\ldots
```

和：

```math
Y_{21},Y_{22},Y_{23},\ldots
```

每一行都来自同一个 group。

因此：

> $j$ 在每一对内部相同，但在不同 pair 之间变化。

---

# 7. 为什么同组两个随机变量的协方差等于 $\sigma_u^2$？

计算：

```math
\mathrm{Cov}(Y_{1j},Y_{2j})
```

代入：

```math
Y_{1j}=\beta_0+u_j+\varepsilon_{1j}
```

```math
Y_{2j}=\beta_0+u_j+\varepsilon_{2j}
```

因为常数 $\beta_0$ 不影响协方差：

```math
\mathrm{Cov}(Y_{1j},Y_{2j})
=
\mathrm{Cov}
(
u_j+\varepsilon_{1j},
u_j+\varepsilon_{2j}
)
```

---

## 7.1 为什么协方差可以展开成四项？

一般地：

```math
\mathrm{Cov}(A+B,C+D)
```

可以展开为：

```math
\mathrm{Cov}(A,C)
+
\mathrm{Cov}(A,D)
+
\mathrm{Cov}(B,C)
+
\mathrm{Cov}(B,D)
```

其结构与普通代数展开：

```math
(A+B)(C+D)
=
AC+AD+BC+BD
```

非常类似。

因此：

```math
\mathrm{Cov}
(
u_j+\varepsilon_{1j},
u_j+\varepsilon_{2j}
)
```

展开为：

```math
\mathrm{Cov}(u_j,u_j)
```

```math
+
\mathrm{Cov}(u_j,\varepsilon_{2j})
```

```math
+
\mathrm{Cov}(\varepsilon_{1j},u_j)
```

```math
+
\mathrm{Cov}(\varepsilon_{1j},\varepsilon_{2j})
```

---

## 7.2 为什么只剩第一项？

随机截距模型通常假设：

```math
u_j\perp\varepsilon_{ij}
```

所以：

```math
\mathrm{Cov}(u_j,\varepsilon_{2j})=0
```

以及：

```math
\mathrm{Cov}(\varepsilon_{1j},u_j)=0
```

同时，在最简单的模型中，不同 observation 的 residual 相互独立：

```math
\mathrm{Cov}(\varepsilon_{1j},\varepsilon_{2j})=0
```

于是只剩：

```math
\mathrm{Cov}(u_j,u_j)
```

而一个随机变量和自己的协方差就是它自己的方差：

```math
\mathrm{Cov}(u_j,u_j)
=
\mathrm{Var}(u_j)
```

所以：

```math
\boxed{
\mathrm{Cov}(Y_{1j},Y_{2j})
=
\sigma_u^2
}
```

直观上：

> 两个 observation 真正共同拥有的随机成分只有 $u_j$，因此它们共同变化的那一部分，正是随机截距的变异。

---

# 8. “边际协方差”是什么意思？

这里需要区分：

```math
\mathrm{Cov}(Y_{1j},Y_{2j}\mid u_j)
```

和：

```math
\mathrm{Cov}(Y_{1j},Y_{2j})
```

如果已经固定了某个具体 group 的 $u_j$，那么：

```math
Y_{1j}
=
\beta_0+u_j+\varepsilon_{1j}
```

```math
Y_{2j}
=
\beta_0+u_j+\varepsilon_{2j}
```

此时：

```math
\beta_0+u_j
```

都是常数。

如果 residual 独立，那么：

```math
\boxed{
\mathrm{Cov}(Y_{1j},Y_{2j}\mid u_j)=0
}
```

但如果不固定 $u_j$，而是把：

```math
u_j\sim N(0,\sigma_u^2)
```

的全部可能性都考虑进去，那么：

```math
\boxed{
\mathrm{Cov}(Y_{1j},Y_{2j})
=
\sigma_u^2
}
```

这就是边际协方差。

“边际化”的数学含义是：

> 把某个随机变量积分掉或求和掉，只看剩余变量的分布。

例如：

```math
p(Y_{1j},Y_{2j})
=
\int
p(Y_{1j},Y_{2j}\mid u_j)
p(u_j)
\,du_j
```

这里就是把 $u_j$ 积分掉。

---

# 9. ICC 与随机截距模型

因为：

```math
\mathrm{Var}(Y_{ij})
=
\sigma_u^2+\sigma_\varepsilon^2
```

而同一 group 内两个 observation 的协方差：

```math
\mathrm{Cov}(Y_{1j},Y_{2j})
=
\sigma_u^2
```

所以它们的相关系数为：

```math
\mathrm{Corr}(Y_{1j},Y_{2j})
=
\frac{
\mathrm{Cov}(Y_{1j},Y_{2j})
}{
\sqrt{
\mathrm{Var}(Y_{1j})
\mathrm{Var}(Y_{2j})
}
}
```

由于两个方差相同：

```math
=
\frac{\sigma_u^2}
{\sigma_u^2+\sigma_\varepsilon^2}
```

这就是 ICC：

```math
\boxed{
ICC
=
\frac{\sigma_u^2}
{\sigma_u^2+\sigma_\varepsilon^2}
}
```

因此：

- $\sigma_u^2$ 越大，相对于组内噪声越明显，ICC 越高；
- $\sigma_\varepsilon^2$ 越大，组内 observation 越不稳定，ICC 越低。

---

# 10. 为什么需要方差—协方差矩阵 $V$？

假设一个 group 有 3 个 observation：

```math
Y_{1j},Y_{2j},Y_{3j}
```

每个 observation 的方差都是：

```math
\sigma_u^2+\sigma_\varepsilon^2
```

任意两个不同 observation 的协方差都是：

```math
\sigma_u^2
```

所以可以把它们整理成矩阵：

```math
V_j=
\begin{pmatrix}
\sigma_u^2+\sigma_\varepsilon^2
&
\sigma_u^2
&
\sigma_u^2
\\
\sigma_u^2
&
\sigma_u^2+\sigma_\varepsilon^2
&
\sigma_u^2
\\
\sigma_u^2
&
\sigma_u^2
&
\sigma_u^2+\sigma_\varepsilon^2
\end{pmatrix}
```

这个矩阵只是把：

- 每个 observation 自己的方差；
- 每两个 observation 之间的协方差；

统一放在一个矩阵里。

因此：

```math
\boxed{
V=\text{数据中所有 observation 的方差—协方差结构}
}
```

---

# 11. 加入 predictor 后的一般模型

如果加入固定效应 predictor：

```math
Y_{ij}
=
\beta_0+\beta_1X_{ij}
+
u_j+\varepsilon_{ij}
```

可以把所有 observation 一次性写成：

```math
\boxed{
\mathbf Y
=
\mathbf X\boldsymbol\beta
+
\mathbf Z\mathbf u
+
\boldsymbol\varepsilon
}
```

其中：

- $\mathbf Y$：所有 observation 组成的向量；
- $\mathbf X\boldsymbol\beta$：fixed-effects 部分；
- $\mathbf Z\mathbf u$：random-effects 部分；
- $\boldsymbol\varepsilon$：所有 residual。

---

# 12. $Z$ 是干什么的？

假设有两个 group，每个 group 有两个 observation：

| Observation | Group |
|---|---|
| 1 | A |
| 2 | A |
| 3 | B |
| 4 | B |

随机截距向量：

```math
\mathbf u=
\begin{pmatrix}
u_A\\
u_B
\end{pmatrix}
```

设计矩阵：

```math
\mathbf Z=
\begin{pmatrix}
1&0\\
1&0\\
0&1\\
0&1
\end{pmatrix}
```

于是：

```math
\mathbf Z\mathbf u
=
\begin{pmatrix}
u_A\\
u_A\\
u_B\\
u_B
\end{pmatrix}
```

所以 $Z$ 的作用只是：

> 告诉模型，每一个 observation 应该使用哪个 group 的随机效应。

---

# 13. 为什么

```math
V=ZGZ^\top+R
```

？

从：

```math
\mathbf Y
=
\mathbf X\boldsymbol\beta
+
\mathbf Z\mathbf u
+
\boldsymbol\varepsilon
```

出发。

固定效应：

```math
X\beta
```

不是随机变量，因此不贡献方差。

所以：

```math
\mathrm{Var}(Y)
=
\mathrm{Var}(Zu+\varepsilon)
```

如果：

```math
u\perp\varepsilon
```

那么：

```math
\mathrm{Var}(Zu+\varepsilon)
=
\mathrm{Var}(Zu)
+
\mathrm{Var}(\varepsilon)
```

矩阵方差具有性质：

```math
\mathrm{Var}(AX)
=
A\mathrm{Var}(X)A^\top
```

因此：

```math
\mathrm{Var}(Zu)
=
Z\mathrm{Var}(u)Z^\top
```

定义：

```math
G=\mathrm{Var}(u)
```

以及：

```math
R=\mathrm{Var}(\varepsilon)
```

于是：

```math
\boxed{
V
=
ZGZ^\top+R
}
```

直观上：

```math
\boxed{
\text{总 covariance structure}
=
\text{random effects 贡献}
+
\text{residual 贡献}
}
```

---

# 14. 为什么

```math
Y\sim N(X\beta,V)
```

？

我们已经得到：

```math
E(Y)=X\beta
```

以及：

```math
\mathrm{Var}(Y)=V
```

同时假设：

```math
u
```

和：

```math
\varepsilon
```

都服从正态分布。

正态随机变量的线性组合仍然是正态分布，因此：

```math
\boxed{
Y\sim N(X\beta,V)
}
```

也就是说：

- 数据的平均结构由 $X\beta$ 决定；
- 数据的 variance/covariance structure 由 $V$ 决定。

---

# 15. 多元正态概率密度函数

如果：

```math
Y\sim N(\mu,\Sigma)
```

那么多元正态概率密度为：

```math
f(y)
=
\frac{1}
{(2\pi)^{n/2}|\Sigma|^{1/2}}
\exp
\left[
-\frac12
(y-\mu)^\top
\Sigma^{-1}
(y-\mu)
\right]
```

在混合效应模型中：

```math
\mu=X\beta
```

以及：

```math
\Sigma=V
```

所以：

```math
\boxed{
f(y)
=
\frac{1}
{(2\pi)^{n/2}|V|^{1/2}}
\exp
\left[
-\frac12
(y-X\beta)^\top
V^{-1}
(y-X\beta)
\right]
}
```

---

# 16. 为什么概率密度函数可以变成似然函数？

这里公式本身没有变。

改变的是：

> 哪些东西被固定，哪些东西被当作未知变量。

概率密度的视角是：

```math
f(y\mid\beta,V)
```

其中：

- 参数 $\beta,V$ 固定；
- $y$ 变化。

问题是：

> 在给定这些参数时，不同的数据 $y$ 有多可能出现？

但实际统计推断时：

- 数据 $y$ 已经观察到了；
- $\beta,V$ 未知。

所以把同一个函数改写成：

```math
L(\beta,V\mid y)
```

也就是：

```math
\boxed{
L(\beta,V\mid y)
=
f(y\mid\beta,V)
}
```

数值完全相同，只是解释角度改变。

因此：

```math
\boxed{
\text{概率：参数固定，看数据}
}
```

而：

```math
\boxed{
\text{似然：数据固定，看参数}
}
```

---

# 17. 为什么要取 log-likelihood？

Likelihood 为：

```math
L
=
\frac{1}
{(2\pi)^{n/2}|V|^{1/2}}
\exp
\left[
-\frac12Q
\right]
```

其中定义：

```math
Q
=
(y-X\beta)^\top
V^{-1}
(y-X\beta)
```

写成幂的形式：

```math
L
=
(2\pi)^{-n/2}
|V|^{-1/2}
e^{-Q/2}
```

两边取自然对数：

```math
\ell=\log L
```

于是：

```math
\ell
=
\log(2\pi)^{-n/2}
+
\log|V|^{-1/2}
+
\log e^{-Q/2}
```

分别得到：

```math
-\frac n2\log(2\pi)
```

```math
-\frac12\log|V|
```

以及：

```math
-\frac12Q
```

所以：

```math
\boxed{
\ell
=
-\frac12
\left[
n\log(2\pi)
+
\log|V|
+
(y-X\beta)^\top
V^{-1}
(y-X\beta)
\right]
}
```

因为 $\log(x)$ 是严格单调递增函数，所以：

```math
\arg\max L
=
\arg\max \log L
```

因此最大化 log-likelihood 和最大化 likelihood 得到完全相同的参数。

取 log 的主要好处是：

- 将乘法变成加法；
- 将指数函数化简；
- 数值计算更加稳定；
- 求导和优化更加方便。

---

# 18. log-likelihood 中两项的直觉

其中：

```math
(y-X\beta)^\top
V^{-1}
(y-X\beta)
```

可以理解为：

> 在考虑 observation 之间的 variance 和 covariance 后，模型预测与实际数据之间的加权偏差有多大。

它是普通最小二乘：

```math
\sum (y_i-\hat y_i)^2
```

在相关数据情况下的推广。

而：

```math
\log|V|
```

起到控制整体方差规模的作用。

如果只追求残差项小，可以无限增大方差，让任何数据都显得“不奇怪”。

```math
\log|V|
```

会惩罚过度膨胀的 covariance structure。

所以 maximum likelihood 实际上在平衡：

```math
\boxed{
\text{拟合数据}
}
```

与：

```math
\boxed{
\text{避免使用过大的方差来解释一切}
}
```

---

# 19. 固定效应 $\beta$ 的 GLS 解从哪里来？

如果暂时认为：

```math
V
```

已经知道，那么 log-likelihood 中与 $\beta$ 有关的部分是：

```math
Q(\beta)
=
(y-X\beta)^\top
V^{-1}
(y-X\beta)
```

最大化 likelihood 等价于最小化：

```math
Q(\beta)
```

对 $\beta$ 求导：

```math
\frac{\partial Q}{\partial\beta}
=
-2X^\top V^{-1}(y-X\beta)
```

令其等于 0：

```math
X^\top V^{-1}(y-X\beta)=0
```

展开：

```math
X^\top V^{-1}y
-
X^\top V^{-1}X\beta
=
0
```

因此：

```math
X^\top V^{-1}X\beta
=
X^\top V^{-1}y
```

两边左乘：

```math
(X^\top V^{-1}X)^{-1}
```

得到：

```math
\boxed{
\hat\beta
=
(X^\top V^{-1}X)^{-1}
X^\top V^{-1}y
}
```

这就是 Generalized Least Squares（GLS）的解。

---

# 20. OLS 是 GLS 的特殊情况

普通线性回归假设：

```math
V=\sigma^2I
```

所以：

```math
V^{-1}
=
\frac{1}{\sigma^2}I
```

代入 GLS：

```math
\hat\beta
=
(X^\top V^{-1}X)^{-1}
X^\top V^{-1}y
```

最终：

```math
\boxed{
\hat\beta_{\mathrm{OLS}}
=
(X^\top X)^{-1}X^\top y
}
```

因此：

```math
\boxed{
\text{OLS 是 GLS 在 observation 独立且同方差情况下的特殊情况}
}
```

这里还需要假设设计矩阵 $X$ 满列秩，使 $(X^\top X)^{-1}$ 存在。

---

# 21. 随机截距方差 $\sigma_u^2$ 是怎么估计的？

因为：

```math
V
=
ZGZ^\top+R
```

而 $G$ 和 $R$ 中包含：

```math
\sigma_u^2
```

和：

```math
\sigma_\varepsilon^2
```

所以这两个 variance component 同时出现在：

```math
|V|
```

和：

```math
V^{-1}
```

里面。

因此，一般情况下无法像 $\beta$ 那样得到简单的闭式解。

实际做法是：

1. 给定一组候选值

```math
\sigma_u^2,\sigma_\varepsilon^2
```

2. 根据它们构造 $V$；

3. 根据 $V$ 得到 $\hat\beta$；

4. 计算 log-likelihood；

5. 改变 variance components；

6. 重复直到 log-likelihood 最大。

所以：

```math
\boxed{
\hat\sigma_u^2,\hat\sigma_\varepsilon^2
}
```

通常通过数值优化得到。

---

# 22. ML 与 REML

ML 直接最大化：

```math
L(\beta,\sigma_u^2,\sigma_\varepsilon^2\mid y)
```

从整个数据分布同时估计 fixed effects 和 variance components。

REML（Restricted Maximum Likelihood）则在估计 variance components 时，对 fixed effects 占用的自由度进行调整。

直观上可以理解为：

> REML 更专注于“去除 fixed-effects 结构以后剩下的变异”来估计方差参数。

因此，在有限样本下，REML 对 variance component 的估计通常比 ML 偏差更小。

这个比较主要针对方差成分；在同一数据集上比较固定效应时，通常应使用 ML 而不是 REML。

---

# 23. 每个 group 的随机截距 $u_j$ 怎么得到？

需要注意：

```math
u_j
```

通常不是像固定效应参数一样单独自由估计，而是在总体方差参数确定后，根据该 group 的数据进行预测。

其一般形式是：

```math
\boxed{
\hat u
=
GZ^\top
V^{-1}
(y-X\hat\beta)
}
```

这称为：

```math
\text{BLUP}
```

即 Best Linear Unbiased Predictor。

当方差参数由数据估计后再代入这个公式时，更准确的名称是 empirical BLUP（EBLUP）。

---

# 24. BLUP 的来源

因为：

```math
Y=X\beta+Zu+\varepsilon
```

且 $u$ 和 $Y$ 都服从正态分布，所以：

```math
\begin{pmatrix}
u\\
Y
\end{pmatrix}
```

服从联合正态分布。

联合正态变量满足条件期望公式：

```math
E(u\mid Y)
=
E(u)
+
\mathrm{Cov}(u,Y)
\mathrm{Var}(Y)^{-1}
(Y-E(Y))
```

这里：

```math
E(u)=0
```

```math
E(Y)=X\beta
```

而：

```math
\mathrm{Var}(Y)=V
```

另外：

```math
\mathrm{Cov}(u,Y)
=
\mathrm{Cov}(u,Zu+\varepsilon)
```

由于：

```math
u\perp\varepsilon
```

所以：

```math
\mathrm{Cov}(u,Y)
=
GZ^\top
```

因此：

```math
E(u\mid Y)
=
GZ^\top
V^{-1}
(Y-X\beta)
```

也就是：

```math
\boxed{
\hat u
=
GZ^\top
V^{-1}
(y-X\hat\beta)
}
```

---

# 25. 最简单随机截距模型中的 shrinkage

对于第 $j$ 个 group：

```math
Y_{ij}
=
\beta_0+u_j+\varepsilon_{ij}
```

假设该 group 有：

```math
n_j
```

个 observation。

组内平均：

```math
\bar Y_j
=
\beta_0+u_j+\bar\varepsilon_j
```

其中：

```math
\mathrm{Var}(\bar\varepsilon_j)
=
\frac{\sigma_\varepsilon^2}{n_j}
```

因此：

```math
\bar Y_j-\beta_0
=
u_j+\bar\varepsilon_j
```

其中：

```math
u_j\sim N(0,\sigma_u^2)
```

而：

```math
\bar\varepsilon_j
\sim
N
\left(
0,
\frac{\sigma_\varepsilon^2}{n_j}
\right)
```

可以推出：

```math
\boxed{
\hat u_j
=
\frac{\sigma_u^2}
{\sigma_u^2+\sigma_\varepsilon^2/n_j}
(\bar Y_j-\beta_0)
}
```

这个闭式表达式把 $\beta_0$、$\sigma_u^2$ 和 $\sigma_\varepsilon^2$ 视为已知；实际拟合时用它们的估计值，因此得到的是经验 BLUP。

定义：

```math
\lambda_j
=
\frac{\sigma_u^2}
{\sigma_u^2+\sigma_\varepsilon^2/n_j}
```

则：

```math
\hat u_j
=
\lambda_j(\bar Y_j-\beta_0)
```

其中：

```math
0<\lambda_j<1
```

因此估计的随机截距不是简单的：

```math
\bar Y_j-\beta_0
```

而是会向 0 收缩。

这就是：

```math
\boxed{\text{shrinkage}}
```

或者：

```math
\boxed{\text{partial pooling}}
```

---

# 26. 为什么 shrinkage 很合理？

如果：

```math
\sigma_u^2
```

很大，说明不同 group 真的差异很大。

那么：

```math
\lambda_j\rightarrow1
```

模型更相信 group 自己的数据。

如果：

```math
\sigma_\varepsilon^2
```

很大，说明 observation 本身噪声很大。

那么：

```math
\lambda_j\rightarrow0
```

模型会把随机截距更多地拉向 0。

如果：

```math
n_j\rightarrow\infty
```

那么：

```math
\frac{\sigma_\varepsilon^2}{n_j}\rightarrow0
```

所以：

```math
\lambda_j\rightarrow1
```

也就是说，该 group 数据越多，其自身均值越可靠，收缩越少。

---

# 27. 整个线性混合效应模型的推导主线

从：

```math
\boxed{
Y=X\beta+Zu+\varepsilon
}
```

开始。

假设：

```math
u\sim N(0,G)
```

```math
\varepsilon\sim N(0,R)
```

于是：

```math
E(Y)=X\beta
```

以及：

```math
\mathrm{Var}(Y)
=
ZGZ^\top+R
=
V
```

因此：

```math
\boxed{
Y\sim N(X\beta,V)
}
```

于是可以写出多元正态密度：

```math
f(y\mid\beta,V)
```

把实际观察到的数据 $y$ 固定下来，把参数当成未知量：

```math
\boxed{
L(\beta,V\mid y)
=
f(y\mid\beta,V)
}
```

然后取 log：

```math
\ell=\log L
```

最大化：

```math
\ell
```

得到：

```math
\hat\beta
```

以及：

```math
\hat\sigma_u^2,\hat\sigma_\varepsilon^2
```

最后根据：

```math
\hat u
=
GZ^\top
V^{-1}
(y-X\hat\beta)
```

预测每个 group 的随机效应。

因此整个逻辑可以概括为：

```math
\boxed{
\text{数据生成模型}
\rightarrow
\text{方差—协方差结构}
\rightarrow
\text{边际正态分布}
\rightarrow
\text{likelihood}
\rightarrow
\text{ML / REML}
\rightarrow
\text{BLUP}
}
```

---

# 28. 最值得记住的几个公式

随机截距模型：

```math
Y_{ij}
=
\beta_0+u_j+\varepsilon_{ij}
```

随机截距：

```math
u_j\sim N(0,\sigma_u^2)
```

残差：

```math
\varepsilon_{ij}\sim N(0,\sigma_\varepsilon^2)
```

总方差：

```math
\mathrm{Var}(Y_{ij})
=
\sigma_u^2+\sigma_\varepsilon^2
```

同组协方差：

```math
\mathrm{Cov}(Y_{1j},Y_{2j})
=
\sigma_u^2
```

ICC：

```math
ICC
=
\frac{\sigma_u^2}
{\sigma_u^2+\sigma_\varepsilon^2}
```

一般线性混合模型：

```math
Y=X\beta+Zu+\varepsilon
```

总体 covariance：

```math
V=ZGZ^\top+R
```

边际分布：

```math
Y\sim N(X\beta,V)
```

GLS：

```math
\hat\beta
=
(X^\top V^{-1}X)^{-1}
X^\top V^{-1}y
```

BLUP：

```math
\hat u
=
GZ^\top
V^{-1}
(y-X\hat\beta)
```

简单随机截距中的 shrinkage：

```math
\hat u_j
=
\frac{\sigma_u^2}
{\sigma_u^2+\sigma_\varepsilon^2/n_j}
(\bar Y_j-\beta_0)
```

---

# 29. 一句话总结

线性混合效应模型的核心不是简单地“给每个 group 多加一个参数”，而是：

> 假设不同 group 的随机效应来自一个共同分布，通过这个分布产生组内相关性；再利用整个数据的方差—协方差结构建立边际概率模型，通过 ML 或 REML 估计总体参数，最后依据总体方差结构对每个 group 的随机效应进行带有 shrinkage 的预测。

