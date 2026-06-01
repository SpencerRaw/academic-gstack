# Examples — Real Outputs from Academic GStack Skills

> What you actually get when you run each skill.

---

## Lit Reviewer — Sample Output

```
📚 文献审查报告: carbon dot PCD mechanisms
检索时间: 2026-06-01 23:05

📊 检索概览
检索论文: 23 | 去重后: 15 | 入选分析: 10 | 高质量(≥35分): 4

🏆 Top 3 排序论文

| # | 标题 | 期刊 | 日期 | 总分 | 相关性 | 新颖性 |
|---|------|------|------|------|--------|--------|
| 1 | CDs induce ferroptosis via GPX4 | ACS Nano | 2025 | 42 | 9 | 8 |
| 2 | Mitochondrial ROS in CD therapy | Small | 2024 | 38 | 8 | 7 |
| 3 | CD size dictates death pathway | Nature Comm | 2025 | 36 | 7 | 9 |

🔬 #1 深度分析
核心假说: CDs downregulate GPX4 → lipid peroxidation → ferroptosis
未检验推论: 线粒体脂质过氧化是否先于GPX4下调？
与你课题的交叉: 你有线粒体ROS数据，他们没看线粒体

🕳️ 研究空白
| 空白领域 | 重要性 | 竞争程度 | 你的优势 |
| CD→线粒体脂质过氧化→ferroptosis因果链 | 🔴高 | 低 | 已有TEM+ROS数据 |
```

---

## Hypothesis Generator — Sample Output

```
🧠 假说生成报告: CD cell death mechanism

🏆 #1: CD-induced mitochondrial lipid peroxidation triggers 
      ferroptosis via GPX4-independent pathway

辩论过程:
机制派(A): 线粒体嵴消失+ROS+膜破裂 → 经典ferroptosis形态
数据派(B): Annexin V- 排除凋亡。但数据缺少脂质过氧化直接证据
类比派(C): 类似Erlotinib在三阴性乳腺癌中的机制——线粒体先于胞质
怀疑派(D): 如何排除necroptosis？RIPK1/RIPK3/MLKL通路未检测
→ 共识: 假说成立但需补实验

验证方案:
预测A: C11-BODIPY 2-4h信号增加 → 活细胞成像
预测B: Fer-1 rescue剂量依赖性 → 剂量反应曲线
预测C: GPX4蛋白水平不变 → Western blot
证伪条件: 如果Fer-1不rescue → ferroptosis假说推翻
```

---

## Peer Reviewer — Sample Output

```
📝 模拟同行评审: CD-ferroptosis manuscript

📊 评审总览
| 审稿人 | 角色 | 建议 |
| #1 | 方法论审查官 | Major Revision |
| #2 | 领域专家 | Minor Revision |
| #3 | 怀疑论者 | Major Revision |

🔴 致命问题 (≥2审稿人一致)

F1: 缺少 necroptosis 排除实验
- #1: RIPK1/3/MLKL应检测
- #3: "ferroptosis不是唯一非凋亡死亡"
→ 修复: 加Nec-1对照 + RIPK3 blot (预估3天)

📋 修订优先级矩阵
| 优先级 | 问题 | 修复成本 | 
| P0 | F1: necroptosis排除 | 中(3d) |
| P0 | F2: GPX4 activity assay | 低(1d) |
| P1 | I1: 讨论中过度声称"首次" | 低(1h) |
```

---

## Journal Matcher — Sample Output

```
🎯 期刊匹配报告: CD-ferroptosis

📊 论文自评
新颖性: 7/10 | 方法学: 8/10 | 影响范围: 领域内
最佳匹配IF区间: 12-18

🥇 Tier 1 (命中率 5-15%)
| 期刊 | IF | 匹配度 | 命中率 | 为什么 |
| ACS Nano | 17 | 82% | 20% | 近2年发表过类似CD毒性研究 |
| Nano Letters | 11 | 75% | 25% | 机制细节充分 |

🥈 Tier 2 (命中率 15-30%) — 推荐！
| Small | 13 | 78% | 25% | 纳米生物界面是scope核心 |

🧭 推荐策略B (平衡): Small → 如被拒 → Nanoscale
```

---

## Data QA — Sample Output

```
🔍 数据质量审计: CD-ferroptosis

🔴 致命缺陷
| F1 | 缺失溶剂对照 | Fig 2A | DMSO用于Erastin但无DMSO-only对照 |

🟡 警告
| W1 | n=3 for GPX4 WB | Fig 4C | 统计功效不足 |
| W2 | Error bar = SEM 但未标注 | Fig 3B | 必须标注 |

📊 审计摘要
完整性:    ████████░░ 82%
统计:      █████████░ 93%
可重复性:  ██████░░░░ 65% ← 最低
图像:      ████████░░ 88%
```

---

## Lit Monitor — Sample Output

```
📡 文献监控周报: 2026-05-26 ~ 06-01

🔴 CRITICAL
#1: "Size-dependent ferroptosis induction by carbon dots"
    来源: bioRxiv, 2026-05-28
    核心发现: <10nm CDs trigger ferroptosis, >10nm trigger apoptosis
    ⚠️ 重叠: 他们做了你计划做的尺寸效应实验
    🎯 应对: 你的差异化——他们只看了细胞，你有体内数据

📊 本周统计
论文总数:     ██████████ 25
🔴 Critical:   ██ 2
🟡 Relevant:   █████ 5
🟢 Background: ██████████████ 18
```

---

## Lab Manager — Sample Output

```
🏠 Lab Dashboard: 2026-06-01 (周一)

⚡ 今日重点: 确认C11-BODIPY数据是否支持ferroptosis假说

📋 任务列表
| # | 优先 | 任务 | 课题 | 预估 |
| 1 | P0 | C11-BODIPY 流式数据分析 | CD-ferroptosis | 1h |
| 2 | P0 | Fer-1 rescue 剂量反应 | CD-ferroptosis | 2h |
| 3 | P1 | GPX4 Western blot | CD-ferroptosis | 3h |
| 4 | P2 | 文献更新检查 | 全课题 | 30m |

📊 各课题进度
| 课题 | 阶段 | 进度 | 下一步 |
| CD-ferroptosis | 📊→✍️ | 75% | 启动Paper Drafter |
| IDR project | 🔬 | 40% | 等待试剂 |
| NIR project | 📖 | 20% | 完成文献分类 |
```
