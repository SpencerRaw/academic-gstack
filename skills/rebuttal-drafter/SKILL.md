---
name: rebuttal-drafter
description: "逐条分析审稿意见，生成回复策略+反驳草稿+修改对照表。P3 技能。"
version: 1.0.0
author: Academic GStack
tags: [research, rebuttal, peer-review, revision, AI4S]
---

# Rebuttal Drafter — 审稿回复策略师

> 审稿意见不是攻击——是免费的论文改进建议。
> 会回复的人：Major Revision → Accepted。不会回复的人：Major Revision → Rejected。

## 触发条件

- 收到审稿意见后
- 用户说"帮我回复审稿人"
- Peer Reviewer 给出了修改建议需要对照

## 输入

1. 📋 **审稿意见**（必需）— 完整的 reviewer comments
2. 📄 **论文初稿**（必需）— 被审的版本
3. 🎯 **期刊 + Editor 决定**（推荐）— Major/Minor Revision

## 三步策略

### Step 1: 意见分类

```
对每条审稿意见分类：

🟢 EASY WIN — 简单修改，马上做
  - 补充引用、修改措辞、增加 clarification
  - 策略: "We thank the reviewer. We have [done X]. The revised text reads: ..."

🟡 SUBSTANTIVE — 需要额外分析/实验
  - 补充统计分析、增加对照实验、深入讨论
  - 策略: "We appreciate this suggestion. To address this, we have [done Y]."

🔴 CHALLENGING — 质疑核心发现
  - 对方不同意你的解释、质疑方法学、要求新实验
  - 策略: 提供证据 + 礼貌但坚定地解释你的立场

⚫ IMPOSSIBLE — 技术上不可行
  - 要求你做不切实际的实验、超出范围
  - 策略: 解释为什么不可行 + 提供替代方案
```

### Step 2: 逐条回复

```
对每条审稿意见 (Reviewer #N, Comment #M):

Original Comment:
"{原文}"

Our Response:
1. 感谢（必须有）
2. 我们做了什么修改（具体在文中哪一行）
3. 为什么这样做（简短论证）
4. 修订后文本（如适用）

如果是 CHALLENGING 意见:
- 先 agree on something（减少对抗感）
- 然后 explain your position（用证据）
- 最后 propose a middle ground
```

### Step 3: 修改对照表

```
| 意见 # | 审稿人 | 意见摘要 | 修改位置 | 修改类型 |
|--------|--------|---------|---------|---------|
| 1-1 | #1 | 补充 X 引用 | Introduction L45-50 | Text |
| 1-2 | #1 | 重新分析 Y | Fig 3, Results L120-140 | Data |
| 2-1 | #2 | 补充 Z 对照实验 | New Fig S4 | Experiment |
| ... | ... | ... | ... | ... |
```

## 回复语气指南

### 正面语气 ✅

```
✅ "We thank the reviewer for this insightful comment."
✅ "This is an excellent point. We have now..."
✅ "We agree with the reviewer that... We have therefore..."
✅ "The reviewer raises an important question. To address it, we..."
✅ "We appreciate this suggestion. The revised manuscript now includes..."
```

### 要避免 ❌

```
❌ "The reviewer is wrong." → "We respectfully offer a different interpretation."
❌ "We already did that." → "As noted in the original manuscript (Line X)..."
❌ "This is beyond the scope." → "While this is an interesting direction, we focused here on..."
❌ 直接说 "No." → 永远不要说 No。说 "We considered this approach but..."
```

## 特殊情况处理

### 两个审稿人意见矛盾

```
"Reviewer 1 suggested X while Reviewer 2 suggested Y. We carefully considered both perspectives and decided to {your_decision} because {reason}. We have noted Reviewer 2's suggestion as a future direction."
```

### Editor 要求 shortening

```
列出每个 section 可以删除/压缩的内容，不牺牲核心信息。目标是 cut 10-15%。
```

### 审稿人要求的新实验无法完成

```
"We agree that experiment X would provide valuable additional evidence. However, {reason: equipment unavailable / time constraint / cell line unavailable}. To address the reviewer's underlying concern about {the_concern}, we have instead {alternative_approach}."
```

## 输出格式

```markdown
# 📝 审稿回复策略: {论文标题}
> 期刊: {journal} | 决定: {decision} | 审稿人: {N} | 总意见: {M} 条

## 📊 意见分类

| 类型 | 数量 | 策略 |
|------|------|------|
| 🟢 EASY WIN | {N} | 直接修改 |
| 🟡 SUBSTANTIVE | {N} | 补充分析/实验 |
| 🔴 CHALLENGING | {N} | 礼貌辩论 |
| ⚫ IMPOSSIBLE | {N} | 解释+替代 |

## 🔴 最需要关注的意见

{Top 3 最可能决定接受/拒绝的意见 + 回复策略}

---

## Response to Reviewer #1

### Comment 1-1: {summary}

**Original Comment:**
> {原文}

**Our Response:**
{回复}

*Changes: Line {X}-{Y}*

### Comment 1-2: ...

---

## Response to Reviewer #2
{同上}

---

## Response to Reviewer #3
{同上}

---

## 📋 修改对照表

| 意见 # | 修改位置 | 修改类型 | 状态 |
|--------|---------|---------|------|
| 1-1 | Intro L45-50 | Text | ✅ 完成 |
| 1-2 | Fig 3 | Data | 🔄 进行中 |
| ... | ... | ... | ... |

---

## 📨 Cover Letter to Editor

{Dear Editor, 感谢+概述修改}
```

## 注意事项

- 每条回复必须以感谢开头——不是虚伪，是职业规范
- 不要在回复里引入新错误（修改数据时特别注意）
- 回复长度与意见严重性成正比——EASY WIN 一句带过，CHALLENGING 多写论证
- 所有页面/行号引用在最终提交前重新核对
- Editor 会读你的回复——不要把 Editor 当傻子
