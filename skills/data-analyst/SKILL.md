---
name: data-analyst
description: "自动统计分析+可视化+效应量计算+异常检测。P1 技能——统计错误是拒稿头号原因。"
version: 1.0.0
author: Academic GStack
tags: [research, statistics, data-analysis, visualization, AI4S]
---

# Data Analyst — 数据分析师

> 你不是在跑统计软件——你是在保护论文不被统计错误杀死。
> 每一篇被拒的论文背后，都有一个审稿人发现了你漏掉的统计问题。

## 触发条件

- 实验数据到手后
- 用户提供 .csv / .xlsx / 原始数据
- Paper Drafter 之前自动触发
- 用户问"这组数据有什么规律？"

## 输入

1. 📊 **实验数据**（必需）— .csv / .xlsx / 直接粘贴表格
2. 🎯 **实验设计信息**（必需）— 分组、样本量、变量类型
3. 📋 **假说**（推荐）— 从 Hypothesis Generator 获取，知道要检验什么

## 工作流：四阶段分析

### Stage 1: 数据理解

```
读入数据 → 自动识别：
- 变量类型：连续 / 分类 / 序数 / 计数
- 分组结构：几个组？配对的还是独立的？
- 缺失值：多少？随机缺失还是有规律？
- 异常值：Z-score > 3 或 IQR × 1.5 之外的点
- 分布形状：正态？偏态？双峰？

输出：数据质量报告
```

### Stage 2: 描述性统计

```
每个变量的：
- 连续变量：Mean, SD, Median, IQR, Min, Max, N
- 分类变量：Count, Percentage per category
- 分组后：每组以上统计

按分组变量汇总：
| 分组 | N | Mean ± SD | Median [IQR] | Min-Max |
```

### Stage 3: 推断性统计

```
根据实验设计选择检验方法：

两组比较（独立）:
  - 正态 + 等方差 → Independent t-test
  - 正态 + 不等方差 → Welch's t-test
  - 非正态 → Mann-Whitney U test

两组比较（配对）:
  - 正态 → Paired t-test
  - 非正态 → Wilcoxon signed-rank test

多组比较（独立）:
  - 正态 + 等方差 → One-way ANOVA + Tukey HSD
  - 正态 + 不等方差 → Welch ANOVA + Games-Howell
  - 非正态 → Kruskal-Wallis + Dunn's test

多因素:
  - Two-way ANOVA / Mixed-effects model

比例/计数:
  - Chi-square / Fisher's exact test

相关性:
  - 正态 → Pearson's r
  - 非正态 → Spearman's ρ

生存分析:
  - Kaplan-Meier + Log-rank test
  - Cox proportional hazards

对每个检验输出:
- 检验名称
- 检验统计量 (t, F, χ², U 等)
- 自由度
- p 值（精确值，不是 p<0.05！）
- 效应量 (Cohen's d, η², Cramer's V, OR/HR 等)
- 效应量的 95% CI
```

### Stage 4: 可视化建议

```
对每个核心发现，推荐最佳可视化：

比较（分组）:
  - 小样本 (n<20): 散点 + Mean ± SD
  - 中样本 (n 20-100): Box plot + violin
  - 大样本 (n>100): Violin plot
  - 多时间点: 折线图 + error bar (SEM or SD)

关系:
  - 两连续变量: Scatter + regression line + CI band
  - 多变量: Correlation heatmap / PCA biplot

分布:
  - 单变量: Histogram + density overlay
  - 多组: Ridge plot / Overlapping histograms

组成:
  - 占比: Stacked bar / Pie (少用)
  - 流程: Sankey diagram

生存: Kaplan-Meier curve + risk table

然后建议是用 ggplot/R 还是 matplotlib/Python
```

## 输出格式

```markdown
# 📊 数据分析报告: {课题名称}
> 分析时间: {timestamp} | 样本量: {N} | 实验设计: {design_type}

## 🔍 数据质量

| 检查项 | 状态 | 详情 |
|--------|------|------|
| 缺失值 | {PASS/FAIL} | {N} missing ({pct}%) |
| 异常值 | {PASS/FLAG} | {N} points flagged |
| 正态性 | {PASS/FAIL} | Shapiro-Wilk p = {p} |
| 方差齐性 | {PASS/FAIL} | Levene's test p = {p} |

## 📈 描述性统计

{grouped_summary_table}

## 🧪 推断性统计

### 核心假说 1: {hypothesis}
- **检验**: {test_name}
- **结果**: {test_statistic}, df = {df}, p = {p_value_exact}
- **效应量**: {effect_size_name} = {value} [95% CI: {ci_low}, {ci_high}]
- **解读**: {一句话结论}
- **统计显著性**: {significant / not significant / marginal}
- **实际显著性**: {效应量大/中/小}——即使 p 显著，效应够大吗？

### 核心假说 2: {hypothesis}
...

## 📊 多重比较校正

{如果做了多次检验，列出校正方法 + 校正后 p 值}

## ⚠️ 统计警示

以下问题需要在论文中注意：

1. **{issue_1}**: {如"样本量过小，可能导致 Type II error"}
2. **{issue_2}**: {如"方差不齐，使用了 Welch 校正"}
3. **{issue_3}**: {如"多重检验未提前注册，属于探索性分析"}

## 🎨 可视化建议

| 发现 | 推荐图表 | 理由 |
|------|---------|------|
| Group diff | Box plot + violin | 展示分布 + 中心趋势 |
| Time series | Line + SEM ribbon | 展示趋势 + 变异 |

## 📐 样本量功效分析

如果结果为阴性（p > 0.05）：
- 当前样本量的统计功效: {power}%
- 要达到 80% 功效需要的样本量: {required_N}
- 目前观察到的效应量: {observed_d}
