# Tutorial — Complete Research Pipeline Walkthrough

> Follow along to turn a vague research idea into a submission-ready manuscript.
> Reading time: 10 minutes.

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

Topic: carbon dots + programmed cell death + tumor therapy
Keywords: carbon dots, photodynamic therapy, ferroptosis,
          pyroptosis, necroptosis, ROS, mitochondria, tumor
Databases: arXiv, bioRxiv, PubMed
Time range: 2024-2026
```

**Output** (excerpt):

```
📚 Literature Review: carbon dot PCD mechanisms
Searched: 23 papers → 15 unique → 10 high quality

🏆 Top 3:
1. Zhang et al. (2025) — CDs induce ferroptosis via GPX4
   downregulation in lung cancer. IF=15.2
   → Untested corollary: Does mitochondrial lipid peroxidation
     precede GPX4 downregulation?

2. Liu et al. (2024) — Mitochondrial ROS triggers atypical
   cell death in CD-treated glioblastoma. IF=12.8
   → Consistent with your data: mitochondrial ROS accumulation

3. Wang et al. (2025) — Carbon dot size determines cell death
   pathway: <5nm = apoptosis, 5-10nm = ferroptosis. IF=18.1
   → What size are your CDs?

🕳️ Research gap: The complete causal chain from CD treatment
   → mitochondrial lipid peroxidation → ferroptosis remains
   unproven in a single study.
```

### Step 2: Hypothesis Generator

```
/skill hypothesis-generator

Based on Lit Reviewer report. Existing data:
- Confocal: mitochondrial ROS significantly increased (2h post-treatment)
- Flow: Annexin V-/PI+ population increased (non-apoptotic death)
- TEM: mitochondrial cristae loss, outer membrane rupture

Available equipment: confocal, flow cytometer, microplate reader, TEM
```

**Output** (excerpt):

```
🧠 Hypothesis Report

🏆 Top 1: CD-induced mitochondrial lipid peroxidation
         triggers ferroptosis via a GPX4-independent pathway

Debate summary:
- Mechanist: Mitochondrial morphology + ROS → lipid peroxidation
- Data-first: Annexin V- rules out apoptosis. TEM rules out pyroptosis.
- Skeptic: How to exclude necroptosis? Add Nec-1 control.
- Consensus: Hypothesis plausible. Needs (a) lipid peroxidation probe
             (b) Fer-1 rescue (c) GPX4 expression check.

Verification:
Prediction A: C11-BODIPY signal increases at 2-4h → live-cell imaging
Prediction B: Fer-1 co-treatment reduces death → dose-response curve
Prediction C: GPX4 protein level unchanged → Western blot

Falsification: If Fer-1 fails to rescue → ferroptosis hypothesis rejected
```

---

## Phase 2: Experiment Design

### Step 3: Method Designer

```
/skill method-designer

Based on Top 1 hypothesis. Equipment: confocal, flow, plate reader.
Timeline: complete within 2 weeks.
```

**Output** (excerpt):

```
Experiment 1: Lipid peroxidation time course (C11-BODIPY)

Protocol:
1. Seed 1×10^4 cells/well (96-well), 37°C overnight
2. Treatment: CDs 50 μg/mL, time points 1-6h
3. Positive control: Erastin 10 μM (known ferroptosis inducer)
4. Negative control: PBS
5. Vehicle control: DMSO (for Erastin)
6. C11-BODIPY 5 μM, 30min → flow cytometry

Sample size: n=4/group (power analysis: d=1.2, α=0.05, power=0.85)
Estimated time: 1 day + 1 day analysis
```

---

## Phase 3: Data Analysis

### Step 4: Data Analyst

```
/skill data-analyst

[Upload: c11-bodipy_flow.csv, viability_dose_response.csv,
 gpdx4_western_blot.csv]

Design:
- C11-BODIPY: 1 factor (treatment), 6 time points, n=4
- Viability: 1 factor (dose), 6 doses, n=3
- GPX4 WB: 2 groups (Ctrl vs CD), n=3
```

**Output** (excerpt):

```
📊 Data Analysis Report

🔍 Data quality: PASS (no missing values, no unreasonable outliers)

🧪 Core Hypothesis Tests:

C11-BODIPY: time × treatment interaction significant
- Two-way ANOVA: F(5,36)=12.3, p=0.0003
- Post-hoc: CD vs Ctrl at 4h: d=1.8, 95%CI[1.2, 2.4]
- ✅ Lipid peroxidation occurs at 2-4h, preceding cell death (6-8h)

Viability + Fer-1 rescue:
- CD alone: IC50 = 45 μg/mL
- CD + Fer-1: IC50 = 120 μg/mL (2.7-fold rescue)
- Welch's t-test: t(8.3)=5.2, p=0.0008, d=2.1
- ✅ Fer-1 nearly completely rescues, strongly supporting ferroptosis

GPX4 WB:
- CD vs Ctrl: band intensity ratio = 0.94
- Paired t-test: t(2)=0.3, p=0.79
- ✅ GPX4 protein level unchanged → supports GPX4-independent pathway

⚠️ Statistical notes:
- GPX4 WB n=3 is low (effect size small, may be underpowered)
- Consider increasing to n=5 or running GPX4 activity assay
```

---

## Phase 4: Manuscript

### Step 5: Paper Drafter

```
/skill paper-drafter

Data: Data Analyst report + all figures
Hypothesis: CD-induced mitochondrial lipid peroxidation
           triggers ferroptosis via GPX4-independent pathway
Target journal: ACS Nano
```

**Output**: Full manuscript draft with structured Abstract, Introduction, Results, Discussion, Methods. (See [EXAMPLES.md](EXAMPLES.md) for sample output format.)

### Step 6: Peer Reviewer (Pre-submission)

```
/skill peer-reviewer

[Paste manuscript draft]
Target journal: ACS Nano
```

**Output**: Three reviewer reports + revision priority matrix. Fix issues before real reviewers see them.

### Step 7: Journal Matcher

```
/skill journal-matcher

Abstract: [paste Abstract]
Self-assessment: novelty 7/10, methodology 8/10, scope: field-specific
```

**Output**: Tiered journal recommendations with acceptance estimates.
- 🥇 ACS Nano (match 82%, est. acceptance ~20%)
- 🥈 Small (match 78%, est. acceptance ~25%) ← balanced pick
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

Now: go to bed. Wake up to a research brief on your phone.

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
Day 2: Experiment Design + Run Experiments (1-2 weeks wet lab)
Day 3: Data Analysis                        (2 hours)
Day 4: Manuscript Draft                     (1 hour)
Day 5: Peer Review + Journal Match          (1 hour)

Total AI time: ~6 hours
Total human time: ~6 hours (decisions + wet lab)
```

Without Academic GStack, this might take 4-6 weeks of fragmented effort.

---

## Next Steps

- [Examples](EXAMPLES.md) — full output samples
- [All Skills](../skills/) — browse all 18 agent roles
- [FAQ](FAQ.md) — common questions
- [Getting Started](GETTING_STARTED.md) — back to quick start
