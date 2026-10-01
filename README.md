# AI-Assisted Learning Notes

> [!CAUTION]
> 本仓库中的大部分内容由人工智能辅助生成，主要用于个人学习、知识整理和复习。
> 其中的信息可能存在错误、遗漏或过时之处，尚未经过完整的人工核查。
> 请勿将其直接作为学术、医疗、法律、财务或其他专业决策的可靠依据；引用或使用前请查阅权威资料进行验证。

## About

本仓库记录我的日常学习笔记。笔记主题、学习方向和最终整理方式由我决定，人工智能参与内容生成、解释、改写和结构整理。

## Topics

- [统计建模与线性模型](statistical-modeling/)
- [贝叶斯方法与 MCMC](bayesian-methods/)
- [计算神经科学与 MRI/fMRI](neuroimaging-mri/)
- [空间统计与空间零模型](spatial-statistics/)
- [圆周统计与复向量](circular-statistics/)
- [研究方法与思维框架](research-methods/)
- [机器学习算法](machine-learning/)

## Review status

新笔记可以在文件开头加入以下元数据，用来标记 AI 辅助情况和人工审核状态：

```yaml
---
ai_assisted: true
review_status: unverified
last_reviewed:
---
```

完成核查后，将 `review_status` 改为 `reviewed`，并在 `last_reviewed` 中填写审核日期。

## Formula formatting

GitHub 上的 Markdown 笔记请用 `$...$` 书写行内公式，用 `math` 代码块书写独立公式。例如：

````text
行内： $y = \beta_0 + \beta_1 x$

独立公式：
```math
\hat\beta = (X^\top X)^{-1}X^\top y
```
````

行内公式前留一个空格；表格内公式的竖线使用 `\lvert` 和 `\rvert`。不要把多行公式放在单独成行的 `$$` 之间，也不要使用 `\(...\)` 或 `\[...\]` 作为 Markdown 中的公式分隔符；提交前可在 GitHub 的文件预览中确认公式显示。
