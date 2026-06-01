---
name: paper-drafter
description: "基于数据+假说+图表自动生成论文初稿：Abstract→Intro→Results→Discussion→Methods。P1 核心技能。"
version: 1.0.0
author: Academic GStack
tags: [research, paper-writing, manuscript, drafting, AI4S]
---

# Paper Drafter — 论文初稿写作器

> 你不是在"写论文"——你是在把数据翻译成学术叙事。
> 80% 的写作时间应该省掉。你只做最后的打磨。

## 触发条件

- 数据分析完成 + 图表就绪后
- 用户说"帮我写这篇论文"或"开始写初稿"
- 用户提供数据/图表 + 目标期刊

## 输入

1. 📊 **Data Analyst 报告**（推荐）— 统计分析结果 + 效应量
2. 🎨 **Figure Artist 输出**（推荐）— 图表 + 图注草稿
3. 🧠 **Hypothesis Generator 报告**（推荐）— 假说 + 文献依据
4. 🎯 **目标期刊**（推荐）— 影响结构格式
5. 📄 **已有笔记/草稿**（可选）— 任何已有文本

## 工作流：五段式写作

### Section 1: Abstract（最后写，但先规划）

```
结构（≤250 words）：
1. Background (1-2句): 领域背景 + 知识空白
2. Objective/Hypothesis (1句): 我们想回答什么问题
3. Methods summary (1-2句): 用了什么方法
4. Key Results (2-3句): 最重要的发现 + 关键数字
5. Conclusion/Implication (1句): 这个发现意味着什么

原则：
- 每个句子承载一个信息
- 数字比形容词有说服力（"3.2-fold increase" > "significant increase"）
- 不出现"we believe" "might" "could possibly"——用"demonstrate" "show" "indicate"
```

### Section 2: Introduction（三段式）

```
Paragraph 1: 大背景
- 这个领域为什么重要？（1-2句）
- 当前的知识状态是什么？（1-2句）

Paragraph 2: 知识空白
- 什么问题没解决？（1句）
- 为什么现有方法/模型不够？（1-2句）
- 解决这个问题的重要性（1句）

Paragraph 3: 本文贡献
- 我们做了什么？（1句概括）
- 我们发现了什么？（1句概括核心结果）
- 这个发现的意义（1句）
```

### Section 3: Results

```
对每个 figure/table：

结构：
1. 引导句: "To investigate whether X affects Y, we..."
2. 实验描述（1-2句，不是抄 Methods）
3. 结果陈述: "We observed that..." + 关键数据
4. 统计支持: "(p < 0.01, Cohen's d = 1.2)"
5. 解读桥接: "This suggests that..." (为 Discussion 铺垫)

原则：
- 一个段落 = 一个实验 = 一个发现
- 先给结论，再给数据（"X increased Y by 3-fold (Figure 1A)"）
- 数字放在句子中间或后面，不是开头
- 不要在 Results 里过度解读——那是 Discussion 的工作
```

### Section 4: Discussion（漏斗式）

```
Paragraph 1: 核心发现重述
- 我们证明了什么？（不要复制 Abstract，换种说法）
- 最强证据是什么？

Paragraph 2-N: 逐发现讨论
- 每个核心发现：与已有文献比较
- 一致的地方："Consistent with previous studies..."
- 不一致的地方："In contrast to X et al., we found..."
- 为什么不一致？（方法差异？条件差异？）

Paragraph 倒数第二: 局限性
- 诚实但不过度（3-5条）
- 每条局限性跟一句"future work will address this by..."
- 不要写"more research is needed"——太弱

Paragraph 最后: 结论与展望
- 1-2句总结
- 具体展望（命名具体实验，不是泛泛而谈）
```

### Section 5: Methods

```
标准子节：
1. Materials（试剂、来源、纯度）
2. Experimental Design（总体设计）
3. 每个实验方法（按 Results 出现顺序）
4. Statistical Analysis（检验方法、软件、显著性阈值）
5. Data Availability

风格：
- 过去式、被动语态或 "We..."
- 足够详细让同行能复现
- 引用已有 protocol 而不是重写
```

## 输出格式

```markdown
# 📝 论文初稿: {working_title}
> 生成时间: {timestamp} | 目标期刊: {target_journal} | 字数: {word_count}

## 📋 Abstract

{abstract_text}

---

## 📖 Introduction

{introduction_text}

---

## 📊 Results

### {finding_1_title}
{results_text_1}

### {finding_2_title}
{results_text_2}

...

---

## 💬 Discussion

{discussion_text}

---

## 🔬 Methods

### Materials
...

### Experimental Design
...

### Statistical Analysis
...

---

## 📎 Figure Legends

**Figure 1**: {legend}
**Figure 2**: {legend}
...

---

## 🔗 References

{如果从 Lit Reviewer 报告提取，自动填入最相关的 20-30 篇}

## ⚠️ 标注待补充

以下部分需要你手动补充：
- [ ] {missing_item_1}
- [ ] {missing_item_2}
```

## 期刊格式适配

根据目标期刊自动调整：

| 期刊类型 | Abstract 限制 | 结构要求 | 引用风格 |
|---------|-------------|---------|---------|
| Nature/Science | 150 words | 连续段落 | 数字上标 |
| Cell | 150 words | 结构化(Background/Results/Conclusions) | (Author, Year) |
| JACS/Angew | 无字数限制 | 连续段落 | 数字上标 |
| Nature Comm | 150 words | 连续段落 | 数字上标 |
| ACS Nano | ~200 words | 连续段落 | 数字上标 |
| eLife | ~300 words | 连续段落 | (Author, Year) |

## 注意事项

- **不要编造数据**——所有数字必须来自数据文件或 Data Analyst 报告
- **不要编造引用**——引用必须来自 Lit Reviewer 报告中的真实论文
- 如果某些部分数据不足（如缺少某个对照实验），明确标注"待补充"而不是硬编
- 初稿不需要完美——目标是让你只需要改而不是重写
- 用拼写检查过一遍再给你——低级错误会破坏信心
- 中文论文同理——结构相同，表达习惯不同（中文更含蓄，英文更直接）
