# Academic GStack — Skills

这个目录包含 18 个 AI agent 角色的 Hermes Skill 定义。

每个角色 = 一个 `SKILL.md` 文件，包含：
- 角色定义（触发条件、输入输出格式）
- 工作流程（具体步骤 + 工具调用）
- 输出模板（报告格式）

## 目录（规划中）

```
skills/
├── lit-reviewer/          # 文献检索 + 分类
├── hypothesis-generator/  # 假说生成 + 排名
├── method-designer/       # 实验方案设计
├── data-analyst/          # 数据分析 + 统计
├── data-qa/               # 数据质量审计
├── figure-artist/         # 图表自动生成
├── novelty-checker/       # 新颖性全网搜索
├── paper-drafter/         # 论文初稿写作
├── peer-reviewer/         # 模拟审稿
├── journal-matcher/       # 期刊推荐
├── grant-writer/          # 基金申请书
├── cover-letter/          # Cover letter
├── rebuttal-drafter/      # 审稿回复
├── pi-reviewer/           # PI 战略审查
├── lab-strategist/        # 多课题调度
├── grant-scout/           # 基金机会监控
├── lit-monitor/           # 新论文推送
├── social-writer/         # 社交媒体推广
├── lab-archivist/         # 知识库管理
└── lab-manager/           # 日常看板
```

## 开发优先级

| 优先级 | 技能 | 理由 |
|--------|------|------|
| P0 | Lit Reviewer | 所有下游依赖文献 |
| P0 | Hypothesis Generator | 核心价值：假说即产品 |
| P0 | Peer Reviewer | 最高杠杆：降低被拒率 |
| P1 | Paper Drafter | 减少 80% 写作时间 |
| P1 | Data Analyst | 统计错误是拒稿头号原因 |
| P1 | Journal Matcher | 投错期刊浪费数月 |
| P2+ | 其余 12 个 | 依次开发 |

## 技能格式

参见 [Hermes Agent 技能编写指南](https://hermes-agent.nousresearch.com/docs/user-guide/skills)

```yaml
---
name: lit-reviewer
description: "系统检索文献，自动分类，提取可检验假说"
version: 0.1.0
---

# Lit Reviewer — 文献审查员

## 触发条件
- 用户提供研究课题关键词
- 定时任务（每周自动检索最新文献）

## 输入
- 研究领域关键词
- 检索数据库（PubMed / arXiv / bioRxiv / Google Scholar）
- 检索范围（时间 / 影响因子 / 引用数）

## 输出
- 文献分类表格（按相关性/质量评分）
- 可检验假说列表（从每篇核心文献提取）
- 研究空白标注
```
