# Academic GStack — Operating System for the One-Person Lab

> [中文版](README.zh-CN.md) | [English](README.md)

> "I don't think I've typed a line of code probably since December."
> — Andrej Karpathy
>
> The future PI doesn't run experiments, doesn't write first drafts, doesn't draw figures.
> They make decisions. The AI agent team handles the rest.

**Academic GStack** applies [Garry Tan's gstack](https://github.com/garrytan/gstack) philosophy to scientific research: gstack turns one engineer into an engineering team. Academic GStack turns one researcher into a virtual lab.

Every scholar = an academic personal brand startup.
- Your paper = your product
- Your citations = your user growth
- Your h-index = your valuation
- Your lab = your company

---

## Core Mapping: gstack → Academic GStack

| gstack (Software Engineering) | Academic GStack (Scientific Research) |
|-------------------------------|---------------------------------------|
| `/office-hours` — product direction interrogation | `/lab-meeting` — research direction interrogation |
| `/plan-ceo-review` — CEO scope challenge | `/pi-review` — PI strategic review |
| `/plan-eng-review` — architecture lock-in | `/method-review` — experimental protocol lock-in |
| `/plan-design-review` — design review | `/figure-review` — figure quality review |
| `/review` — code review | `/peer-review` — simulated peer review |
| `/qa` — browser testing | `/data-qa` — data quality audit |
| `/cso` — security audit | `/novelty-check` — novelty verification |
| `/ship` — release engineer | `/submit` — submission engineer |
| `/retro` — engineering retro | `/lab-retro` — project retrospective |
| `/codex` — second opinion | `/second-opinion` — independent AI peer review |
| `/autoplan` — auto-review pipeline | `/auto-experiment` — auto-experiment pipeline |

---

## Agent Role Matrix (18 Roles)

### 🧠 Strategy Layer
| Role | Function |
|------|----------|
| **PI Reviewer** | Scope challenge: is this direction worth pursuing? What tier journal? |
| **Lab Strategist** | Multi-project scheduling: resource allocation, priorities, deadline management |
| **Grant Scout** | Match funding opportunities, auto-generate proposal drafts |

### 🔬 Execution Layer
| Role | Function |
|------|----------|
| **Lit Reviewer** | Systematic search + auto-classification + extract testable hypotheses |
| **Hypothesis Generator** | Generate ranked hypotheses from known data |
| **Method Designer** | Design experimental protocols, estimate sample sizes, write protocols |
| **Data Analyst** | Auto statistics, visualization, anomaly detection, effect size calculation |
| **Data QA** | Audit data integrity, find flaws, verify reproducibility |
| **Figure Artist** | Auto-generate publication-quality figures |
| **Novelty Checker** | Web-wide novelty search, flag existing work |

### ✍️ Output Layer
| Role | Function |
|------|----------|
| **Paper Drafter** | Write first draft: Abstract→Intro→Results→Discussion |
| **Peer Reviewer** | Simulate 3 reviewers, provide revision feedback |
| **Journal Matcher** | Analyze paper features → recommend target journals + acceptance estimate |
| **Grant Writer** | Auto-generate grant proposals from papers |
| **Cover Letter** | Auto-write cover letters for target journals |
| **Rebuttal Drafter** | Analyze reviewer comments → generate response strategy |

### 🔄 Operations Layer
| Role | Function |
|------|----------|
| **Lab Manager** | Multi-project status board, deadline alerts, resource conflict detection |
| **Lit Monitor** | arXiv/bioRxiv new paper alerts + relevance scoring |
| **Social Writer** | Auto-generate Twitter/X threads + LinkedIn + popular science summaries |
| **Lab Archivist** | Auto-organize lab notes, code, data into structured knowledge base |

---

## Workflow: From Idea to Publication

```
Think ──→ Plan ──→ Experiment ──→ Analyze ──→ Write ──→ Review ──→ Submit ──→ Reflect
  │         │          │             │          │          │           │          │
/lab-    /method-  Auto-Exp      /data-    /paper-   /peer-     /submit   /lab-
meeting  review                  analysis  draft     review     +cover    retro
  │         │          │             │          │          │           │
/pi-     /method-  /data-qa      /figure-  /peer-    /journal-  /social-
review   review     audit        artist    review    match      writer
                    │             │          │
                 You decide CHECKPOINT    You decide CHECKPOINT
```

---

## Development Status

- [x] Design doc complete (18 role definitions + full workflow)
- [x] P0 skills complete (Lit Reviewer / Hypothesis Generator / Peer Reviewer)
- [x] Strategy layer complete (PI Reviewer / Lab Strategist)
- [x] Pipeline engine complete (ac-gstack-pipeline + cron)
- [x] End-to-end deployment (Hermes Skills + nightly cron jobs)
- [x] P1 skills complete (Paper Drafter / Data Analyst / Journal Matcher)
- [x] P2 skills complete (Method Designer / Data QA / Figure Artist / Lit Monitor)
- [x] Lit Monitor cron job active (Mon/Thu 8:00)
- [ ] Novelty Checker / Grant Writer / Cover Letter / Social Writer
- [ ] Public docs + tutorials

**13/18 skills complete (72%)**

---

## Tech Stack

- **Agent Framework**: [Hermes Agent](https://github.com/NousResearch/hermes-agent)
- **Science Engine**: Co-Scientist (hypothesis generation + debate)
- **Orchestration**: maestro (multi-agent task dispatch)
- **Scheduling**: cron + delegate_task

---

## Inspiration

- [Garry Tan's gstack](https://github.com/garrytan/gstack) — the one-person engineering team
- [Andrej Karpathy](https://github.com/forrestchang/andrej-karpathy-skills) — four rules of AI-assisted programming
- [Science CEO Methodology](https://github.com/SpencerRaw/academic-gstack/tree/main/docs) — from lab technician to research commander

---

MIT License · Building 🏗️
