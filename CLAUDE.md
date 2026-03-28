# AI Scout — Automated Workflow Intelligence

Daily intelligence sweep that monitors AI tooling, Claude Code releases, and ecosystem changes. Evaluates findings against the founder's workflow templates and reports actionable digest to Telegram.

## How This Works

You are running as a CC cloud scheduled task. Every run:

1. Read the founder's current workflow templates from this repo
2. Search each source for updates since yesterday
3. Evaluate every finding against the templates — does it affect, improve, or obsolete anything?
4. Format a Telegram digest and send it
5. Log findings to `findings/` for historical reference

Everything lives in this single repo — operating manual, workflow templates, and findings log.

## Source Tiers

### Tier 1 — Check Every Run (daily)

These sources change the founder's daily work. Check all of them every run.

| Source | What to Search | Why It Matters |
|--------|---------------|----------------|
| CC Changelog | `https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md` | New CC features, fixes, breaking changes |
| CC Docs Changelog | `https://code.claude.com/docs/en/changelog` | Formatted release notes, new docs pages |
| Anthropic Blog | Search: `site:anthropic.com/research OR site:anthropic.com/news` | Major product launches, model releases, capability announcements |
| Releasebot Anthropic | `https://releasebot.io/updates/anthropic` | All Anthropic product releases tracked automatically |
| Hacker News AI | Search: `site:news.ycombinator.com claude code OR anthropic OR ai coding agent` | Where new tools trend before Twitter. Practitioner discoveries. |
| Reddit r/ClaudeAI | Search: `site:reddit.com/r/ClaudeAI` last 24h | Workflow tricks, undocumented features, community patterns |
| Playwright Releases | Search: `playwright releases changelog 2026` | UI review + demo recording pipeline dependency |

### Tier 2 — Check Weekly (Mondays only)

These affect specific projects or future plans. Only check on Monday runs.

| Source | What to Search | Why It Matters |
|--------|---------------|----------------|
| Next.js Releases | Search: `next.js releases changelog 2026` | App framework — breaking changes, new features |
| React Ecosystem | Search: `react 2026 new features releases` | Component patterns, hooks, server components |
| Remotion Releases | Search: `remotion video releases changelog 2026` | Demo video pipeline dependency |
| Ollama / llama.cpp | Search: `ollama releases OR llama.cpp releases 2026` | Local model routing on Alienware |
| Quantization News | Search: `TurboQuant OR PolarQuant OR KV cache compression llama.cpp 2026` | Would expand context windows within current VRAM envelope |
| Composio Updates | Search: `composio MCP updates 2026` | Remote MCP connector for Telegram in cloud tasks |

## Evaluation Criteria

For every finding, evaluate against the founder's templates in this repo:

- `new-project-master.md` — the full project bootstrap system (architecture, screen design, health system, ops pipeline, demo video, CLAUDE.md template)
- `project-audit.md` — the audit checklist for existing projects
- `generic-project-instructions-template.md` — non-app project template

### Evaluation Questions (ask for each finding)

1. **Does this change an existing workflow?** Does it affect how the bootstrap, health system, screen design, ops pipeline, demo video, or any other documented system works? If yes → `ACTION NEEDED`
2. **Does this enable something new?** Could this meaningfully improve an existing workflow, or does it enable something the founder has been waiting for (check the "On the horizon" items)? If yes → `OPPORTUNITY`
3. **Does this obsolete a workaround?** Is there something in the templates that exists as a workaround for a limitation that's now fixed? If yes → `ACTION NEEDED`
4. **Is this interesting but not urgent?** Worth knowing about, but no immediate workflow impact? → `BOOKMARKED`
5. **Is this noise?** Minor patch, marketing fluff, doesn't affect the founder's stack? → Skip entirely. Don't report it.

### Specific Things to Watch For

These are high-priority patterns the founder cares about. Flag immediately if found:

- **CC scheduled tasks changes** — any updates to cloud task capabilities, new environment options, MCP connector changes
- **CC hooks updates** — new hook types, hook improvements (founder uses git-guard, auto-format, doc-drift-reminder)
- **CC Channels / permission relay updates** — may affect future ops pipelines
- **CC subagent / teams improvements** — affects parallelization in CC-PROMPTs
- **New CC skills or skill system changes** — affects the self-growing skills architecture
- **Playwright breaking changes** — affects UI review route crawler and demo recording
- **Sentry SDK changes for Next.js** — affects health system Track 1
- **Remotion v4+ changes** — affects demo video pipeline
- **Model capability improvements** — especially context window, tool use, vision (affects what CC can do autonomously)
- **MCP protocol changes** — affects Composio integration and any MCP-based tooling
- **Token cost decreases** — founder is watching for when inline evaluator pattern becomes viable
- **TurboQuant/PolarQuant PRs in llama.cpp** — founder is explicitly monitoring for these
- **ghost-cursor-playwright updates** — affects demo recording human-like interactions

## Telegram Digest Format

Send via a direct curl call to the Telegram Bot API:

```bash
curl -s -X POST "https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage" \
  -d chat_id="${TELEGRAM_CHAT_ID}" \
  -d text="<digest text>" \
  -d parse_mode="Markdown"
```

If `TELEGRAM_BOT_TOKEN` or `TELEGRAM_CHAT_ID` are not set, skip Telegram delivery entirely and note "⚠️ Telegram credentials not configured — digest saved to findings log only" in the findings log.

Format:

```
🔍 AI Scout — [DATE]

[If findings exist:]

⚡ ACTION NEEDED ([count])
1. [Source] — [One-line description]. Impact: [which workflow/system affected]
2. ...

💡 OPPORTUNITY ([count])
3. [Source] — [One-line description]. Potential: [what it would improve]
4. ...

📌 BOOKMARKED ([count])
5. [Source] — [One-line summary]
6. ...

---
→ Open this run at claude.ai/code/scheduled to drill into any item
→ Bring findings to a project conversation for CC-PROMPT design

[If no findings:]

✅ No meaningful changes detected. All systems current.

[If Tier 2 day:]
📋 Weekly deep scan included (Next.js, Remotion, local models, quantization)
```

Keep it tight. One line per finding. The founder reads this on their phone.

## Findings Log

After sending the digest, save a copy to `findings/[YYYY-MM-DD].md` in this repo. Commit and push to `main`. This creates a searchable history of what was reported and when.

Format:
```markdown
# AI Scout Findings — [DATE]

## Action Needed
- [Full details for each item]

## Opportunities
- [Full details for each item]

## Bookmarked
- [Full details for each item]

## Sources Checked
- [List of URLs fetched with status]

## Evaluation Notes
- [Any context about why items were categorized as they were]
```

## Error Handling

- If a source is unreachable, note it in the digest footer: "⚠️ [Source] unreachable — will retry next run"
- If templates aren't found in this repo, send an error alert instead of a digest
- If Telegram delivery fails, log the digest to findings/ anyway so it's not lost
- Never skip the entire run because one source failed — report what you can

## What This Scout Does NOT Do

- It does not implement changes. It reports and recommends. The founder decides.
- It does not monitor the founder's app projects. It monitors the tools those projects use.
- It does not send alerts outside the daily schedule. One digest per day, not a firehose.
- It does not evaluate products/services the founder doesn't use. Stay focused on the stack.
