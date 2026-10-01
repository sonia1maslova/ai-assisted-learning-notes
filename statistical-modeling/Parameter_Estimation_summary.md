# 参数估计（Parameter Estimation）知识总结

## 1. 参数估计的核心概念

统计模型通常描述为：

```math
Y=f(X,\theta)+\epsilon
```

其中：

-   $Y$：观测数据（dependent variable）
-   $X$：预测变量或设计矩阵（predictors/design matrix）
-   $f()$：模型结构
-   $\theta$：未知参数（parameters）
-   $\epsilon$：误差项（error）

模型本身描述"数据如何产生"，而参数估计回答：

> 给定观测数据，如何找到最合理的参数值？

例如线性模型：

```math
Y=X\beta+\epsilon
```

其中：

```math
\beta=
\begin{bmatrix}
\beta_0\\
\beta_1
\end{bmatrix}
```

表示截距和斜率。

------------------------------------------------------------------------

# 2. 参数估计的一般流程

统一框架：

```text
假设数据生成模型
        ↓
定义未知参数
        ↓
定义评价标准（Loss / Likelihood / Posterior）
        ↓
寻找最佳参数
        ↓
得到参数估计值
```

不同参数估计方法的主要区别：

1.  优化什么目标？
2.  如何寻找最优参数？

------------------------------------------------------------------------

# 3. 最小二乘估计（Least Squares, LS）

## 3.1 基本思想

目标：

让预测值和真实值之间的误差最小。

线性模型：

```math
Y=X\beta+\epsilon
```

预测：

```math
\hat{Y}=X\beta
```

残差：

```math
e=Y-X\beta
```

残差平方和：

```math
RSS=e^Te
```

即：

```math
RSS=(Y-X\beta)^T(Y-X\beta)
```

目标：

```math
\min_{\beta}(Y-X\beta)^T(Y-X\beta)
```

------------------------------------------------------------------------

## 3.2 为什么使用平方误差？

因为：

-   正负误差会抵消
-   平方保证所有误差贡献为正
-   大误差受到更强惩罚

展开：

```math
e^Te=e_1^2+e_2^2+...+e_n^2
```

------------------------------------------------------------------------

## 3.3 求解析解

目标函数：

```math
Loss=(Y-X\beta)^T(Y-X\beta)
```

展开：

```math
Loss=
Y^TY-Y^TX\beta-\beta^TX^TY+\beta^TX^TX\beta
```

对参数求导：

```math
\frac{\partial Loss}{\partial\beta}=0
```

得到：

```math
-2X^TY+2X^TX\beta=0
```

整理：

```math
X^TX\beta=X^TY
```

两边左乘：

```math
(X^TX)^{-1}
```

得到：

```math
\boxed{
\hat{\beta}=(X^TX)^{-1}X^TY
}
```

这就是普通最小二乘（OLS）的解析解。

------------------------------------------------------------------------

# 4. 最大似然估计（Maximum Likelihood Estimation, MLE）

## 4.1 核心思想

MLE 不问：

"误差是否最小？"

而问：

> 哪一组参数最可能产生当前观察到的数据？

数学：

```math
\hat{\theta}=\arg\max_\theta L(\theta)
```

其中：

```math
L(\theta)=p(\mathrm{data}\mid\theta)
```

称为 likelihood（似然）。

------------------------------------------------------------------------

# 5. 为什么正态误差下 MLE 等价于最小二乘？

假设：

```math
\epsilon\sim N(0,\sigma^2)
```

正态分布：

```math
p(\epsilon)= \frac1{\sqrt{2\pi\sigma^2}}
e^{-\frac{\epsilon^2}{2\sigma^2}}
```

对于多个独立观测：

```math
L(\beta) = \prod_i p(e_i)
```

代入：

```math
L(\beta) = C e^{-\frac{\sum e_i^2}{2\sigma^2}}
```

其中：

C 为常数。

最大化：

```math
L(\beta)
```

等价于最大化：

```math
e^{-\frac{\sum e_i^2}{2\sigma^2}}
```

因为指数函数单调：

等价于最小化：

```math
\boxed{
\sum e_i^2
}
```

因此：

```math
\boxed{
MLE=\text{Least Squares}
}
```

在线性模型 + 正态误差假设下成立。

------------------------------------------------------------------------

# 6. 最大后验估计（MAP）

## 6.1 思想

MLE：

只考虑数据。

MAP：

同时考虑：

-   数据
-   先验知识

贝叶斯公式：

```math
\mathrm{Posterior} \propto \mathrm{Likelihood}\times \mathrm{Prior}
```

即：

```math
P(\theta\mid \mathrm{data}) \propto
P(\mathrm{data}\mid\theta)P(\theta)
```

MAP寻找：

```math
\boxed{
\hat{\theta}
=
\arg\max_\theta p(\theta\mid \mathrm{data})
}
```

------------------------------------------------------------------------

# 7. 贝叶斯参数估计（Bayesian Estimation）

与传统方法不同：

不是寻找一个固定参数。

而是估计：

```math
P(\theta\mid \mathrm{data})
```

即：

参数的不确定性分布。

输出：

-   posterior mean
-   credible interval
-   posterior probability

------------------------------------------------------------------------

# 8. MCMC 参数估计

复杂模型中：

posterior无法直接求解。

例如：

```math
P(\theta\mid \mathrm{data})
```

无法解析计算。

因此使用：

Markov Chain Monte Carlo。

基本思想：

通过随机采样：

```math
\theta_1,\theta_2,...,\theta_n
```

逼近后验分布。

例如：

最终得到：

    1.8
    2.0
    2.3
    2.5
    2.7

这些样本代表：

```math
P(\theta\mid \mathrm{data})
```

你的 bpnreg circular mixed model 就属于这一类。

------------------------------------------------------------------------

# 9. 梯度下降（Gradient Descent）

用于：

没有解析解的大规模优化问题。

目标：

最小化：

```math
Loss(\theta)
```

计算梯度：

```math
\nabla Loss(\theta)
```

更新：

```math
\theta_{new} =
\theta-\alpha\nabla Loss
```

其中：

$\alpha$

为学习率。

应用：

-   神经网络
-   大规模机器学习

------------------------------------------------------------------------

# 10. EM算法（Expectation-Maximization）

用于：

存在隐藏变量（latent variables）的模型。

例如：

混合模型。

两个步骤：

## E step

估计隐藏变量：

```math
P(Z\mid \mathrm{data},\theta)
```

## M step

更新参数：

```math
\theta
```

循环：

```text
初始化参数
    ↓
E step
    ↓
M step
    ↓
重复直到收敛
```

------------------------------------------------------------------------

# 11. REML（Restricted Maximum Likelihood）

用于：

线性混合模型。

模型：

```math
Y=X\beta+Zu+\epsilon
```

包含：

-   固定效应 $\beta$
-   随机效应 $u$
-   方差参数

REML：

先减少固定效应影响，再估计方差结构。

常用于：

Linear Mixed Model。

------------------------------------------------------------------------

# 12. 方法之间关系

```text
参数估计
├── 优化类
│   ├── Least Squares
│   ├── Gradient Descent
│   └── Newton-Raphson
├── 似然类
│   ├── Maximum Likelihood
│   └── REML
└── 贝叶斯类
    ├── MAP
    └── MCMC
```

------------------------------------------------------------------------

# 13. 与常见模型对应

| 模型 | 参数估计方法 |
|---|---|
| 普通线性回归 | OLS / MLE |
| GLM | MLE + 数值优化 |
| Logistic regression | MLE |
| Linear mixed model | ML / REML |
| Bayesian mixed model | MCMC |
| Circular Bayesian model | MCMC |
| Neural network | Gradient descent |

------------------------------------------------------------------------

# 14. 核心总结

模型拟合本质：

```math
\boxed{
模型结构
+
参数估计方法
=
完整模型
}
```

模型告诉我们：

> 数据如何生成。

参数估计告诉我们：

> 根据数据，参数是多少。

最重要的三类思想：

1.  最小化误差：

```math
\min Loss
```

2.  最大化数据概率：

```math
\max Likelihood
```

3.  推断参数分布：

```math
P(\theta\mid \mathrm{data})
```

理解这三类思想，可以统一理解 GLM、混合模型、贝叶斯模型以及机器学习模型。
