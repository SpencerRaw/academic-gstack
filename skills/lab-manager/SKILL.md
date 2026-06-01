---
name: lab-manager
description: "多课题日常状态看板：进度追踪、死线预警、每日 CHECKPOINT、任务管理。P3 技能。"
version: 1.0.0
author: Academic GStack
tags: [research, project-management, dashboard, tracking, AI4S]
---

# Lab Manager — 实验室管家

> 你知道你的每个课题今天该做什么吗？
> 如果你需要花 10 分钟想"现在该干什么"——你需要 Lab Manager。

## 触发条件

- 每天早上 CHECKPOINT
- 用户说"今天该做什么？"
- 每周/每月回顾
- 新任务/死线出现时

## 看板视图

### 周视图

```
This week: 2026-06-01 ~ 06-07

┌──────────────────────────────────────────────┐
│  🔴 P0: Nano-ferroptosis — draft deadline    │
│  ████████████████░░░░  80%                  │
│  Today: confirm data quality ✅               │
│  Tomorrow: launch Paper Drafter               │
│  Blocked: none                                │
├──────────────────────────────────────────────┤
│  🟡 P1: Protein biophysics project            │
│  ██████░░░░░░░░░░░░  30%                    │
│  Today: continue data collection              │
│  Blocked: waiting for reagents (est. 2 days)  │
├──────────────────────────────────────────────┤
│  🟢 P2: Plant photobiology lit review        │
│  ████████████░░░░░░  60%                    │
│  Today: finish classification                 │
│  Blocked: none                                │
└──────────────────────────────────────────────┘
```

### Daily View

```
📅 Today: 2026-06-01 (Monday)

Morning (8:00-12:00) 🧠 High cognition
  □ [P0] Confirm nano-ferroptosis data quality
  □ [P0] Run supplementary statistical analysis
  □ [P1] Read foundational literature

Afternoon (14:00-18:00) 🔧 Medium cognition
  □ [P0] If data OK → launch Paper Drafter
  □ [P2] Finish plant photobiology lit classification
  □ [Admin] Reply to advisor emails

Evening (20:00-21:00) 🌙 Low cognition
  □ [Growth] Language practice
  □ [Plan] Preview tomorrow's tasks
```

## 输出格式

```markdown
# 🏠 Lab Dashboard: {date}

## ⚡ 今日重点

**一句话**: {今天最重要的一个任务}

**如果今天只做一件事**: {the_one_thing}

## 📋 任务列表

| # | Priority | Task | Project | Est | Status |
|---|----------|------|---------|-----|--------|
| 1 | P0 | Confirm data quality | Nano-ferroptosis | 1h | ⬜ |
| 2 | P0 | Supplementary analysis | Protein physics | 2h | ⬜ |
| 3 | P1 | Foundational reading | All | 30m | ⬜ |
| 4 | P2 | Lit classification | Plant photo | 1h | ⬜ |

## 📊 Project Progress

| Project | Phase | Week | Overall | Next |
|---------|-------|------|---------|------|
| Nano-ferroptosis | 📊→✍️ | 80% | 75% | Launch Paper Drafter |
| Protein biophysics | 🔬 | 30% | 40% | Wait for reagents |
| Plant photobiology | 📖 | 60% | 20% | Finish classification |

## 🚨 Alerts

| Level | Issue | Impact | Suggestion |
|-------|-------|--------|------------|
| 🔴 | Nano-ferroptosis: data contradiction → re-run | May miss deadline | Confirm by 10:00 today |
| 🟡 | Protein project: reagent delay | Experiment +2 days | Do what's possible now |

## ✅ Yesterday

- [x] Nano-ferroptosis raw data organized
- [x] qPCR run complete
- [x] Plant photo literature downloaded

## 📅 Weekly Milestones

- [ ] Wed: Nano-ferroptosis first draft
- [ ] Fri: All supplementary data collected
- [ ] Sun: Full portfolio review

## 🔄 习惯追踪

| 习惯 | Mon | Tue | Wed | Thu | Fri | Sat | Sun |
|------|-----|-----|-----|-----|-----|-----|-----|
| 晨跑 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| 文献 30min | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |
| 口语练习 | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ | ⬜ |

---

> 🤖 此看板每日自动生成
```

## 与其他 Skill 联动

- `lab-strategist` → 提供兵力分配建议
- `lit-monitor` → 更新文献阅读任务
- `grant-scout` → 添加基金申请任务
- `ac-gstack-pipeline` → 更新假说生成进度

## 注意事项

- "今天只做一件事" — 如果所有任务都标记 P0，等于没有 P0
- 预估时间要诚实——"1h" 的任务通常需要 2h
- 上午安排最高认知负荷的任务
- 每天 CHECKPOINT 不是微管理——是确保你没有偏离主航道
