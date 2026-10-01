
# 建模基础知识：从模型、似然到优化的整体框架

## 1. 建模的总体思想

所有统计建模和机器学习模型，本质上都在解决：

> 假设一个数据生成机制，然后寻找一组参数，使模型尽可能符合真实数据。

整体流程：

```
真实世界
 ↓
产生数据（未知机制）
 ↓
提出模型
 ↓
定义参数 θ
 ↓
模型预测数据
 ↓
比较预测与真实数据差异
 ↓
定义目标函数（loss / likelihood）
 ↓
估计参数
 ↓
模型评价
```

---

# 2. 模型本质：一个函数

模型可以抽象为：

```math
y=f(x,\theta)
```

其中：

- x：输入变量
- y：输出变量
- θ：模型参数

不同模型的区别主要在：

1. 函数形式不同
2. 参数不同
3. 参数估计方法不同

例如：

线性模型：

```math
Y=\beta_0+\beta_1X+\epsilon
```

神经网络：

```math
y=f(x,W)
```

---

# 3. 参数（Parameter）

参数是模型中未知、需要估计的量。

例如：

```math
Y=\beta_0+\beta_1X
```

其中：

- β0：截距
- β1：斜率

模型拟合的目标：

找到最合理的参数。

通常表示：

```math
\theta
```

θ代表所有参数的集合。

---

# 4. 损失函数（Loss Function）

模型预测：

```math
\hat y
```

真实值：

```math
y
```

两者差异：

```math
y-\hat y
```

称为残差。

为了衡量模型错误程度，需要定义损失函数。

例如均方误差：

```math
\mathrm{MSE}=
\frac{1}{n}\sum_{i=1}^{n}(y_i-\hat y_i)^2
```

目标：

让Loss尽可能小。

---

# 5. 似然（Likelihood）

## 5.1 概率和似然的区别

概率：

已知参数，预测数据：

```math
P(\mathrm{data}\mid\theta)
```

问题：

“如果参数是真的，出现这些数据的概率是多少？”

---

似然：

已知数据，评价参数：

```math
L(\theta\mid\mathrm{data})
```

问题：

“哪个参数最能解释当前数据？”

数学形式类似，但是解释方向不同。

---

# 6. 最大似然估计（MLE）

目标：

找到让数据出现概率最大的参数：

```math
\theta^*=\mathrm{argmax}_\theta L(\theta)
```

含义：

找到最可能产生当前数据的参数。

---

# 7. argmin 和 argmax

## argmin

argument of minimum

表示：

找到使函数达到最小值的输入。

例如：

```math
\theta^*=\mathrm{argmin}_\theta L(\theta)
```

含义：

找到让loss最小的参数θ。

---

## argmax

表示：

找到使函数达到最大值的输入。

例如：

```math
\theta^*=\mathrm{argmax}_\theta L(\theta)
```

含义：

找到likelihood最大的参数。

---

重要区别：

|目标|公式|
|-|-|
|最小化误差|argmin|
|最大化概率|argmax|

---

# 8. 梯度下降（Gradient Descent）

argmin描述目标：

“我要找到最低点”。

梯度下降描述方法：

“如何找到最低点”。

公式：

```math
\theta=\theta-\eta\nabla_{\theta}L(\theta)
```

解释：

- θ：当前参数
- η：学习率（learning rate）
- ∇L：损失函数梯度

梯度表示函数增加最快方向。

因为目标是下降，所以沿梯度反方向移动：

```math
-\nabla_{\theta}L(\theta)
```

---

# 9. 优化整体关系

```
目标：
找到最佳参数

        ↓

数学表达：

argmin / argmax

        ↓

求解方法：

梯度下降
解析解
MCMC
EM算法
```

---

# 10. 常见数学符号

|符号|含义|
|-|-|
|X|输入变量、自变量|
|Y|输出变量、因变量|
|ŷ|预测值|
|θ|参数集合|
|β|固定效应参数|
|ε|误差|
|n|样本数量|
|i|第i个观测|
|Σ|求和|
|x̄|平均值|
|P|概率|
|L|似然函数|
|μ|均值|
|σ|标准差|
|∇|梯度|
|η|学习率|
|∝|正比于|
|argmin|寻找最小值对应参数|
|argmax|寻找最大值对应参数|

---

# 11. 混合模型中的符号

线性混合模型：

```math
Y=X\beta+Zu+\epsilon
```

含义：

|符号|含义|
|-|-|
|Y|观测数据|
|X|固定效应设计矩阵|
|β|固定效应|
|Z|随机效应设计矩阵|
|u|随机效应|
|ε|误差|

---

# 12. 贝叶斯模型

贝叶斯公式：

```math
P(\theta\mid\mathrm{data})
\propto
P(\mathrm{data}\mid\theta)P(\theta)
```

三个部分：

## Prior

```math
P(\theta)
```

先验知识。

## Likelihood

```math
P(\mathrm{data}\mid\theta)
```

数据对参数的支持。

## Posterior

```math
P(\theta\mid\mathrm{data})
```

结合数据后的参数分布。

---

# 13. 阅读模型公式的方法

看到任何模型公式：

## 第一步

问：

我要解释什么？

（Y是什么）

## 第二步

问：

输入是什么？

（X是什么）

## 第三步

问：

未知参数是什么？

（θ、β是什么）

## 第四步

问：

误差或概率模型是什么？

（ε、likelihood）

## 第五步

问：

参数如何估计？

- MLE
- Bayesian
- MCMC
- Gradient descent

---

# 14. 建模核心思想总结

任何模型都可以拆成：

1. 数据生成假设（Model）
2. 参数（Parameter）
3. 目标函数（Loss / Likelihood）
4. 参数估计方法（Optimization / Inference）
5. 模型评价（Model evaluation）

理解这五部分，就能理解大多数统计模型和机器学习模型。
