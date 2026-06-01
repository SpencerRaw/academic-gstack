---
name: lit-monitor
description: "持续监控 arXiv/bioRxiv 新论文，按相关性评分推送。每周自动运行。P2 技能。"
version: 1.0.0
author: Academic GStack
tags: [research, literature-monitoring, arxiv, biorxiv, alerting, AI4S]
---

# Lit Monitor — 文献监控器

> 你不知道你不知道什么——直到有人发表了。
> 持续扫描新论文，确保你永远比审稿人更早知道领域动态。

## 触发条件

- Cron job 每周自动触发（推荐每周一和周四）
- 用户说"最近有什么新论文？"
- 投稿前检查（确认没有刚发表的相关论文）

## 输入

1. 📋 **监控关键词列表**（必需）— 每个课题的检索词
2. 🎯 **课题相关性标准**（推荐）— 什么算"高度相关"
3. 📊 **已有文献库**（推荐）— 用于去重

## 监控源

| 来源 | 覆盖 | 频率 | 特点 |
|------|------|------|------|
| arXiv | 物理/CS/数学/定量生物 | 每日 | 预印本，最早 |
| bioRxiv | 生物 | 每日 | 生物预印本 |
| chemRxiv | 化学 | 每日 | 化学预印本 |
| PubMed | 生物医学 | 每日 | 正式发表+Early Access |
| Google Scholar Alerts | 全领域 | 不定 | 覆盖广但噪声大 |

## 工作流

### Step 1: 检索

```
对每个课题的关键词组合，搜索最近 7 天的新论文：

web_search:
  "{keywords}" site:arxiv.org → 最近1周 → 5篇
  "{keywords}" site:biorxiv.org → 最近1周 → 5篇
  "{keywords}" pubmed → 最近1周 → 5篇

去重（通过标题/DOI）
目标: 每个课题 10-20 篇新论文
```

### Step 2: 快速分类

```
对每篇论文做三分类：

🔴 CRITICAL — 直接竞争/scoop风险
  - 和你的在研课题高度重叠
  - 可能抢在你前面发表
  - 需要立即阅读和应对

🟡 RELEVANT — 相关但不紧急
  - 与课题相关但方向不同
  - 方法可借鉴
  - 领域重要进展

🟢 BACKGROUND — 背景知识
  - 领域新动态
  - 不直接影响当前课题
  - 扩展知识面
```

### Step 3: CRITICAL 论文深度处理

```
对标记为 CRITICAL 的论文:
1. web_extract → 提取摘要/全文
2. 与你的假说对照:
   - 他们证实了你的假说？→ 你需要加快
   - 他们证伪了你的假说？→ 你需要调整方向
   - 他们做了类似的实验？→ 你需要差异化
3. 紧急程度评估:
   - 如果预印本 → 他们的正式发表还有 {estimated_time}
   - 如果已发表 → 你已经晚了，需要调整 story
```

### Step 4: 生成推送

```
生成监控报告 → 推送到 Telegram
```

## 输出格式

```markdown
# 📡 文献监控周报: {date_range}
> 监控关键词: {keywords} | 来源: arXiv, bioRxiv, PubMed

---

## 🔴 CRITICAL（需要立即关注）

### #1: {title}
- **来源**: {source}, {date}
- **URL**: {link}
- **核心发现**: {one_sentence}
- **与你的课题关系**: 
  - ⚠️ 重叠: {他们做了类似的 X}
  - 🏃 时间线: 预印本，预计 {X} 个月后正式发表
  - 🎯 你的应对: {accelerate / differentiate / pivot}

### #2: ...

---

## 🟡 RELEVANT（值得阅读）

| # | 标题 | 来源 | 为什么相关 |
|---|------|------|-----------|
| 1 | {title} | {source} | 方法可借鉴 |
| ... | ... | ... | ... |

---

## 🟢 BACKGROUND（领域动态）

| # | 标题 | 来源 | 一句话 |
|---|------|------|--------|
| 1 | {title} | {source} | ... |
| ... | ... | ... | ... |

---

## 📊 本周统计

```
论文总数:     ██████████ 25
🔴 Critical:   ██ 2
🟡 Relevant:    █████ 5
🟢 Background:  ██████████████ 18
```

## 🏃 Scoop 风险等级

| 课题 | 风险 | 最近竞争论文 | 建议 |
|------|------|------------|------|
| Project A | 🟡 Medium | {N} 篇 | 加速数据分析 |
| Project B | 🟢 Low | 0 篇 | 正常推进 |
| Project C | 🟢 Low | {N} 篇 | 正常推进 |

---

> 🤖 下次监控: {next_run_date}
```

## Cron 配置

```bash
# 每周一和周四推送
hermes cron create "0 8 * * 1,4" \
  --name "ac-gstack-lit-monitor" \
  --prompt "加载 lit-monitor skill。对配置的所有课题进行本周文献监控。搜索 arXiv、bioRxiv、PubMed 的最新论文。生成分类推送。" \
  --skills "lit-monitor" \
  --deliver "telegram" \
  --enabled_toolsets "web,file,skills,memory"
```

## 注意事项

- CRITICAL 判断要保守——不要吓唬用户。只有真正重叠的才标 CRITICAL
- 去重很重要——同一篇论文可能在多个源出现
- 如果某周 0 篇 CRITICAL，不要编造
- "已被 scoop"的判断要非常谨慎，不要轻率下结论
- 你的论文 vs 他们的论文——差异可能比你想象的大
