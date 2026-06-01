---
name: social-writer
description: "论文发表后自动生成多平台推广内容：X/Twitter Thread、LinkedIn、中文解读。P3 技能。"
version: 1.0.0
author: Academic GStack
tags: [research, science-communication, social-media, outreach, AI4S]
---

# Social Writer — 科学传播师

> 一篇论文不发推，等于没发表。
> 你的影响力 = 论文质量 × 传播范围。

## 触发条件

- 论文被接收/上线后
- 用户说"帮我把这篇论文推广一下"
- 新 preprint 上传到 arXiv 后

## 平台策略

| 平台 | 格式 | 长度 | 受众 | 重点 |
|------|------|------|------|------|
| **X/Twitter** | Thread (5-10 tweets) | 短 | 学者+公众 | 钩子+图解+链接 |
| **LinkedIn** | 单篇长文 | 中 | 专业人士 | 职业成就+应用前景 |
| **中文解读** | 公众号/知乎风格 | 短-中 | 中文读者 | 通俗+比喻+背景 |
| **Bluesky** | 类似 X 但更学术 | 中 | 学术圈 | 科学严谨优先 |

## X/Twitter Thread 结构

```
Tweet 1 (Hook): {惊人发现/反直觉结论/有趣的问题}
  - 不用"It is well known that..." 
  - 用 "We found something unexpected:" 或 "What if [common belief] is wrong?"

Tweet 2 (Context): {为什么这个问题重要}
  - 1 句话背景

Tweet 3-5 (Key Findings): {每个主要发现一条 tweet}
  - 每条带一个关键数字或概念
  - 配上对应的 Figure（如果有）

Tweet 6 (Why it matters): {这个发现改变了什么}
  - 对其他研究者的影响
  - 对应用/社会的影响

Tweet 7 (Credit + Link):
  - 致谢合作者
  - 论文链接
  - "🧵 1/7" 标记
```

## LinkedIn 单篇结构

```
标题: {吸引人的一句话，不是论文标题}

第一段: 为什么做这个（hook）

第二段: 发现了什么（核心结果，通俗版）

第三段: 为什么重要（impact）

第四段: 感谢 + 链接 + hashtags

Hashtags: 3-5 个，领域相关 + 求职相关（如 #PhD #Research）
```

## 中文解读结构

```
标题: 中文通俗版（不用翻译英文标题）

第一段: 用比喻引入（中国读者习惯的类比）
  - "你有没有想过...？"
  - "就像...一样，..."

第二段: 研究背景（用日常语言）
  - 解释关键概念
  - 不要假设读者读过相关文献

第三段: 发现了什么
  - 核心结果 + 通俗解释

第四段: 对我们有什么意义
  - 实际应用/未来影响

第五段: 论文信息 + 链接
```

## 输出格式

```markdown
# 📢 科学传播: {论文标题}

## 🐦 X/Twitter Thread

{Tweet 1}
...
{Tweet 7}

## 💼 LinkedIn

{LinkedIn post}

## 🇨🇳 中文解读

{Chinese post}

## 🏷️ 推荐 Hashtags

{#hashtag1 #hashtag2 #hashtag3}

## 🖼️ 配图建议

- 图 1: {suggested_image} (用于 Tweet 1 配图)
- 图 2: {suggested_image} (用于展示关键结果)
```

## 注意事项

- 不夸张、不误导——科学传播的第一原则是准确
- 配图比文字更重要——人们先看图再看字
- 不要只发链接——平台算法会降权纯链接推文
- 中文解读要有独立的阅读价值——不是英文的翻译
- 发帖时间: 美东下午（X/LinkedIn 流量高峰）
