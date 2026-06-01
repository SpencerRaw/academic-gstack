# Academic GStack — 一人实验室的操作系统

> [English](README.md) | [中文版](README.zh-CN.md)

> "从去年12月起，我大概一行代码都没打过。"
> — Andrej Karpathy
>
> 未来的 PI 不亲自做实验、不亲自写初稿、不亲自画图。
> 他们只做判断。AI agent 团队包揽剩下的。

**Academic GStack** 把 [Garry Tan 的 gstack](https://github.com/garrytan/gstack) 哲学应用到学术研究：gstack 让一个工程师变成一支工程团队，Academic GStack 让一个科研人员变成一所虚拟实验室。

每个学者 = 一个学术个人品牌 startup。
- 你的论文 = 你的产品
- 你的引用量 = 你的用户增长
- 你的 h-index = 你的估值
- 你的实验室 = 你的公司

---

## 核心映射：gstack → Academic GStack

| gstack（软件工程） | Academic GStack（科研） |
|---------------------|------------------------|
| `/office-hours` — 产品方向审讯 | `/lab-meeting` — 课题方向审讯 |
| `/plan-ceo-review` — CEO 范围挑战 | `/pi-review` — PI 视角战略审查 |
| `/plan-eng-review` — 架构锁死 | `/method-review` — 实验方案锁死 |
| `/plan-design-review` — 设计审查 | `/figure-review` — 图表质量审查 |
| `/review` — 代码审查 | `/peer-review` — 模拟同行评审 |
| `/qa` — 浏览器测试 | `/data-qa` — 数据质量审计 |
| `/cso` — 安全审计 | `/novelty-check` — 新颖性验证 |
| `/ship` — 发布工程师 | `/submit` — 投稿工程师 |
| `/retro` — 工程回顾 | `/lab-retro` — 课题回顾 |
| `/codex` — 第二意见 | `/second-opinion` — 独立 AI 同行评审 |
| `/autoplan` — 自动审查流水线 | `/auto-experiment` — 自动实验流水线 |

---

## Agent 角色矩阵（18 个）

### 🧠 战略层
| 角色 | 做什么 |
|------|--------|
| **PI Reviewer** | 范围挑战：这个方向值得追吗？能发什么级别？ |
| **Lab Strategist** | 多课题调度：兵力分配、优先级、死线管理 |
| **Grant Scout** | 匹配基金机会、自动生成申请书初稿 |

### 🔬 执行层
| 角色 | 做什么 |
|------|--------|
| **Lit Reviewer** | 系统检索 + 自动分类 + 提取可检验假说 |
| **Hypothesis Generator** | 基于已知数据生成排名假说 |
| **Method Designer** | 设计实验方案、估算样本量、写 protocol |
| **Data Analyst** | 自动统计、可视化、异常检测、效应量计算 |
| **Data QA** | 审计数据完整性、找漏洞、检验可重复性 |
| **Figure Artist** | 自动生成发表级图表 |
| **Novelty Checker** | 全网搜索验证新颖性，标注已有工作 |

### ✍️ 产出层
| 角色 | 做什么 |
|------|--------|
| **Paper Drafter** | 写初稿：Abstract→Intro→Results→Discussion |
| **Peer Reviewer** | 模拟 3 个审稿人，给修改意见 |
| **Journal Matcher** | 分析论文特征 → 推荐目标期刊 + 命中率估算 |
| **Grant Writer** | 基于论文自动生成基金申请书 |
| **Cover Letter** | 针对目标期刊自动写 cover letter |
| **Rebuttal Drafter** | 逐条分析审稿意见 → 生成回复策略 |

### 🔄 运营层
| 角色 | 做什么 |
|------|--------|
| **Lab Manager** | 多课题状态看板、死线预警、资源冲突检测 |
| **Lit Monitor** | arXiv/bioRxiv 新论文推送 + 相关性评分 |
| **Social Writer** | 自动生成 Twitter/X thread + LinkedIn + 中文科普 |
| **Lab Archivist** | 自动整理实验记录、代码、数据到结构化知识库 |

---

## 工作流：从想法到发表

```
Think ──→ Plan ──→ Experiment ──→ Analyze ──→ Write ──→ Review ──→ Submit ──→ Reflect
  想法      方案       实验          分析         写作       审稿        投稿        复盘
  │          │          │             │           │          │           │           │
/lab-    /method-   自动实验      /data-     /paper-   /peer-     /submit   /lab-
meeting  review                  analysis   draft     review     +cover    retro
  │          │          │             │           │          │           │
/pi-     /method-   /data-qa      /figure-   /peer-    /journal-  /social-
review   review     审计          artist     review    match      writer
                     │             │           │
                 你判断 CHECKPOINT          你判断 CHECKPOINT
```

---

## 当前开发状态

- [x] 设计文档完成（18 个角色定义 + 完整工作流）
- [x] P0 技能开发完成（Lit Reviewer / Hypothesis Generator / Peer Reviewer）
- [x] 战略层技能完成（PI Reviewer / Lab Strategist）
- [x] Pipeline 引擎完成（ac-gstack-pipeline + cron）
- [x] 端到端部署完成（Hermes Skills + 夜间定时任务）
- [ ] P1 技能开发（Paper Drafter / Data Analyst / Journal Matcher）
- [ ] 公开文档 + 使用教程

---

## 技术栈

- **Agent 框架**: [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- **科学引擎**: Co-Scientist（假说生成 + 辩论）
- **编排层**: maestro（多 agent 任务分发）
- **调度**: cron + delegate_task

---

## 灵感来源

- [Garry Tan's gstack](https://github.com/garrytan/gstack) — 一人工程团队的哲学
- [Andrej Karpathy](https://github.com/forrestchang/andrej-karpathy-skills) — AI 辅助编程的四条规则
- [Science CEO 方法论](https://github.com/SpencerRaw/academic-gstack/tree/main/docs) — 从实验员到科研指挥家

---

MIT License · 构建中 🏗️
