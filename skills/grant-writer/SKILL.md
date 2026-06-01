---
name: grant-writer
description: "基于论文/假说自动生成基金申请书初稿：背景、目标、创新点、预算、时间线。P2 技能。"
version: 1.0.0
author: Academic GStack
tags: [research, grant-writing, funding, proposal, AI4S]
---

# Grant Writer — 基金申请书生成器

> 基金 = 自由 = 博后选择权 = 创业启动资金。
> 你不会因为申请太多基金被拒——你只会因为不申请而后悔。

## 触发条件

- 论文初稿或假说成型后
- 基金申请季开始前
- 用户说"帮我写个基金申请书"
- PI Reviewer 标记了"高基金潜力"的课题

## 申请书结构（标准 NSF/NIH/NSFC 格式）

### Section 1: 项目摘要 (Project Summary)

```
三段式：

智力价值 (Intellectual Merit):
  这个项目要解决什么科学问题？
  为什么现有方法/理论不够？
  你的方法有什么独特优势？

更广泛影响 (Broader Impacts):
  这个研究对社会/技术/教育有什么影响？
  谁受益？（不只是学术界）

关键词: 5-8 个
```

### Section 2: 研究背景与意义

```
Paragraph 1: 大背景
  - 这个领域为什么重要
  - 当前的知识状态

Paragraph 2: 知识空白
  - 什么没解决
  - 为什么难解决
  - 解决它的重要性

Paragraph 3: 你的前期基础
  - 你已经做了什么（preliminary data）
  - 为什么你是做这件事的最佳人选
```

### Section 3: 研究目标与假说

```
Overall Goal: {一句话}

Specific Aim 1: {目标}
  Hypothesis: {假说}
  Rationale: {为什么这个假说是合理的}
  Approach: {用什么方法}
  Expected Outcomes: {做什么预期}
  Alternative Strategies: {如果失败了怎么办}

Specific Aim 2: {同上}

Specific Aim 3: {同上}

Aims 之间的逻辑关系: {Aim 1 → Aim 2 → Aim 3 怎么串联}
```

### Section 4: 研究方法

```
对每个 Aim:
  - 实验设计
  - 关键方法（不用重写 protocol，但要足够详细让 reviewer 相信你会做）
  - 样本量与统计计划
  - 潜在问题与替代方案
  - 时间线

创新点标注:
  - 🆕 方法创新: {new_method}
  - 🆕 概念创新: {new_concept}
  - 🆕 跨学科: {cross_disciplinary_aspect}
```

### Section 5: 预算与时间线

```
Year 1:
  Q1-Q2: {aim1_experiments}
  Q3-Q4: {aim1_analysis + aim2_start}
  人员: {personnel}
  设备/试剂: {major_expenses}

Year 2:
  ...

Year 3:
  ...

预计总预算: ${total} (根据基金类型调整)
```

### Section 6: 预期成果

```
论文: 预计发表 {N} 篇，目标期刊 {journal_tier}
人才培养: 培养 {N} 名研究生/博士后
技术产出: {patents / software / databases / protocols}
学术交流: 参加 {N} 次国际会议
```

## 基金类型适配

| 基金 | 特点 | 重点 |
|------|------|------|
| NSFC 面上 | 3年, ~55万 | 前期基础+创新性 |
| NSFC 青年 | 3年, ~30万 | 创新潜力+可行性 |
| NIH R01 | 5年, $1-2M | Prelim data + 团队能力 |
| NIH R21 | 2年, $275K | 高风险高回报探索 |
| NSF | 3年 | 更广泛影响强调 |
| ERC Starting | 5年, €1.5M | 申请人独立性和突破性 |
| 博后基金（各种） | 1-2年 | 个人发展+导师匹配 |

## 输出格式

完整的申请书，按以上六节组织。

额外输出：
- 一句话 elevator pitch（电梯间偶遇基金会主任时用）
- 评审标准对照表（你的申请书 vs 该基金的评审标准）

## 注意事项

- Preliminary data 要标注哪些是已有的，哪些是"预期会有的"
- 预算要合理——太多显得贪婪，太少显得不切实际
- 时间线不要太乐观——加上 30% buffer
- 每个 Aim 都必须有 alternative strategy——"如果失败了怎么办"
- 不要假设 reviewer 是你的领域专家——背景部分要写得让隔壁领域的人也能理解
