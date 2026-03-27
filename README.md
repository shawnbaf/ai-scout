# AI Scout

Automated daily intelligence sweep for AI tooling and workflow changes. Runs as a CC cloud scheduled task.

## What It Does

- Monitors Claude Code releases, Anthropic updates, and ecosystem changes daily
- Evaluates findings against the founder's workflow templates (included in this repo)
- Sends a categorized Telegram digest at 11am
- Logs all findings for historical reference

## Setup

1. Cloud scheduled task clones this repo
2. Task runs daily at 11am, sends digest to Telegram via CC Channels
3. Findings logged to `findings/` directory

## Repo Structure

- `CLAUDE.md` — scout operating manual
- `findings/` — daily findings history
- `new-project-master.md` — full project bootstrap system template
- `project-audit.md` — audit checklist for existing projects
- `generic-project-instructions-template.md` — non-app project template
