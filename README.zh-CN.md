# ⚠️ 构建中 (Work in Progress)

> Academic GStack 正在活跃开发中。以下设计文档描述目标架构。
> 当前状态：P0 技能完成，夜间流水线已部署。

---

# Academic GStack — 一人实验室的操作系统

> "I don't think I've typed a line of code probably since December."
> — Andrej Karpathy
>
> 未来的 PI 不亲自做实验、不亲自写初稿、不亲自画图。
> TA 只做判断。AI agent 团队做剩下的。

**Academic GStack** 把 [Garry Tan 的 gstack](https://github.com/garrytan/gstack) 哲学应用到学术研究：gstack 让一个工程师变成一支工程团队，Academic GStack 让一个科研人员变成一所虚拟实验室。

每个学者 = 一个学术个人品牌的 startup。
- 论文 = 产品
- 引用量 = 用户增长
- h-index = 估值
- 实验室 = 公司

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
| `/autoplan` — 自动审查流水线 | `/auto-experiment` — 自动实验流水线 |

---

## Agent 角色矩阵（18 个）

### 🧠 战略层
| 角色 | 做什么 |
|------|--------|
| **PI Reviewer** | 范围挑战：方向值得追吗？能发什么级别？ |
| **Lab Strategist** | 多课题调度：兵力分配、优先级、死线管理 |
| **Grant Scout** | 匹配基金机会、自动生成申请书初稿 |

### 🔬 执行层
| 角色 | 做什么 |
|------|--------|
| **Lit Reviewer** | 系统检索 + 自动分类 + 提取可检验假说 |
| **Hypothesis Generator** | 四角色辩论 + 排名假说 + 验证方案 |
| **Method Designer** | 设计实验方案、估算样本量、写 protocol |
| **Data Analyst** | 自动统计、可视化、异常检测、效应量 |
| **Data QA** | 审计数据完整性、检验可重复性 |
| **Figure Artist** | 自动生成发表级图表 |
| **Novelty Checker** | 全网搜索验证新颖性 |

### ✍️ 产出层
| 角色 | 做什么 |
|------|--------|
| **Paper Drafter** | 写初稿：Abstract→Intro→Results→Discussion |
| **Peer Reviewer** | 模拟 3 个审稿人，给修改意见 |
| **Journal Matcher** | 推荐目标期刊 + 命中率估算 |
| **Grant Writer** | 基于论文自动生成基金申请书 |
| **Cover Letter** | 针对目标期刊自动定制 |
| **Rebuttal Drafter** | 逐条分析审稿意见 → 回复策略 |

### 🔄 运营层
| 角色 | 做什么 |
|------|--------|
| **Lab Manager** | 多课题状态看板、死线预警 |
| **Lit Monitor** | arXiv/bioRxiv 新论文推送 + 相关性评分 |
| **Social Writer** | 自动生成 Twitter/X + LinkedIn + 中文解读 |
| **Lab Archivist** | 自动整理实验记录到结构化知识库 |

---

## 工作流：从想法到发表

```
Think ──→ Plan ──→ Experiment ──→ Analyze ──→ Write ──→ Review ──→ Submit
  │          │          │             │           │          │           │
方向审讯  方案审查   自动实验      数据分析    论文初稿   模拟审稿    投稿
  │          │          │             │           │          │           │
PI审查    方法审查   数据审计      图表生成    同行评审   期刊匹配    推广
                     │             │           │
                 你判断 CHECKPOINT          你判断 CHECKPOINT
```

---

## 当前开发状态

- [x] 设计文档完成（18 角色 + 工作流）
- [x] P0 技能完成（Lit Reviewer / Hypothesis Generator / Peer Reviewer）
- [x] 战略层完成（PI Reviewer / Lab Strategist）
- [x] Pipeline 引擎完成（夜间流水线 + cron）
- [x] 端到端部署完成
- [x] 全部 18 个 skill 完成 (100%)
- [x] 3 个 cron job 活跃
- [ ] 公开文档 + 教程

**18/18 skills 完成 (100%)** 🎉

---

## 技术栈

- **Agent 框架**: [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- **科学引擎**: Co-Scientist（假说生成 + 辩论）
- **编排层**: maestro（多 agent 任务分发）
- **调度**: cron + delegate_task

---

## 灵感来源

- [Garry Tan's gstack](https://github.com/garrytan/gstack) — 一人工程团队
- [Andrej Karpathy](https://github.com/forrestchang/andrej-karpathy-skills) — AI 编程方法论

---

MIT License · 构建中 🏗️
