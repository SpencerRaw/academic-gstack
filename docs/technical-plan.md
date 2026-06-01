# Academic GStack — Technical Architecture

> How to build an academic gstack using the Hermes Agent ecosystem

---

## Architecture Overview

```
┌──────────────────────────────────────────────────────┐
│               Science CEO (You)                       │
│     Set direction → CHECKPOINT judgment → Next round  │
├──────────────────────────────────────────────────────┤
│              Academic GStack Orchestration             │
│           maestro + kanban + cron                      │
├──────────┬──────────┬──────────┬──────────────────────┤
│ Strategy │ Research │ Output   │ Operations           │
│ PI       │ Lit      │ Paper    │ Lab Manager          │
│ Strategy │ Hypo     │ Peer     │ Lit Monitor          │
│ Grant    │ Method   │ Journal  │ Social Writer        │
│          │ Data     │ Grant    │ Archivist            │
│          │ Figure   │ Rebuttal │                      │
│          │ Novelty  │          │                      │
├──────────┴──────────┴──────────┴──────────────────────┤
│                 Foundation Layer                       │
│     Co-Scientist ←→ SciDAO ←→ Domain Models           │
│     Hermes skills ←→ delegate_task ←→ cron            │
└──────────────────────────────────────────────────────┘
```

---

## Implementation: Hermes Skill System

Each agent role = one Hermes Skill. Benefits:
1. Loads naturally into sessions (`/skill lit-reviewer`)
2. Triggered automatically by cron jobs
3. Parallel execution via delegate_task
4. Continuously improved by darwin-skill
5. Persistent across sessions

### Skill Directory Structure

```
~/.hermes/skills/academic-gstack/
├── lit-reviewer/SKILL.md
├── hypothesis-generator/SKILL.md
├── method-designer/SKILL.md
├── data-analyst/SKILL.md
├── data-qa/SKILL.md
├── figure-artist/SKILL.md
├── novelty-checker/SKILL.md
├── paper-drafter/SKILL.md
├── peer-reviewer/SKILL.md
├── journal-matcher/SKILL.md
├── grant-writer/SKILL.md
├── cover-letter/SKILL.md
├── rebuttal-drafter/SKILL.md
├── pi-reviewer/SKILL.md
├── lab-strategist/SKILL.md
├── grant-scout/SKILL.md
├── lit-monitor/SKILL.md
├── social-writer/SKILL.md
├── lab-archivist/SKILL.md
└── lab-manager/SKILL.md
```

---

## Core Pipelines

### Pipeline 1: Hypothesis → Experiment Design (run at night, results in the morning)

```
cron: triggers nightly at 23:00
    │
    ▼
delegate_task (3 parallel agents)
    ├── Project A agent:
    │   /skill lit-reviewer → search latest literature
    │   /skill hypothesis-generator → generate hypotheses from data
    │   /skill method-designer → design verification experiments
    │   /skill novelty-checker → verify novelty
    │   Output → project_a_hypothesis_report.md
    │
    ├── Project B agent:
    │   Same pipeline, different domain
    │   Output → project_b_hypothesis_report.md
    │
    └── Project C agent:
        Same pipeline, different domain
        Output → project_c_hypothesis_report.md
```

### Pipeline 2: Data → Manuscript Draft

```
delegate_task:
    /skill data-analyst → statistical analysis + visualization
    /skill data-qa → audit data integrity
    /skill figure-artist → publication-quality figures
    /skill paper-drafter → write first draft
    /skill peer-reviewer → simulate 3 reviewers
    /skill journal-matcher → recommend target journals
```

### Pipeline 3: Submission → Revision

```
delegate_task:
    /skill cover-letter → generate for target journal
    [Submit, wait for reviews]
    /skill rebuttal-drafter → analyze responses point by point
```

---

## Technology Stack

### Orchestration Layer

| Component | Purpose |
|-----------|---------|
| `delegate_task` | Parallel agent execution with session isolation |
| `cronjob` | Scheduled nightly pipeline triggers |
| `kanban` (maestro) | Multi-project dashboard and progress tracking |

### Agent Layer

| Component | Purpose |
|-----------|---------|
| Co-Scientist | Hypothesis generation + debate engine |
| Domain Foundation Models | Field-specific knowledge (e.g., nanomaterial models) |
| Claude / DeepSeek / GPT | General-purpose LLM driving each agent role |

### Knowledge Layer

| Component | Purpose |
|-----------|---------|
| SciDAO | Community verification + crowdsourced feedback |
| Obsidian / Logseq | Personal knowledge management |
| Session store | All agent conversation records |

---

## Data Flow

```
User input (one-sentence direction)
    │
    ▼
Lab Strategist decomposes into subtasks
    │
    ├──→ Lit Reviewer (literature search)
    │       │
    │       ▼
    ├──→ Hypothesis Generator (hypothesis generation)
    │       │
    │       ▼
    ├──→ Method Designer (experiment design)
    │       │
    │       ▼
    │   [== CHECKPOINT: Human decision ==]
    │       │
    │       ▼
    ├──→ Data Analyst (data analysis)
    │       │
    │       ▼
    ├──→ Figure Artist (figure generation)
    │       │
    │       ▼
    ├──→ Paper Drafter (manuscript draft)
    │       │
    │       ▼
    ├──→ Peer Reviewer (simulated review)
    │       │
    │       ▼
    │   [== CHECKPOINT: Human revision ==]
    │       │
    │       ▼
    └──→ Submit Engineer (journal submission)
```

---

## Key Design Decisions

### 1. Why not automate wet-lab experiments?

Agents don't run wet-lab experiments. But they can:
- Design protocols, sample sizes, control groups
- Generate lab notebook templates
- Analyze experimental data
- Detect anomalies and new phenomena

Humans do experiments. AI does the cognitive labor.

### 2. Why run multiple projects in parallel?

Single-threaded research:
- Wait for experiments → idle
- Wait for reviews → idle
- Wait for reagents → idle

N parallel threads: while A analyzes data, B searches literature, C drafts a manuscript. Time utilization ×N.

### 3. Why build cross-domain extensions for every project?

Each research project gets two versions:
- **Standard version**: publish in the project's native field
- **Extended version**: connect to a higher-impact cross-domain direction

The extension is your differentiation weapon — it opens doors to labs and funding that the standard version alone cannot access.

---

## Priority Ranking

| Priority | Role | Rationale |
|----------|------|-----------|
| 🔴 P0 | Lit Reviewer | All downstream depends on literature input |
| 🔴 P0 | Hypothesis Generator | Core value: hypotheses are the product |
| 🔴 P0 | Peer Reviewer | Highest leverage: review feedback → lower rejection rate |
| 🟡 P1 | Paper Drafter | Reduces 80% of writing time |
| 🟡 P1 | Data Analyst | Statistical errors are the #1 rejection cause |
| 🟡 P1 | Journal Matcher | Wrong journal wastes 3-6 months |
| 🟢 P2 | Figure Artist | Better figures → higher citation rates |
| 🟢 P2 | Grant Writer | Grants = freedom = startup capital |
| 🟢 P2 | Social Writer | Academic personal brand building |
| 🔵 P3 | Lit Monitor | Passive information flow |
| 🔵 P3 | Lab Manager | Quality of life improvement |

---

## Roadmap

1. **Week 1**: Complete P0 skills (Lit Reviewer + Hypothesis Generator + Peer Reviewer)
2. **Week 1**: Set up first cron job (nightly literature search)
3. **Week 2-3**: P0+P1 fully operational, first project running complete pipeline
4. **Month 1**: Multi-project parallel mode — start at night, receive reports in the morning
