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

### Workflows & Patterns (daily)

These search for what people are doing with the tools, not what changed in the tools.

| Search Query | Why It Matters |
|-------------|----------------|
| "Claude Code workflow tips" | Practitioner patterns, productivity tricks |
| "Claude Code multiple agents parallel" | Multi-agent orchestration patterns |
| "Claude Code frontend design" | UI/UX workflows, design-to-code patterns |
| "AI video creation workflow 2026" | Remotion, Playwright recording, demo generation |
| "solo developer AI productivity" | One-person team scaling patterns |
| "Claude Code hooks creative uses" | Community hook patterns we haven't thought of |
| "AI coding agent best practices" | General patterns applicable to our CC setup |
| "cursor vs claude code workflow" | Competitor workflows worth stealing |
| "AI tools for developers 2026" | New tools that could plug into our workflow |
| "remotion video automation" | Patterns beyond what our demo pipeline does |
| "Claude Code plugins best" | New plugins worth installing |
| "Claude Code skills community" | Community skill files that fill gaps in our setup |
| "Claude Code MCP servers useful" | MCP integrations that add real capability |
| "awesome claude code tools" | Curated tool lists — cherry-pick, don't bulk install |

Search HN, Reddit, and general web. Same evaluation criteria as releases — compare against templates, categorize. Skip noise aggressively using the Founder Profile filter below.

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

## What the Founder Is Building

The founder is building a one-person factory. Every tool in the system is a machine on the assembly line. The pattern across everything he's built:

1. **CC drives it.** If CC can't orchestrate it from CLI or script, he doesn't want it. No GUI-dependent tools, no manual dashboards.
2. **It produces a real artifact.** Videos, screenshot grids, health reports, digests, findings logs. Not things you look at — things that get used or shipped.
3. **It runs on autopilot once set up.** Design it once in Claude.ai → CC-PROMPT it → it runs forever via skills, hooks, or scheduled tasks.
4. **It consolidates, never fragments.** One doc not seven. One command not scattered scripts. If adding it means maintaining another thing, it better replace two things.
5. **It makes him literally faster.** Fewer steps between idea and shipped feature. Not "more informed" — faster.

When evaluating any finding, ask: "Would this significantly reduce the manual work a solo founder does today?" Full automation is ideal but not required — the founder still manually hands docs to CC, copies prompts between surfaces, and reviews before approving. The bar isn't zero manual steps. The bar is: does this tool make a workflow meaningfully faster or open a capability that wasn't practical before? If yes, it's signal.

## Founder Profile — Signal vs Noise Filter

Apply this filter to every finding before including it in the digest. When in doubt, skip it — one good finding beats five mediocre ones.

### Signal — always include:
- Reduces manual steps in an existing workflow (health system, UI review, screen design, demo video, scout itself)
- Patterns for running multiple CC agents on the same codebase without conflicts (worktrees, parallel tracks, subagent orchestration)
- Design-to-code workflows that are tighter than the current JSX artifact → CC-PROMPT pipeline
- Advanced CC skills/hooks/CLAUDE.md patterns — beginner tips are noise, creative uses of systems we already run are signal
- Local model tricks for 8GB VRAM (Ollama, llama.cpp, quantization breakthroughs, context window expansion)
- Remotion patterns beyond basic composition — dynamic scene generation, automated multi-format export, anything the demo pipeline doesn't already do
- Managing multiple projects as one person without multiplying maintenance
- Anything that makes "update once, apply everywhere" more real
- New CC features that affect scheduled tasks, hooks, channels, subagents, or skills — these are the systems we actively use
- New tools that could plug into the existing workflow — the way Remotion plugged into the demo pipeline. Look for tools that: solve a real problem the founder currently handles manually, work from CLI or have programmatic APIs (CC needs to drive them), don't require a team to operate, and have a free tier or one-time cost. Examples: video/media generation, design automation, screenshot/visual testing, deployment utilities, code generation, documentation generators, data seeding, anything CC could orchestrate.
- If a workflow pattern uses a tool we don't use, include the full finding — the tool might be worth evaluating

### Noise — always skip:
- Beginner tutorials ("how to install Claude Code", "getting started with CC")
- Generic AI hype ("AI will change everything", "10 ways AI boosts productivity")
- Tool comparisons for tools already evaluated and rejected
- Enterprise or team-specific workflows — the founder is solo
- SaaS tools that require ongoing subscriptions with no free tier and no clear ROI for a solo operator
- Cursor, Copilot, or Windsurf migration guides — committed to CC
- Prompt engineering basics
- "Awesome Claude Code" lists that are just link dumps
- Content marketing disguised as tips
- Anything the founder's system already does — don't report what we already built as a discovery

### Edge cases:
- If someone solved a problem we haven't hit yet but might, that's BOOKMARKED not OPPORTUNITY
- If a finding is stale (we already adopted it), skip it entirely — check the template docs first

## Telegram Digest Format

Send via a direct curl call to the Telegram Bot API:

```bash
curl -s -X POST "https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage" \
  -d chat_id="${TELEGRAM_CHAT_ID}" \
  -d text="<digest text>" \
  -d parse_mode="Markdown"
```

If `TELEGRAM_BOT_TOKEN` or `TELEGRAM_CHAT_ID` are not set, skip Telegram delivery entirely and note "⚠️ Telegram credentials not configured — digest saved to findings log only" in the findings log.

One line per finding. No version numbers, no source labels. Just what changed and why it matters to our workflow. Max 15 words per line. Don't tell us what to do — describe what it means. Details stay in the findings log.

Format:

```
🔍 AI Scout — [DATE]

🔧 TOOL UPDATES
⚡ ACTION NEEDED ([count])
1. ...
💡 OPPORTUNITY ([count])
2. ...

🧠 WORKFLOWS & PATTERNS
💡 WORTH TRYING ([count])
3. ...

📌 BOOKMARKED ([count])
4. ...

→ Details: findings/[DATE].md
→ Full breakdown: open task session at claude.ai/code/scheduled
```

If no findings: `✅ No changes. All systems current.`

Remember: one line per finding. No version numbers. Just what changed and why it matters to our workflow. Max 15 words per line. Details stay in the findings log.

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
