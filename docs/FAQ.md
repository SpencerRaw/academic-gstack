# FAQ — Frequently Asked Questions

---

## General

### What is Academic GStack?

Academic GStack applies Garry Tan's "one-person engineering team" philosophy to scientific research. It's a collection of 18 AI agent roles (skills) that automate the cognitive labor of research — literature review, hypothesis generation, experiment design, data analysis, paper writing, peer review, and more.

### Is this a replacement for researchers?

No. It's a force multiplier. You still make the decisions. You still run the wet-lab experiments. The AI handles the cognitive overhead — searching, analyzing, drafting, reviewing — so you can focus on what only you can do: creative scientific judgment.

### Does it actually work?

Yes, in active daily use. The skills are designed to work with real research workflows. The nightly pipeline has been running since June 2026, generating hypothesis reports for multiple concurrent projects. See [TUTORIAL.md](TUTORIAL.md) for a complete walkthrough.

### What makes this different from just using ChatGPT/Claude for research?

Two things:
1. **Structure**: Each skill is a specialized workflow with proven methodologies, not a blank prompt. The Lit Reviewer doesn't just "search papers" — it classifies, scores, extracts hypotheses, and identifies gaps.
2. **Pipeline**: Skills chain together. Lit Reviewer output flows into Hypothesis Generator which flows into Method Designer. And cron jobs run the whole thing while you sleep.

---

## Setup & Usage

### Do I need Hermes Agent?

Currently, yes. Academic GStack skills are written for the Hermes Agent framework. We're open to ports for Claude Code, Codex CLI, and other agents — see [CONTRIBUTING.md](../CONTRIBUTING.md) if you want to help.

### How do I install it?

```bash
git clone https://github.com/SpencerRaw/academic-gstack.git
cp -r academic-gstack/skills/* ~/.hermes/skills/
```

See [GETTING_STARTED.md](GETTING_STARTED.md) for the full 5-minute guide.

### What LLM do I need?

Any model that supports tool calling. The skills use web search (for literature), file operations (for data), and delegation (for parallel execution). Claude, GPT-4, DeepSeek, and Gemini all work well.

### Can I use it without Telegram?

The cron notifications currently deliver via Telegram. You can change the delivery target to any platform Hermes supports (Discord, Slack, Email, etc.) or set `--deliver local` to skip notifications entirely.

### How much does it cost?

The skills are free and MIT-licensed. You pay for your LLM API usage (OpenRouter, Anthropic, etc.). A typical nightly pipeline run costs ~$0.50-2.00 in API credits depending on the model.

---

## Skills & Pipelines

### Which skill should I start with?

`lit-reviewer`. It's the gateway — all downstream skills depend on literature input. Plus, a good lit review is immediately useful even without the rest of the pipeline.

### Can I use skills individually?

Yes. Every skill is self-contained. You don't need the pipeline. Load any skill with `/skill <name>` in a Hermes session.

### How do I customize skills for my field?

Skills are designed to be field-agnostic. The Lit Reviewer works for any discipline with published literature. Journal Matcher covers chemistry, biology, materials, and more. To add your field's journals or conventions, edit the `SKILL.md` file directly.

### Can the pipeline handle multiple projects?

Yes. The `ac-gstack-pipeline` skill and `lab-strategist` are designed for N parallel projects. Configure your projects in the pipeline prompt and it will run them concurrently.

### What if the literature search returns nothing?

The pipeline retries with expanded search terms once. If still zero results, it flags "insufficient literature" and skips downstream steps for that project. This is rare but can happen in very niche fields.

---

## Privacy & Security

### Are my research ideas exposed?

Skills run on your local machine through your Hermes Agent. Your API calls go to your configured LLM provider. Nothing is sent to Academic GStack servers — there are none.

### Can I use this for confidential/industry research?

Yes, with appropriate precautions. Use a local LLM (via Ollama) for maximum privacy. Never include proprietary data in prompts sent to cloud providers.

---

## Contributing

### How can I contribute?

See [CONTRIBUTING.md](../CONTRIBUTING.md). We welcome:
- New skills (Grant Writer for specific agencies, domain-specific reviewers, etc.)
- Improvements to existing skills
- Ports to other agent frameworks (Claude Code, Codex, OpenClaw)
- Bug reports and feature requests

### Can I add a skill for my specific field?

Absolutely. Follow the skill format in `skills/README.md`. Each skill is one `SKILL.md` file. PRs welcome.
