---
ai_assisted: true
review_status: unverified
last_reviewed:
---

# 复向量（Complex Vector）基础知识总结

## 1. 什么是复向量？

复向量（complex vector）是使用复数表示的向量。

二维实向量：

```math
\mathbf{v}=(x,y)
```

可以表示为复数：

```math
z=x+yj
```

其中：

-   x：实部（real part）
-   y：虚部（imaginary part）
-   j：虚数单位

满足：

```math
j^2=-1
```

因此：

```math
(x,y)\longleftrightarrow x+yj
```

二者表示同一个二维方向和长度。

------------------------------------------------------------------------

# 2. 复数的几何意义

复数：

```math
z=a+bj
```

对应复平面：

-   横轴：实部 Re(z)
-   纵轴：虚部 Im(z)

例如：

```math
z=3+4j
```

等价于二维向量：

```math
(3,4)
```

长度：

```math
|z|=\sqrt{3^2+4^2}=5
```

方向：

```math
\theta=\arctan\!\left(\frac{4}{3}\right)
```

因此复数天然包含：

1.  大小（magnitude）
2.  方向（phase angle）

------------------------------------------------------------------------

# 3. 极坐标形式与欧拉公式

复数也可以写成：

```math
z=r\,e^{j\theta}
```

其中：

-   r：向量长度
-   theta：方向角度

欧拉公式：

```math
e^{j\theta}=\cos\theta+j\sin\theta
```

例如：

```math
e^{j60^\circ}
```

展开：

```math
e^{j60^\circ}=\cos 60^\circ+j\sin 60^\circ
```

因为：

```math
\cos 60^\circ=0.5,\qquad \sin 60^\circ\approx0.866
```

所以：

```math
e^{j60^\circ}\approx0.5+0.866j
```

因此：

```math
(0.5,0.866)\longleftrightarrow 0.5+0.866j\approx e^{j60^\circ}
```

表示同一个单位方向向量。

------------------------------------------------------------------------

# 4. 为什么需要复向量？

角度不是普通线性变量。

例如：

```math
10^\circ\quad\text{和}\quad350^\circ
```

普通平均：

```math
\frac{10^\circ+350^\circ}{2}=180^\circ
```

这是错误的。

因为：

```math
0^\circ=360^\circ
```

角度具有周期性。

复向量通过：

```math
\theta\longmapsto e^{j\theta}
```

将角度转换成单位向量。

之后可以直接进行向量加和。

------------------------------------------------------------------------

# 5. 圆周平均（Circular Mean）

对于多个角度：

```math
\theta_1,\theta_2,\ldots,\theta_n
```

转换为：

```math
z_k=e^{j\theta_k}
```

求和：

```math
Z=\sum_{k=1}^{n}e^{j\theta_k}
```

平均方向：

```math
\bar\theta=\mathrm{arg}(Z)
```

集中程度：

```math
\mathrm{MRL}=\frac{|Z|}{n}
```

其中：

MRL（mean resultant length）表示方向集中程度。

------------------------------------------------------------------------

# 6. MRL 的意义

如果所有角度接近：

例如：

```math
60^\circ,\;65^\circ,\;70^\circ
```

向量方向一致：

此时 MRL 接近 1。

表示高度集中。

如果角度随机：

例如：

```math
0^\circ,\;120^\circ,\;240^\circ
```

向量相互抵消：

此时 MRL 接近 0。

表示没有稳定方向。

------------------------------------------------------------------------

# 7. 加权复向量

当不同观测的重要性不同，可以加入权重：

```math
Z=\sum_{k=1}^{n}w_k e^{j\theta_k}
```

其中：

-   theta_k：第 k 个方向
-   w_k：权重

在神经信号分析中：

权重可以表示：

-   信号强度
-   相位集中程度（MRL）

------------------------------------------------------------------------

# 8. 神经科学中的应用

## 8.1 相位分析

脑电、SEEG、LFP 等信号中的相位属于圆周变量。

不能直接计算普通平均。

因此：

```math
\theta\longmapsto e^{j\theta}
```

得到：

```math
Z=\sum_{k=1}^{n}e^{j\theta_k}
```

其中：

方向：

```math
\text{phase}=\mathrm{arg}(Z)
```

表示平均偏好相位。

长度：

```math
\mathrm{MRL}=\frac{|Z|}{n}
```

表示相位集中程度。

## 8.2 PAC 中的复向量表示

对于 phase-amplitude coupling：

首先得到相位 bin 概率：

```math
p(k)
```

每个相位 bin：

```math
e^{j\theta(k)}
```

复向量：

```math
z=\sum_k p(k)e^{j\theta(k)}
```

展开：

```math
z=\sum_k p(k)\cos\theta(k)
  +j\sum_k p(k)\sin\theta(k)
```

其中：

-   实部表示水平分量
-   虚部表示垂直分量

最终：

```math
\text{preferred phase}=\mathrm{arg}(z)
```

```math
\text{phase concentration}=|z|
```

------------------------------------------------------------------------

# 9. 复向量与普通向量的关系

| | 普通向量 | 复向量 |
|---|---|---|
| 表示 | $(x,y)$ | $x+yj$ |
| 空间 | 二维空间 | 复平面 |
| 包含信息 | 长度 + 方向 | 长度 + 方向 |
| 优势 | 一般空间问题 | 旋转、相位、周期问题 |

数学上：

```math
(x,y)\longleftrightarrow x+yj
```

二者等价。

但是复向量更加适合处理周期性数据。

------------------------------------------------------------------------

# 总结

复向量的核心思想：

```text
角度
  ↓
单位复向量
  ↓
复向量加和
  ↓
平均方向 + 集中程度
```

在神经振荡研究中：

-   复向量方向 = preferred phase
-   复向量长度 = phase concentration / MRL

这是圆周统计、PAC、相位同步分析的重要数学基础。
