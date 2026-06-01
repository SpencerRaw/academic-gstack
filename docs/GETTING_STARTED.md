# Getting Started — 5 Minutes to Your First AI-Powered Research Pipeline

> No PhD in AI required. Just your research question and a Hermes Agent.

---

## Prerequisites

- [Hermes Agent](https://github.com/NousResearch/hermes-agent) installed and configured
- An LLM provider configured (OpenRouter, Anthropic, DeepSeek, etc.)
- 5 minutes

## Step 1: Install Academic GStack Skills (30 seconds)

```bash
git clone https://github.com/SpencerRaw/academic-gstack.git /tmp/academic-gstack
cp -r /tmp/academic-gstack/skills/* ~/.hermes/skills/
```

Verify:

```bash
hermes skills list | grep -E "lit-reviewer|hypothesis|peer-review"
```

You should see all 18 skills listed as `enabled`.

## Step 2: Your First Literature Review (2 minutes)

Start a Hermes session and load the Lit Reviewer:

```
/skill lit-reviewer
```

Then give it a research topic:

> Search for recent papers on carbon dots for photodynamic cancer therapy. Keywords: carbon dots, photodynamic therapy, reactive oxygen species, tumor. Focus on 2024-2026. Classify by relevance and extract testable hypotheses.

Hermes will search arXiv, bioRxiv, PubMed and return a ranked report with extracted hypotheses and research gaps.

**What you get**: A structured lit review you can actually use — not just a list of papers.

## Step 3: Generate Hypotheses (2 minutes)

Take the top 3 papers from the lit review and run:

```
/skill hypothesis-generator
```

> Based on the lit review, generate ranked hypotheses for carbon dot-mediated cell death mechanisms. Current data: confocal microscopy shows mitochondrial ROS accumulation. Available equipment: flow cytometer, microplate reader.

**What you get**: Ranked hypotheses with verification experiments, falsification conditions, and debate notes from 4 different scientific perspectives.

## Step 4: Peer Review Before Submission (1 minute)

Got a draft? Before submitting to a journal:

```
/skill peer-reviewer
```

Paste your abstract or upload your draft. Three reviewer personas will tear it apart — so the real reviewers don't have to.

**What you get**: A revision priority matrix showing exactly what to fix and in what order.

## Step 5: Set Up the Nightly Pipeline (30 seconds)

The real power move — automate steps 2-4 to run while you sleep:

```bash
hermes cron create "0 23 * * *" \
  --name "my-nightly-research" \
  --prompt "Load ac-gstack-pipeline skill. Run the full nightly research pipeline for my project: [your project description]. Generate daily brief." \
  --skills "ac-gstack-pipeline" \
  --deliver "telegram"
```

**What you get**: Every morning, a research brief on your phone with new hypotheses ranked and ready.

---

## What's Next?

- [Full Tutorial](TUTORIAL.md) — walkthrough of a complete research pipeline
- [Examples](EXAMPLES.md) — see real output from each skill
- [All Skills](../skills/) — browse all 18 agent roles
- [FAQ](FAQ.md) — common questions answered

---

## Quick Reference

| You want to... | Use this skill |
|---------------|----------------|
| Find papers + extract hypotheses | `lit-reviewer` |
| Generate ranked hypotheses | `hypothesis-generator` |
| Design experiments | `method-designer` |
| Analyze data statistically | `data-analyst` |
| Audit data quality | `data-qa` |
| Generate figures | `figure-artist` |
| Check novelty | `novelty-checker` |
| Write a paper draft | `paper-drafter` |
| Get pre-submission review | `peer-reviewer` |
| Find the right journal | `journal-matcher` |
| Write a cover letter | `cover-letter` |
| Respond to reviewers | `rebuttal-drafter` |
| Write a grant proposal | `grant-writer` |
| Monitor new papers weekly | `lit-monitor` |
| Find funding opportunities | `grant-scout` |
| Promote your paper | `social-writer` |
| Organize your lab data | `lab-archivist` |
| Daily task dashboard | `lab-manager` |
