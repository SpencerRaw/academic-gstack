# Academic GStack — Skills

这个目录包含 18 个 AI agent 角色的 Hermes Skill 定义。

每个角色 = 一个 `SKILL.md` 文件，包含：
- 角色定义（触发条件、输入输出格式）
- 工作流程（具体步骤 + 工具调用）
- 输出模板（报告格式）

## 开发状态

### ✅ P0 — 已完成
| 技能 | 描述 |
|------|------|
| `lit-reviewer` | 文献检索 + 分类 + 假说提取 |
| `hypothesis-generator` | 四角色辩论 + 排名假说 + 验证方案 |
| `peer-reviewer` | 三审稿人模拟 + 修订优先级矩阵 |

### ✅ 战略层 — 已完成
| 技能 | 描述 |
|------|------|
| `pi-reviewer` | PI 视角战略审查 + 五问框架 |
| `lab-strategist` | 多课题并行调度 + 瓶颈预测 |

### ✅ 编排层 — 已完成
| 技能 | 描述 |
|------|------|
| `ac-gstack-pipeline` | 夜间流水线引擎：串联 Lit → Hypothesis → PI → 日报 |

### 📋 P1 — 计划中
| 技能 | 描述 |
|------|------|
| `paper-drafter` | 论文初稿：Abstract→Results→Discussion |
| `data-analyst` | 自动统计 + 可视化 + 效应量 |
| `journal-matcher` | 期刊推荐 + 命中率估算 |

### 📋 P2 — 待开发
| 技能 | 描述 |
|------|------|
| `method-designer` | 实验方案设计 + 样本量估算 |
| `data-qa` | 数据完整性审计 |
| `figure-artist` | 发表级图表生成 |
| `novelty-checker` | 新颖性全网搜索 |
| `grant-writer` | 基金申请书自动生成 |
| `cover-letter` | Cover letter 定制 |
| `rebuttal-drafter` | 审稿意见逐条回复 |
| `grant-scout` | 基金机会监控 |
| `lit-monitor` | arXiv/bioRxiv 新论文推送 |
| `social-writer` | 社交媒体推广 |
| `lab-archivist` | 知识库管理 |
| `lab-manager` | 日常状态看板 |

## 技能格式

参见 [Hermes Agent 技能编写指南](https://hermes-agent.nousresearch.com/docs/user-guide/skills)

```yaml
---
name: lit-reviewer
description: "系统检索文献，自动分类，提取可检验假说"
version: 1.0.0
---

# Lit Reviewer — 文献审查员
...
```
