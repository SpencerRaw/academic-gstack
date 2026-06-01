---
name: novelty-checker
description: "全网搜索验证假说/发现的新颖性，标注已有工作，防止重复发明。P2 技能。"
version: 1.0.0
author: Academic GStack
tags: [research, novelty-check, prior-art, literature, AI4S]
---

# Novelty Checker — 新颖性验证师

> "First" "Novel" "Unprecedented" — 三个词让你的论文被 desk reject。
> 在你声称之前，先确认。

## 触发条件

- Hypothesis Generator 输出后
- 论文投稿前（最后检查）
- 用户说"这个想法有人做过吗？"
- Peer Reviewer 质疑新颖性时

## 工作流

### Step 1: 假说分解

```
把核心假说分解为可搜索的组件：

假说: "碳点通过线粒体途径诱导 ferroptosis"

分解:
1. 碳点 + ferroptosis
2. 碳点 + 线粒体 + 细胞死亡
3. carbon dots + ferroptosis + mitochondria
4. CDs + iron-dependent cell death
5. 碳点 + 铁死亡（CNKI/万方）
```

### Step 2: 多源搜索

```
对每个分解后的查询:

Google Scholar: "{query}" → 检查被引数高的结果
PubMed: "{query}" → 生物医学
arXiv: "{query}" → 预印本
bioRxiv: "{query}" → 生物预印本
chemRxiv: "{query}" → 化学预印本
Web of Science: "{query}" → 正式发表
CNKI/万方: "{中文查询}" → 中文文献
```

### Step 3: 重叠分析

```
对每篇搜索结果，判断与你的假说的重叠程度：

🔴 HIGH OVERLAP — 几乎相同
  - 相同的机制、相同的系统、相同的结论
  - 你的假说已被发表 → 需要 pivot

🟡 PARTIAL OVERLAP — 部分重叠
  - 相似但不完全相同
  - 你的差异点: {differentiating_factor}
  - 需要重新定位 story

🟢 NO OVERLAP — 无直接竞争
  - 不同系统/不同机制/不同方法
  - 可以声称新颖性
```

### Step 4: 新颖性声明撰写

```
如果 HIGH OVERLAP → 不要硬说 novel。调整角度：
  - "Building on X et al., we extend..."  
  - "While X demonstrated Y in system A, we show Y in system B..."
  - "X et al. observed correlation; here we establish causation..."

如果 PARTIAL OVERLAP → 明确你的增量贡献：
  - "Unlike previous studies that..., we..."
  - "Previous work focused on X; here we reveal Y..."

如果 NO OVERLAP → 可以声称 novel，但要保守：
  - "To our knowledge, this is the first demonstration that..."
  - (加上 "in this system" 限定，不要泛化到整个领域)
```

## 输出格式

```markdown
# 🔎 新颖性验证报告: {假说}
> 搜索时间: {timestamp} | 搜索源: {sources} | 总命中: {N}

## 📊 重叠总览

| 重叠度 | 数量 | 行动 |
|--------|------|------|
| 🔴 HIGH | {N} | Pivot or reframe |
| 🟡 PARTIAL | {N} | Differentiate |
| 🟢 NONE | {N} | Claim novelty |

## 🔴 高度重叠（最接近的已有工作）

### #1: {title}
- **来源**: {journal}, {year}
- **URL**: {link}
- **他们做了什么**: {summary}
- **与你假说的重叠**: {specific_overlap}
- **差异点**: {difference}
- **应对**: {action}

## 🟡 部分重叠

| # | 标题 | 重叠点 | 差异点 | 你的定位 |
|---|------|--------|--------|---------|
| ... | ... | ... | ... | ... |

## ✅ 新颖性声明建议

基于以上分析，你的论文可以声明：

**推荐版本（保守且有据）:**
> "While the role of ROS in carbon dot-mediated cytotoxicity has been reported, the specific involvement of mitochondrial lipid peroxidation and ferroptotic cell death remains uncharacterized. Here we demonstrate that..."

**避免的声称:**
> ~~"This is the first study to..."~~ (太强，容易被 challenge)
> ~~"Carbon dots have never been shown to..."~~ (很可能有中文文献)

## ⚠️ 特别提醒

- 检查了中文文献吗？（CNKI/万方）——英文搜索经常会漏掉中文工作
- 检查了预印本吗？——可能比你早 6 个月
- 检查了专利吗？—— Google Patents/WIPO
