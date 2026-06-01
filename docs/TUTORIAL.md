# Tutorial — Complete Research Pipeline Walkthrough

> Follow along to turn a vague research idea into a submission-ready manuscript.
> Estimated time reading: 10 minutes. Actual pipeline runtime: varies.

---

## Scenario

You're a PhD student working on nanomaterial-based cancer therapy. Your advisor says: *"Figure out the mechanism by Friday."*

You have:
- Confocal images showing mitochondrial ROS after treatment
- Flow cytometry data showing non-apoptotic cell death
- No clear hypothesis yet

Let's run the full pipeline.

---

## Phase 1: Literature Review → Hypothesis Generation

### Step 1: Lit Reviewer

```
/skill lit-reviewer

课题: carbon dots + programmed cell death + tumor therapy
关键词: carbon dots, photodynamic therapy, ferroptosis, 
       pyroptosis, necroptosis, ROS, mitochondria, tumor
数据库: arXiv, bioRxiv, PubMed
时间范围: 2024-2026
```

**Output** (excerpt):

```
📚 文献审查报告: carbon dot PCD mechanisms
检索: 23 papers → 15 unique → 10 high quality

🏆 Top 3:
1. Zhang et al. (2025) — CDs induce ferroptosis via GPX4 
   downregulation in lung cancer. IF=15.2
   → 未检验推论: 线粒体脂质过氧化是否先于 GPX4 下调？

2. Liu et al. (2024) — Mitochondrial ROS triggers atypical 
   cell death in CD-treated glioblastoma. IF=12.8
   → 与你数据一致: 线粒体 ROS 积累

3. Wang et al. (2025) — Carbon dot size determines cell death 
   pathway: <5nm = apoptosis, 5-10nm = ferroptosis. IF=18.1
   → 你的 CDs 是什么尺寸？

🕳️ 研究空白: CD-induced mitochondrial lipid peroxidation 
   → ferroptosis 的完整因果链未被直接证明
```

### Step 2: Hypothesis Generator

```
/skill hypothesis-generator

基于 Lit Reviewer 报告。已有数据:
- 共聚焦: 线粒体 ROS 显著增加 (2h post-treatment)
- 流式: Annexin V-/PI+ 群体增加 (非凋亡死亡)
- TEM: 线粒体嵴消失、外膜破裂

可用设备: 共聚焦 (C-LSM), 流式, 酶标仪, TEM
```

**Output** (excerpt):

```
🧠 假说生成报告

🏆 Top 1: CD-induced mitochondrial lipid peroxidation 
         triggers ferroptosis via a GPX4-independent pathway

辩论过程:
- 机制派: 线粒体形态变化 + ROS → 指向脂质过氧化
- 数据派: Annexin V- 排除凋亡，TEM 排除焦亡
- 怀疑派: 如何排除 necroptosis？建议加 Nec-1 对照
- 共识: 假说合理，但需要 (a) 脂质过氧化探针 
         (b) Fer-1  rescue 实验 (c) GPX4 表达检测

验证方案:
Predictions:
A) C11-BODIPY 信号在 2h 内增加 → 实验: 活细胞成像
B) Fer-1 共处理减少细胞死亡 → 实验: 剂量-反应
C) GPX4 蛋白水平不变 → 实验: Western blot

证伪条件: 如果 Fer-1 不 rescue → ferroptosis 假说被推翻
```

---

## Phase 2: Experiment Design

### Step 3: Method Designer

```
/skill method-designer

基于 Top 1 假说。设备: 共聚焦、流式、酶标仪。
时间: 2 周内完成。
```

**Output** (excerpt):

```
实验 1: 脂质过氧化时间进程 (C11-BODIPY)

Protocol:
1. 接种 1×10^4 cells/well (96-well), 37°C 过夜
2. 处理: CDs 50 μg/mL, 1-6h 时间点
3. 阳性对照: Erastin 10 μM (已知 ferroptosis 诱导剂)
4. 阴性对照: PBS 处理
5. 溶剂对照: DMSO (用于 Erastin)
6. C11-BODIPY 5 μM, 30min → 流式检测

样本量: n=4/组 (power analysis: d=1.2, α=0.05, power=0.85)
预计时间: 1 天 + 1 天分析
```

---

## Phase 3: Data Analysis

### Step 4: Data Analyst

```
/skill data-analyst

[上传: c11-bodipy_flow.csv, viability_dose_response.csv, 
 gpdx4_western_blot.csv]

实验设计: 
- C11-BODIPY: 1 factor (treatment), 6 time points, n=4
- Viability: 1 factor (dose), 6 doses, n=3  
- GPX4 WB: 2 groups (Ctrl vs CD), n=3
```

**Output** (excerpt):

```
📊 数据分析报告

🔍 数据质量: PASS (无缺失值, 无不合理异常值)

🧪 核心假说检验:

C11-BODIPY: time × treatment 交互显著
- Two-way ANOVA: F(5,36)=12.3, p=0.0003
- Post-hoc: CD vs Ctrl at 4h: d=1.8, 95%CI[1.2, 2.4]
- ✅ 脂质过氧化发生在 2-4h，早于细胞死亡 (6-8h)

Viability + Fer-1 rescue:
- CD alone: IC50 = 45 μg/mL
- CD + Fer-1: IC50 = 120 μg/mL (2.7-fold rescue)
- Welch's t-test: t(8.3)=5.2, p=0.0008, d=2.1
- ✅ Fer-1 几乎完全 rescue，强烈支持 ferroptosis

GPX4 WB:
- CD vs Ctrl: band intensity ratio = 0.94
- Paired t-test: t(2)=0.3, p=0.79
- ✅ GPX4 蛋白水平不变 → 支持 GPX4-independent 路径

⚠️ 统计警示:
- GPX4 WB n=3 偏低（趋势不显著但效应量小）
- 建议增加到 n=5 或做 GPX4 activity assay
```

---

## Phase 4: Manuscript

### Step 5: Paper Drafter

```
/skill paper-drafter

数据: Data Analyst 报告 + 所有图表
假说: CD-induced mitochondrial lipid peroxidation 
      triggers ferroptosis via GPX4-independent pathway
目标期刊: ACS Nano
```

**Output**: Full manuscript draft with structured Abstract, Introduction, Results, Discussion, Methods. (Omitted for brevity — see [EXAMPLES.md](EXAMPLES.md))

### Step 6: Peer Reviewer (Pre-submission)

```
/skill peer-reviewer

[粘贴论文初稿]
目标期刊: ACS Nano
```

**Output**: Three reviewer reports + revision priority matrix. Fix the issues before real reviewers see them.

### Step 7: Journal Matcher

```
/skill journal-matcher

摘要: [粘贴 Abstract]
自评: 新颖性 7/10, 方法学 8/10, 影响范围: 领域内
```

**Output**: Tiered journal recommendations with acceptance estimates.
- 🥇 ACS Nano (match 82%, est. acceptance ~20%)
- 🥈 Small (match 78%, est. acceptance ~25%) ← balance pick
- 🥉 Nanoscale (match 72%, est. acceptance ~35%)

---

## Phase 5: Automate Everything

### Step 8: Nightly Pipeline

```bash
hermes cron create "0 23 * * *" \
  --name "cd-ferroptosis-pipeline" \
  --prompt "Load ac-gstack-pipeline skill. Run the full pipeline for: carbon dot-induced ferroptosis in cancer therapy." \
  --skills "ac-gstack-pipeline" \
  --deliver "telegram"
```

Now: go to bed. Wake up to a research brief.

### Step 9: Weekly Literature Monitor

```bash
hermes cron create "0 8 * * 1,4" \
  --name "cd-ferroptosis-lit-monitor" \
  --prompt "Load lit-monitor skill. Monitor: carbon dots, ferroptosis, GPX4, lipid peroxidation, cancer therapy." \
  --skills "lit-monitor" \
  --deliver "telegram"
```

Never be scooped again.

---

## Summary: What Just Happened

```
Day 1: Lit Review + Hypothesis Generation  (2 hours)
Day 2: Experiment Design + Run Experiments (1-2 weeks)
Day 3: Data Analysis                        (2 hours)
Day 4: Manuscript Draft                     (1 hour)
Day 5: Peer Review + Journal Match          (1 hour)

Total AI time: ~6 hours
Total human time: ~6 hours (decision-making + experiments)
```

Without Academic GStack, this might take 4-6 weeks of scattered effort.

---

## Next Steps

- [Examples](EXAMPLES.md) — see full output samples
- [All Skills](../skills/) — browse all 18 agent roles
- [FAQ](FAQ.md) — common questions
- [Getting Started](GETTING_STARTED.md) — back to quick start
