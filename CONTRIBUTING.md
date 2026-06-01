# Contributing to Academic GStack

🎉 Thanks for your interest! Academic GStack is an open-source project that applies the gstack philosophy to academic research.

## Ways to Contribute

### Add a new skill

Each agent role is a `SKILL.md` file. To add a new one:

1. Create `skills/{skill-name}/SKILL.md`
2. Follow the format (see any existing skill for reference):
   - YAML frontmatter (name, description, version, tags)
   - Trigger conditions
   - Input format
   - Workflow steps
   - Output format
   - Pitfalls / notes
3. Add to `skills/README.md`
4. Submit a PR

### Improve an existing skill

Found a bug or want to improve a skill? PRs welcome.

### Add a new agent host

Currently built for Hermes Agent. Want to port to Claude Code, Codex, or OpenClaw? See gstack's [ADDING_A_HOST.md](https://github.com/garrytan/gstack/blob/main/docs/ADDING_A_HOST.md) for the pattern.

## Skill Guidelines

- **Self-contained**: each skill should work independently
- **Output-oriented**: every skill produces a structured report
- **No hardcoded secrets**: never include API keys or credentials
- **Generic examples**: use "Project A/B/C" not real project names
- **Multi-language aware**: English preferred, Chinese examples welcome

## Development Setup

```bash
# Clone
git clone https://github.com/SpencerRaw/academic-gstack.git

# Install skills to Hermes
cp -r skills/* ~/.hermes/skills/

# Verify
hermes skills list | grep -E "lit-reviewer|hypothesis|peer-review"
```

## License

MIT — see [LICENSE](LICENSE)
