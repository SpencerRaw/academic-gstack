---
name: figure-artist
description: "自动生成发表级图表：配色、排版、分辨率、多面板布局。P2 技能。"
version: 1.0.0
author: Academic GStack
tags: [research, data-visualization, figures, publication, AI4S]
---

# Figure Artist — 图表设计师

> 好图不是"好看"——好图是让审稿人用 10 秒看懂你 6 个月的实验。
> 差图会让最好的数据看起来不可信。

## 触发条件

- Data Analyst 分析完成后
- Paper Drafter 需要图表时
- 用户说"帮我画个图"
- 数据到齐需要做 Figure Panel

## 设计原则

### 原则 1: 自明性 (Self-Explanatory)
图形 + 图注 = 不需要读正文就能理解。
- 坐标轴标签清楚
- 图例完整
- 缩写首次出现标注全称

### 原则 2: 诚实性 (Honesty)
数据怎么分布就怎么画。不隐藏变异、不截断坐标轴。
- 展示所有数据点（不只是 Mean ± SEM）
- 坐标轴从零开始或在断裂处明确标注
- Error bar 标注是 SD / SEM / CI

### 原则 3: 一致性 (Consistency)
整篇论文的配色、字体、样式统一。
- 同一实验条件下颜色相同
- 同一变量在不同图中用同一符号
- 字体大小在印刷品中 ≥ 6pt

### 原则 4: 可达性 (Accessibility)
色盲友好 + 灰度打印可读。
- 不用红-绿组合
- 用 ColorBrewer / viridis 调色板
- 形状 + 颜色双重编码

## 图表类型决策树

```
数据问题是：

"比较值的大小？"
├── 2组 → Bar/Point plot + individual points
├── 3-6组 → Box plot + violin
├── 6+组 → Heatmap 或 降维图
└── 多因素 → Faceted plot 或 Interaction plot

"观察随时间/条件的变化趋势？"
├── 连续X → Line + ribbon/error band
├── 分类X → Connected dot plot
└── 多组趋势 → Faceted lines

"两个变量之间的关系？"
├── 均为连续 → Scatter + regression (with CI)
├── 多变量 → Correlation heatmap 或 PCA biplot
└── 非线性 → LOESS smoothing

"数据的分布？"
├── 单变量 → Histogram + density
├── 多组 → Ridge plot 或 Overlapping density
└── 多变量 → Pair plot 或 PCA

"组成部分/占比？"
├── 2-5类 → Stacked bar 或 Donut
├── 5+类 → Treemap
└── 层级 → Sankey 或 Sunburst

"空间/位置信息？"
├── 细胞/组织 → Microscopy image panel
├── 地理 → Map/Choropleth
└── 分子结构 → 3D structure ribbon/surface

"流程/机制？"
→ Schematic diagram (Illustrator/BioRender)
```

## 多面板 Figure 布局

```
标准布局 (Nature/Cell 风格):

Figure 1 (核心发现):
┌─────────────┬─────────────┐
│   Fig 1A    │   Fig 1B    │
│  Schematic  │  Main data  │
├─────────────┴─────────────┤
│          Fig 1C           │
│    Supporting evidence    │
├─────────────┬─────────────┤
│   Fig 1D    │   Fig 1E    │
│  Validation │  Statistics │
└─────────────┴─────────────┘

每个 Figure ≤ 6 panels
每个 Panel 标注字母 (A-F)，按阅读顺序
```

## 配色方案

```
推荐调色板（色盲友好）：

定性（分类数据）:
  - ColorBrewer Set2: #66C2A5 #FC8D62 #8DA0CB #E78AC3
  - 适用于: 不同实验组/条件

顺序（连续数据）:
  - viridis: 从紫到黄
  - 适用于: 表达量/浓度/强度

发散（有中点）:
  - RdBu: 红-白-蓝
  - 适用于: 变化倍数/差异/相关系数

避免:
  - 红+绿（色盲无法区分）
  - 彩虹配色（jet/rainbow）
  - 默认 Excel 配色
  - 低于 6pt 的文字
```

## 分辨率与格式

```
期刊要求:

Nature/Cell/Science:
  - 初次投稿: PDF/EPS, 矢量图, 字体嵌入
  - 修改稿: TIFF ≥ 300dpi (照片), ≥ 600dpi (线条)
  - 宽度: 89mm (单栏) / 183mm (双栏)

ACS (JACS/Nano Letters):
  - TIFF/PNG ≥ 300dpi
  - 字体 Arial/Helvetica
  - 线条 ≥ 0.5pt (打印后可见)

RSC (Chemical Science):
  - TIFF/PDF ≥ 600dpi (线条), ≥ 300dpi (照片)
  - 推荐矢量格式

通用规则:
  - 初次投稿: 矢量图 (PDF/EPS/SVG) —— 无损、无限缩放
  - 照片: TIFF ≥ 300dpi
  - 绝对不要: 截屏 / PowerPoint 导出 / JPEG (< 300dpi)
```

## 输出格式

```markdown
# 🎨 图表生成报告: {论文标题}

## Figure 1: {figure_title}

### 设计方案
- 图表类型: {chart_type}
- 数据: {data_source}
- 配色: {palette}
- 分辨率: {dpi} dpi, {format}

### Panels

**Fig 1A**: {description}
- 显示: {what it shows}
- 关键特征: {key feature to highlight}
- 数据 n: {sample_size}

**Fig 1B**: ...
...

### 图注草稿
**Figure 1. {title}.** (A) {description}. (B) {description}. 
Data are presented as {mean ± SD / median [IQR]}. 
n = {N} {biological/technical} replicates. 
{p_value_info}. Scale bars: {scale}.

### 已生成文件
- `fig1.{format}` — {dpi}dpi, {width}×{height}mm
- 源代码: `fig1.{R/py}`

---

## Figure 2: ...

## 📐 排版建议

- 总 Figure 数: {N} (建议 ≤ 6-8 个主 Figure + 补充)
- 补充 Figure 数: {N_supp}
- 建议拆分为 {X} 个主 Figure + {Y} 个补充 Figure
```

## 注意事项

- 可以先出草稿图（快速），再出精修图（耗时）
- 用代码生成（R/ggplot2 或 Python/matplotlib/seaborn）而不是手动调——可复现、可修改
- 图注在一个单独文件中管理——方便统一修改
- 投稿前确认目标期刊的具体要求（尺寸/格式/分辨率/字体）
- 复杂示意图（机制图）推荐 BioRender 或 Illustrator，代码难以生成
