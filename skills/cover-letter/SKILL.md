---
name: cover-letter
description: "针对目标期刊自动生成定制 Cover Letter。突出新颖性+匹配度+无利益冲突。P3 技能。"
version: 1.0.0
author: Academic GStack
tags: [research, cover-letter, submission, publishing, AI4S]
---

# Cover Letter — 投稿信定制师

> Editor 用 30 秒决定送审还是 desk reject。
> 你的 Cover Letter 是这 30 秒里唯一的武器。

## 触发条件

- Journal Matcher 推荐目标期刊后
- 论文定稿准备投稿前
- 用户说"帮我写个 cover letter"

## 输入

1. 📄 **论文信息**（必需）— 标题、Abstract、核心发现
2. 🎯 **目标期刊**（必需）— 期刊名称
3. 🧠 **Journal Matcher 报告**（推荐）— 为什么匹配这个期刊

## Cover Letter 结构

### Paragraph 1: 投稿声明 + 标题

```
Dear Editor,

We are pleased to submit our manuscript entitled
"{MANUSCRIPT_TITLE}"
for consideration for publication in {JOURNAL_NAME}.

一句话说明为什么投这个期刊（不超过 20 字）:
"{This work aligns with {Journal}'s focus on...}"
或
"{Recent publications in {Journal} on {topic} make this a natural fit.}"
```

### Paragraph 2: 研究背景 + 知识空白

```
{领域背景 1-2 句}

However, {知识空白——什么还不知道}.
```

### Paragraph 3: 我们做了什么 + 核心发现

```
Here, we {方法概括} and demonstrate that {核心发现}.

Our key findings include:
(i) {finding_1}
(ii) {finding_2}
(iii) {finding_3}
```

### Paragraph 4: 为什么重要

```
这个发现的意义（对领域/对应用）

{1-2 句，呼应期刊的 scope 和读者群}

This work provides {contribution} and opens new avenues for {future_directions}.
```

### Paragraph 5: 声明

```
We confirm that:
- This manuscript has not been published and is not under consideration elsewhere.
- All authors have read and approved the final version.
- The authors declare no competing financial interests.
- {如果有推荐审稿人，这里提}
- {如果有要排除的审稿人，这里提（附理由）}
```

### Paragraph 6: 结尾

```
We believe our findings will be of broad interest to the readership of {JOURNAL}.
We look forward to your consideration.

Sincerely,
{Corresponding Author Name}
{Affiliation}
{Email}
```

## 期刊特定策略

| 期刊类型 | 强调什么 | 避免什么 |
|---------|---------|---------|
| Nature/Science/Cell | 突破性、广泛兴趣 | 过多技术细节 |
| 子刊 (Nature Comm等) | 坚实性、方法学严格 | 过度声称突破 |
| 领域顶刊 (JACS等) | 领域内的重要性 | 对其他领域讲太多 |
| 专业期刊 | 方法学/数据的可靠性 | 空洞的"广泛兴趣" |

## 输出格式

完整的 Cover Letter 文本，可直接复制粘贴到投稿系统。

附加输出：
- 推荐审稿人列表（3-5 人，附理由）
- 如需排除审稿人，提供理由模板
