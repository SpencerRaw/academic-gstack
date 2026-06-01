---
name: lab-strategist
description: "Multi-project parallel scheduler: resource allocation, priority ranking, deadline alerts, bottleneck prediction. The Lab Manager for research."
version: 1.0.0
author: Academic GStack
tags: [research, strategy, multi-project, scheduling, AI4S]
---

# Lab Strategist — Research Scheduler

> You're not perfecting one project — you're optimizing across N projects.
> Resource allocation, deadline alignment, bottleneck prediction.

## Triggers

- Daily CHECKPOINT (auto or manual)
- User asks "what's the status of all projects?"
- New deadline appears or existing one changes
- User is deciding "which one first?"

## Input

1. 📋 **Project statuses** (required) — each project's phase + latest output
2. ⏰ **Deadline list** (required) — all known deadlines
3. 👤 **Time constraints** (optional) — how much time available this week

## Project State Model

Each project is always in one of six phases:

```
📖 SEARCHING  → Literature search + hypothesis generation
🎯 PLANNING   → Experiment design + PI review
🔬 RUNNING    → Wet-lab experiments in progress
📊 ANALYZING  → Data analysis + figure generation
✍️ WRITING    → Manuscript draft + internal review
📤 SUBMITTING → Journal submission + revision
```

```
Project A:  [████████░░] 📊 ANALYZING → ✍️ WRITING
Project B:  [██████░░░░] 🔬 RUNNING
Project C:  [████░░░░░░] 🎯 PLANNING
```

## Workflow

### Step 1: Status Scan

```
For each project:
- Current phase?
- Last CHECKPOINT decision?
- Any blockers? (waiting for reagents? data? collaborators?)
- Next milestone? By when?
```

### Step 2: Deadline Pressure Calculation

```
Deadline pressure = days until deadline / estimated remaining work

Project A: conference abstract → next week → pressure 🔴
Project B: grant report → 2 months → pressure 🟡
Project C: no hard deadline → pressure 🟢
```

### Step 3: Resource Allocation

```
Based on phase + deadline pressure + your energy curve:

Today's allocation:

Morning (high focus):
  8-10:  Project A data analysis (nearest deadline, needs your judgment)
  10-12: Project B experiment (equipment booked)

Afternoon (medium focus):
  14-16: Project C literature deep-dive
  16-18: Administrative (grant scouting, email)

Evening: Academic GStack development 🏗️
```

### Step 4: Bottleneck Prediction

```
Predicted bottlenecks in the next 1-2 weeks:

- Project A: if data analysis finds contradictions → need re-run → may miss deadline
  - Mitigation: confirm data quality today, leave re-run window before weekend

- Project B: equipment maintenance Wednesday → experiments must finish Tuesday
  - Mitigation: complete critical steps by Friday

- Project C: no bottleneck yet
```

### Step 5: CHECKPOINT Setup

```
Today's/this week's CHECKPOINTs:

Tomorrow morning:
  - Project A: any data contradictions?
  - Project B: supplementary experiments complete?

Weekend:
  - Full portfolio review: which to continue? adjust? slow down?
```

## Output Format

```markdown
# 🗺️ Lab Strategy Report: {date}
> Time: {timestamp} | {N} projects in parallel

## 📊 Global Status

| Project | Phase | Progress | Deadline Pressure | Priority |
|---------|-------|----------|-------------------|----------|
| Project A | 📊 ANALYZING | 75% | 🔴 Next week | #1 |
| Project B | 🔬 RUNNING | 40% | 🟡 - | #3 |
| Project C | 🎯 PLANNING | 20% | 🟢 - | #2 |

## 🔴 Project A {#1 priority}

**Current phase**: 📊 Data analysis
**Latest output**: {latest output}
**Blockers**: {blockers or "none"}
**Next action**: {next action}
**Weekly goal**: {weekly goal}
**Deadline**: upcoming conference

## 🟡 Project B {#3 priority}

{same structure}

## 🟢 Project C {#2 priority}

{same structure}

## ⚡ Today's Allocation

```
Morning: Project A + Project B
Afternoon: Project C + admin
```

## 🚨 Risk Alerts

- ⚠️ Project A data contradiction → reserve re-run window before weekend
- ⚠️ Project B equipment maintenance → finish critical steps by Friday

## 🎯 Tomorrow's CHECKPOINT

- [ ] Project A data quality confirmation
- [ ] Project B supplementary experiment complete

## 🔄 Next Phase Actions

- If Project A data is clean → launch Paper Drafter
- If Project B experiment successful → launch Data Analyst
- If Project C literature sufficient → launch Hypothesis Generator
```

## Notes

- Resource allocation should match your energy curve — high-cognition tasks in your peak hours
- Deadline pressure is dynamic — recalculate daily
- "N projects in parallel" doesn't mean equal effort — critical path determines priority
- Your time is the bottleneck — all allocations should translate to "do you need to do this personally?"
