---
name: lab-archivist
description: "自动整理实验记录、代码、数据到结构化知识库。可搜索、可复现、可传承。P3 技能。"
version: 1.0.0
author: Academic GStack
tags: [research, knowledge-management, archiving, reproducibility, AI4S]
---

# Lab Archivist — 知识库管理员

> 你毕业之后，你的实验记录去哪了？
> 如果下一个接手你课题的人看不懂你的笔记，你的科研就断了。

## 触发条件

- 每个实验完成后
- 每周自动整理
- 论文发表后归档
- 用户说"帮我整理实验记录"

## 归档结构

```
project-{name}/
├── README.md                    ← 项目概述 + 快速导航
├── experiments/
│   ├── 2026-06-01_dose-response/
│   │   ├── protocol.md          ← 实验方案
│   │   ├── notebook.md          ← 实验记录 (日期/操作/观察)
│   │   ├── data/
│   │   │   ├── raw/             ← 原始数据（只读，永不修改）
│   │   │   └── processed/       ← 处理后的数据
│   │   ├── analysis/
│   │   │   ├── analysis.py      ← 分析代码
│   │   │   └── figures/         ← 生成的图表
│   │   └── README.md            ← 实验总结 + 关键发现
│   └── 2026-06-03_mechanism/
│       └── ...
├── manuscripts/
│   ├── v1/                      ← 初稿
│   ├── v2/                      ← 修改稿
│   └── submitted/               ← 投稿版本
├── literature/
│   └── reading-notes.md         ← 文献阅读笔记
├── presentations/
│   └── 2026-06_group-meeting/
├── data-registry.md             ← 所有数据文件的索引
└── project-log.md               ← 项目大事记
```

## 工作流

### 日常归档
```
每天/每次实验后:
1. 扫描最近的实验记录
2. 提取:
   - 日期
   - 实验名称
   - 使用的试剂（货号/批号）
   - 关键参数
   - 数据文件路径
   - 观察/异常
3. 更新 project-log.md
4. 标记是否完成了数据备份
```

### 每周整理
```
每周:
1. 检查是否有未归档的实验记录
2. 更新 data-registry.md
3. 检查原始数据是否已备份（推荐 3-2-1 备份策略）
4. 标记本周的关键进展
```

### 论文归档
```
论文发表后:
1. 冻结所有相关数据（read-only archive）
2. 上传到 figshare / Zenodo / 机构数据库
3. 生成 DOI
4. 更新 README 标注数据可用性
```

## 输出格式（project-log.md）

```markdown
# Project Log: {课题名称}

## 2026-06-01: {实验名称}

**目的**: {为什么做这个实验}
**方案**: [{protocol_name}](experiments/2026-06-01_dose-response/protocol.md)

**关键参数**:
- 细胞密度: {value}
- 处理浓度: {value}
- 处理时间: {value}

**主要发现**:
- {finding_1}
- {finding_2}

**异常/注意**:
- {anomaly}

**数据位置**: [experiments/2026-06-01_dose-response/data/](...)

**下一步**: {next_experiment}
```

## 备份检查清单

```
□ 原始数据是否在至少 2 个物理位置？（本地 + 云/外置硬盘）
□ 原始数据是否只读？（防止意外修改）
□ 关键试剂信息是否记录？（货号、批号、过期日期）
□ 分析代码是否有版本控制？（git）
□ 是否有人能独立复现你的分析？
```

## 命名规范

```
实验文件夹: YYYY-MM-DD_{简短描述}  (如 2026-06-01_dose-response)
数据文件: {实验名}_{变量}_{日期}.{ext}  (如 dose-response_raw_20260601.csv)
图表: fig{N}_{描述}.{ext}  (如 fig1_dose-response.pdf)
```

## 注意事项

- 原始数据永不被修改——任何处理都保存为新文件
- 归档不需要完美——80% 的整理好过 100% 的想整理但没做
- 命名规范从一开始就遵守——后期改名是噩梦
- 每周归档比事后补记容易 10 倍
