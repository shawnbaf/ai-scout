# AI Scout

Automated daily intelligence sweep for AI tooling and workflow changes. Runs as a CC cloud scheduled task.

## What It Does

- Monitors Claude Code releases, Anthropic updates, and ecosystem changes daily
- Evaluates findings against the AI Optimization Hub workflow templates
- Sends a categorized Telegram digest at 11am
- Logs all findings for historical reference

## Setup

1. This repo exists as the scout's home
2. Cloud scheduled task clones this repo + `ai-optimization-hub`
3. Task runs daily at 11am, sends digest to Telegram via CC Channels
4. Findings logged to `findings/` directory

## Repos

- **ai-scout** (this repo) — scout operating manual + findings history
- **ai-optimization-hub** — workflow templates (read-only, never modified by scout)
