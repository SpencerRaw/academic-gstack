---
name: ac-gstack-pipeline
description: "Academic GStack 夜间科研流水线：串联 Lit Reviewer → Hypothesis Generator → PI Reviewer，输出三课题假说日报。每日 cron 自动触发。"
version: 1.0.0
author: Academic GStack
tags: [research, pipeline, automation, cron, AI4S]
---

# Academic GStack Pipeline — 夜间科研流水线

> 睡前一句话，醒来三份假说报告等着你。
> 这是 Academic GStack 的核心引擎。

## 触发方式

- **自动**：cron job 每日定时触发
- **手动**：`/skill ac-gstack-pipeline` + 指定课题
- **单课题**：`/skill ac-gstack-pipeline 课题=lyq`

## Pipeline 架构

```
输入: 三个课题方向（一句话）

┌─────────────┐
│ lyq: 碳点PCD │──→ Lit Reviewer ──→ Hypothesis Generator ──→ ┐
│ 光诱导肿瘤   │      (文献检索)       (假说+辩论+排名)         │
└─────────────┘                                               │
                                                              ├──→ PI Reviewer ──→ 报告
┌─────────────┐                                               │    (战略审查)
│ yx: IDR+    │──→ Lit Reviewer ──→ Hypothesis Generator ──→ ┤
│ chromatin   │                                              │
└─────────────┘                                              │
                                                              │
┌─────────────┐                                               │
│ bxt: NIR+   │──→ Lit Reviewer ──→ Hypothesis Generator ──→ ┘
│ 植物光调控  │
└─────────────┘

输出: 三份假说日报 + 一份调度建议
```

## 执行步骤

### Step 0: 读取课题配置

从 memory 和 goals-and-milestones 中读取当前三课题状态：

```
lyq: 碳点光诱导细胞死亡(PCD)肿瘤治疗。关键词: carbon dots, photodynamic therapy, 
     PCD, ferroptosis, pyroptosis, apoptosis, ROS, tumor
     设备: 共聚焦、流式细胞仪
     死线: 下周 demo

yx:  转录因子IDR与染色质互作。关键词: intrinsically disordered region, 
     transcription factor, chromatin recognition, phase separation, 
     biomolecular condensates
     
bxt: NIR碳点植物光调控。关键词: carbon dots, NIR, plant photobiology, 
     light regulation, horticulture, photosynthesis, LED
```

### Step 1: 并行文献检索

对三个课题同时启动 Lit Reviewer（用 delegate_task 并行）：

```
delegate_task(tasks=[
  {goal: "lit-review for lyq PCD carbon dots...", skills: ["lit-reviewer"]},
  {goal: "lit-review for yx IDR chromatin...", skills: ["lit-reviewer"]},
  {goal: "lit-review for bxt NIR plant...", skills: ["lit-reviewer"]},
])
```

### Step 2: 并行假说生成

拿到三份 Lit Reviewer 报告后，同时启动 Hypothesis Generator：

```
delegate_task(tasks=[
  {goal: "hypothesis-generation for lyq...", skills: ["hypothesis-generator"]},
  {goal: "hypothesis-generation for yx...", skills: ["hypothesis-generator"]},
  {goal: "hypothesis-generation for bxt...", skills: ["hypothesis-generator"]},
])
```

### Step 3: 战略审查 + 调度

拿到三份假说报告后，启动 PI Reviewer + Lab Strategist：

```
1. 对每个课题跑 PI Reviewer（Hold Scope 模式）
2. 跑 Lab Strategist 生成今日兵力分配
```

### Step 4: 生成日报

汇总所有输出为一份日报，格式见下方。

## 输出格式（日报）

```markdown
# 🌅 科研日报: {date}
> 睡前启动 · 醒来收货 | Academic GStack Pipeline

---

## 🔴 lyq: 碳点PCD光诱导肿瘤细胞死亡

### 📚 文献更新
- 检索到 {N} 篇新论文，其中 {M} 篇高度相关
- 最重要发现: {one_sentence}

### 🧠 推荐假说 Top 1
**{hypothesis_title}**
{核心机制一句话}

验证实验: {one_experiment}
蛋白电路延伸: {extension_or_"暂无"}

### 🎯 PI 判断
{继续/调整/缩小} — {理由一句话}

---

## 🟡 yx: 转录因子IDR-染色质识别

{同上结构}

---

## 🟢 bxt: NIR碳点园艺

{同上结构}

---

## 🗺️ 今日调度建议

| 时段 | 任务 | 课题 | 为什么 |
|------|------|------|--------|
| 上午 | {task} | {project} | {reason} |
| 下午 | {task} | {project} | {reason} |

---

## ⚠️ 预警

- {alert_1}
- {alert_2}

---

> 🤖 此报告由 Academic GStack Pipeline 自动生成
> 下次运行: 今晚 23:00
```

## Cron 配置

```bash
hermes cron create "0 23 * * *" \
  --name "ac-gstack-nightly-pipeline" \
  --prompt "加载 ac-gstack-pipeline skill。运行完整夜间科研流水线：对 lyq(碳点PCD)、yx(IDR+chromatin)、bxt(NIR植物) 三个课题依次执行 Lit Reviewer → Hypothesis Generator → PI Reviewer → Lab Strategist。生成日报。" \
  --skills "ac-gstack-pipeline" \
  --deliver "telegram" \
  --enabled_toolsets "web,terminal,file,skills,delegation,memory"
```

## 单课题手动触发

```
/skill ac-gstack-pipeline 课题=lyq
```

只对 lyq 跑完整流水线。

## 注意事项

- Pipeline 在 cron 环境下运行，不能依赖当前会话上下文
- 每个 delegate_task 的子 agent 只加载需要的 skill，减少 token 消耗
- 如果某课题文献检索为 0 篇，扩展检索词后重试一次，仍为 0 则标注"文献不足"并跳过后续步骤
- 日报通过 Telegram 推送到你手机上——醒来直接看
- 如果 cron 因 API 限额失败，第二天自动重试（只跑失败的课题）
