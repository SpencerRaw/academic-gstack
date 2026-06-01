# Academic GStack — 技术方案

> 如何用 Hermes Agent 生态实现一个学术版 gstack

---

## 架构总览

```
┌──────────────────────────────────────────────────────┐
│                   Science CEO（你）                    │
│         设定方向 → CHECKPOINT 判断 → 下一轮           │
├──────────────────────────────────────────────────────┤
│                  Academic GStack 调度层                │
│              maestro + kanban + cron                   │
├──────────┬──────────┬──────────┬──────────────────────┤
│ 战略层   │ 执行层   │ 产出层   │ 运营层               │
│ PI       │ Lit      │ Paper    │ Lab Manager          │
│ Strategy │ Hypo     │ Peer     │ Lit Monitor          │
│ Grant    │ Method   │ Journal  │ Social Writer        │
│          │ Data     │ Grant    │ Archivist            │
│          │ Figure   │ Rebuttal │                      │
│          │ Novelty  │          │                      │
├──────────┴──────────┴──────────┴──────────────────────┤
│                   底层能力                              │
│   Co-Scientist ←→ SciDAO ←→ CD Foundation Model       │
│   Hermes skills ←→ delegate_task ←→ cron              │
└──────────────────────────────────────────────────────┘
```

---

## 实现方式：Hermes Skill 体系

每个 agent 角色 = 一个 Hermes Skill。好处：
1. 自然加载到会话中（`/skill lit-reviewer`）
2. 可以被 cron job 自动调用
3. 可以被 delegate_task 并行分发
4. 可以被 darwin-skill 持续进化
5. 跨 session 持久化

### Skill 目录结构

```
~/.hermes/skills/academic-gstack/
├── lit-reviewer/SKILL.md          # 文献检索 + 分类 + 假说提取
├── hypothesis-generator/SKILL.md  # 假说生成 + 辩论排名
├── method-designer/SKILL.md       # 实验方案设计
├── data-analyst/SKILL.md          # 数据分析 + 统计
├── data-qa/SKILL.md               # 数据质量审计
├── figure-artist/SKILL.md         # 图表自动生成
├── novelty-checker/SKILL.md       # 新颖性全网搜索
├── paper-drafter/SKILL.md         # 论文初稿
├── peer-reviewer/SKILL.md         # 模拟审稿
├── journal-matcher/SKILL.md       # 期刊推荐
├── grant-writer/SKILL.md          # 基金申请
├── cover-letter/SKILL.md          # Cover letter
├── rebuttal-drafter/SKILL.md      # 审稿回复
├── pi-reviewer/SKILL.md           # PI 战略审查
├── lab-strategist/SKILL.md        # 多课题调度
├── grant-scout/SKILL.md           # 基金机会监控
├── lit-monitor/SKILL.md           # 新论文推送
├── social-writer/SKILL.md         # 社交媒体推广
├── lab-archivist/SKILL.md         # 知识库管理
└── lab-manager/SKILL.md           # 日常看板
```

---

## 核心流水线

### Pipeline 1: 假说 → 实验方案（睡前跑，醒来收）

```
cron: 每晚 23:00 触发
    │
    ▼
delegate_task (并行 3 个)
    ├── lyq-agent:
    │   /skill lit-reviewer → 搜索 PCD+碳点最新文献
    │   /skill hypothesis-generator → 基于文献 + 已有数据生成假说
    │   /skill method-designer → 为 Top 3 假说设计验证实验
    │   /skill novelty-checker → 验证假说新颖性
    │   输出 → lyq 假说报告.md
    │
    ├── yx-agent:
    │   同上流程，但针对 IDR+chromatin
    │   输出 → yx 假说报告.md
    │
    └── bxt-agent:
        同上流程，但针对 NIR+horticulture
        输出 → bxt 假说报告.md
```

### Pipeline 2: 数据 → 论文初稿

```
delegate_task:
    /skill data-analyst → 统计分析 + 可视化
    /skill data-qa → 审计数据完整性
    /skill figure-artist → 生成发表级图表
    /skill paper-drafter → 写初稿
    /skill peer-reviewer → 模拟 3 个审稿人给意见
    /skill journal-matcher → 推荐目标期刊
```

### Pipeline 3: 投稿 → 修订

```
delegate_task:
    /skill cover-letter → 针对目标期刊生成
    [投稿，等审稿意见]
    /skill rebuttal-drafter → 逐条分析 → 回复策略
```

---

## 技术选型

### 调度层

| 组件 | 用途 | 为什么 |
|------|------|--------|
| `delegate_task` | 并行 agent 执行 | Hermes 内置，自动管理 session 隔离 |
| `cronjob` | 睡前启动定时任务 | 持久化调度，跨 session |
| `kanban` (maestro) | 三课题看板 | 可视化进度，知道每个课题在哪个阶段 |

### Agent 层

| 组件 | 用途 |
|------|------|
| Co-Scientist | 假说生成 + 辩论引擎（~88% 论文还原度） |
| CD Foundation Model | 碳点领域专用模型，提供领域知识 |
| DeepSeek / Claude | 通用 LLM 驱动每个 agent 角色 |

### 知识层

| 组件 | 用途 |
|------|------|
| SciDAO | 社区验证 + 众包反馈 |
| Obsidian vault | 个人知识管理 |
| `~/.hermes/sessions/` | 所有 agent 会话记录 |

---

## 数据流

```
用户输入（自然语言一句话方向）
    │
    ▼
Lab Strategist 拆解成子任务
    │
    ├──→ Lit Reviewer（文献检索）
    │       │
    │       ▼
    ├──→ Hypothesis Generator（假说生成）
    │       │
    │       ▼
    ├──→ Method Designer（实验方案）
    │       │
    │       ▼
    │   [== CHECKPOINT: 你判断是否跑实验 ==]
    │       │
    │       ▼
    ├──→ Data Analyst（数据分析）
    │       │
    │       ▼
    ├──→ Figure Artist（图表生成）
    │       │
    │       ▼
    ├──→ Paper Drafter（初稿写作）
    │       │
    │       ▼
    ├──→ Peer Reviewer（模拟审稿）
    │       │
    │       ▼
    │   [== CHECKPOINT: 你修改定稿 ==]
    │       │
    │       ▼
    └──→ Submit Engineer（投稿）
```

---

## 关键设计决策

### 1. 为什么不自己做实验？

Agent 不跑湿实验。但 Agent 可以：
- 设计实验方案（protocol、样本量、对照组）
- 生成实验记录模板
- 分析实验数据
- 发现数据中的异常/新现象

人做实验，AI 做脑力劳动。

### 2. 为什么要并行三个课题？

单线程跑一个课题：
- 等实验结果 → 空闲
- 等审稿 → 空闲
- 等试剂 → 空闲

三线程并行：A 在分析数据时，B 在搜文献，C 在写初稿。时间利用率 ×3。

### 3. 为什么每个课题都要有"蛋白电路延伸版"？

你做碳点 → 发碳点论文 → 只能找碳点博后。
你做碳点 + 把它延伸到蛋白电路 → 能找蛋白电路博后 → Caltech Elowitz。

每个课题的延伸版是你的差异化武器。

---

## 优先级排序

| 优先级 | 角色 | 理由 |
|--------|------|------|
| 🔴 P0 | Lit Reviewer | 所有下游依赖文献输入 |
| 🔴 P0 | Hypothesis Generator | 核心价值：假说即产品 |
| 🔴 P0 | Peer Reviewer | 最高杠杆：审稿意见 = 被拒率 ↓ |
| 🟡 P1 | Paper Drafter | 减少 80% 写作时间 |
| 🟡 P1 | Data Analyst | 统计错误是拒稿头号原因 |
| 🟡 P1 | Journal Matcher | 投错期刊浪费 3-6 个月 |
| 🟢 P2 | Figure Artist | 好图 = 引用率 ↑ |
| 🟢 P2 | Grant Writer | 基金 = 自由 = 创业资本 |
| 🟢 P2 | Social Writer | 学术个人品牌建设 |
| 🔵 P3 | Lit Monitor | 被动信息流 |
| 🔵 P3 | Lab Manager | 锦上添花 |

---

## 下一步行动

1. **本周**：写完 P0 三个 skill（Lit Reviewer + Hypothesis Generator + Peer Reviewer）
2. **本周**：设置第一个 cron job（每晚自动文献检索）
3. **2周内**：P0+P1 全部就位，lyq 课题跑通完整流水线
4. **1个月**：三课题并行，每天睡前启动、醒来收三份报告
