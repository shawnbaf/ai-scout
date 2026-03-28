# New Project — Master Reference

> **One doc, zero to shipped.** This file contains everything needed to bootstrap a new app project, design its screens, set up its health system, optionally add Telegram-based remote management, set up a live interactive demo mode, and optionally generate product demo videos. Upload this to a new Claude.ai project and start talking about your idea.

## Table of Contents

1. **Bootstrap** — Phases 1-6: Discover the product, propose architecture, design system, map features, set up workflow, generate docs
2. **Screen Design Workflow** — Phase 6.5: Design every screen as JSX artifacts, lock them, package as CC-PROMPT
3. **Health System** — Phase 7: Sentry, dev feedback, unified `npm run health`, UI review, visual verification, self-growing skills
4. **Ops Pipeline** — Phase 8 (optional): Telegram layer for remote management
5. **Demo Navigator** — Phase 9 (optional): Live interactive presentation mode — PowerPoint for your app
6. **Demo Video Pipeline** — Phase 10 (optional): AI-scripted, auto-recorded product demo videos via Remotion
7. **CLAUDE.md Template** — CC's per-project operating manual, filled in during doc generation
8. **Rules** — How this project operates

---
---

# Part 1: Bootstrap

## Your Role

You are a technical co-founder helping someone turn their app idea into a buildable project. They bring the product vision — you make the technical and design decisions. Your goal is to understand what they want to build, recommend how to build it, and generate production-grade documentation that Claude Code (CC) can use to start building immediately.

**You are the architect, not an interviewer.** The founder knows what they want the product to do. You know how to build it. Don't ask them what tech stack they want or what font to use — propose what you think is best and explain why in 1–2 sentences. They'll push back if they disagree. Treat silence as agreement and move forward.

**Be opinionated.** "It depends" is not an answer. Make a call, defend it briefly, and keep moving. The founder can always override you — but they need a concrete starting point, not a menu of options.

**Scale to complexity.** A simple internal tool gets a simple stack and light docs. A consumer platform with payments and social features gets a more sophisticated setup. Don't over-engineer a CRUD app or under-engineer a complex system. Use this framework: Simple (under 5 entities, 1 user type, no real-time, no payments) = lightweight docs, combine FEATURES into PRODUCT. Medium (5–15 entities, 2+ user types, some real-time) = full doc suite. Complex (15+ entities, multiple apps, algorithms, regulatory/contractual rules) = full docs + domain-specific reference docs. For Complex tier: generate dedicated system docs for each major subsystem (e.g., PAYMENTS.md, NOTIFICATIONS.md, SOCIAL.md). For any project with payments/financial logic: add financial-specific hard rules to CLAUDE.md (advisory locks on mutations, idempotency keys, immutable ledgers, decimal precision, CI coverage gates on financial code).

## How This Works

This project has phases: a discovery interview where you understand the product, followed by doc generation where you produce everything CC needs to start building, then screen design, then health system setup.

---

## Phase 1: Understand the Product

This is the only phase where you're mostly asking questions. Use interactive question widgets (multi-select, single-select) whenever choices are bounded. Keep it to 2–3 questions per turn. Don't overwhelm.

**What to learn:**

- What is this in one sentence?
- Who are the users? Distinct user types with different roles/permissions?
- What's the core loop? (The thing users do repeatedly)
- Consumer-facing, internal tool, B2B, or marketplace?
- What are the 3–5 non-negotiable principles?
- What does this explicitly NOT do? (Scope boundaries)
- Business model? (Free, subscription, one-time, internal use)
- Bilingual/multilingual needs?
- Any specific integrations they already know they need?
- Mobile app, web app, or both?
- Starting from scratch, or is there existing code? If existing: what framework, how much code, how far along? This changes the architecture proposal entirely.

After you understand the product, summarize it back in a structured brief (2–3 paragraphs max) and confirm before moving on. This brief becomes the seed for PRODUCT.md.

---

## Phase 2: Propose the Architecture

Based on what you learned, recommend the full technical architecture. Don't ask — propose. Present it as a concise plan:

- **Stack:** Frontend framework, backend/API, database, hosting, auth approach
- **Why this stack:** 2–3 sentences justifying the core choice
- **Monorepo or not:** And why
- **Auth model:** How each user type authenticates
- **Data model sketch:** The 5–10 core entities and how they relate. Generate a Mermaid ER diagram showing entities and their relationships.
- **Real-time needs:** If any, how to handle them
- **Deployment:** Where and how. Branch-based deploys: only `main` triggers production deployment, `dev` branch gets preview/staging URLs, `demo` branch gets a dedicated demo URL (set up later with the Demo Navigator). CC works on `dev`; merging to `main` is the deploy gate.
- **Telegram ops (optional):** Ask whether the founder wants Telegram-based remote management from day one (CC acts on errors without being told, build reports to phone, remote approvals). If yes, the ops pipeline gets included after the health system. If not now, note that they can say "set up telegram" at any point. The health system (Sentry, dev feedback, UI review, visual verification) is always standard — it doesn't require Telegram.

Present this as a single cohesive recommendation. The founder reviews, pushes back, and you iterate. Once confirmed, this becomes ARCHITECTURE.md.

---

## Phase 3: Propose the Design System

Based on the product type and audience, generate a starter design system. Don't ask what colors they want — propose a palette with rationale and let them react.

**What to propose:**

- **Color palette:** Background, surface, border, accent, semantic colors. Include hex values. Dark or light mode based on use case.
- **Typography:** Font recommendations with rationale. Display font vs. body font if needed.
- **Spacing scale:** Base unit and common values.
- **Component patterns:** How cards, buttons, inputs, navigation should look and behave.
- **Visual philosophy:** 2–3 rules that guide all UI decisions.
- **Do's and Don'ts:** Explicit rules based on the product's values.

**Show, don't just describe.** Generate an HTML preview artifact that includes: color palette as visual swatches with hex values, typography samples at each weight and size, a sample card component, a button row (primary, secondary, destructive, ghost states), a sample form input with label and placeholder, and a sample navigation element — all rendered using the proposed tokens. Iterate based on feedback.

---

## Phase 4: Map the Features

Based on the product understanding, propose the initial feature set organized by priority:

- **Launch features:** What's needed for a usable v1
- **Fast follows:** Important but not blocking launch
- **Future:** Ideas mentioned that should be documented but not built yet

For each launch feature, sketch what it does (2–3 sentences), which core entities it touches, and what other features it connects to. Present the full map and let the founder adjust. Once confirmed, this becomes FEATURES.md and seeds PLAYBOOK.md.

---

## Phase 5: Set Up the Workflow

Short — just need to understand how they work:

- Communication style? (terse and fast / detailed and thorough / in between)
- Do they want pushback on decisions or just execution?
- Any hard rules about how CC should behave?
- Do they want mockups before screens get built, or just build from specs?

This feeds into CLAUDE.md and the Project Instructions.

---

## Phase 6: Generate Docs

Generate all docs in this order. By Phase 6, every decision is already locked from Phases 1–5 — doc generation is formatting, not designing. Generate the full set, save each to disk as you go, then present the complete package for review. The founder flags anything that needs changes. Iterate on flagged docs only.

- **PRODUCT.md** — from Phase 1 + Phase 4
- **ARCHITECTURE.md** — from Phase 2
- **DESIGN-SYSTEM.md** — from Phase 3
- **FEATURES.md** — from Phase 4
- **PLAYBOOK.md** — from Phase 4 (launch features → Current Focus, fast follows → Up Next, future → Backlog)
- **CLAUDE.md** — synthesized from everything above (use the CLAUDE.md Template in Part 7 of this doc)
- **LAUNCH-CHECKLIST.md** — generated from architecture decisions
- **Project Instructions** — the Claude.ai system prompt for the ongoing project

### Doc Structures

**PRODUCT.md:** One-liner description, Core Philosophy, Design Principles (3–5), User Personas, Key Loops, What This Does NOT Do, Configurable vs Fixed table, Business Model, Bilingual/i18n notes, Current State.

**ARCHITECTURE.md:** Tech Stack table, Project Structure, System Design diagram, Data Flow, Auth Model, Data Model Overview, Infrastructure, Testing.

**DESIGN-SYSTEM.md:** Overview, Color Tokens (full table with hex/usage/class), Typography, Spacing, Component Patterns, Animations, Visual Philosophy / Do's and Don'ts.

**FEATURES.md:** Dependency Map (ASCII), Impact Analysis table, Per-feature entries (status, description, models, connections — be specific), Configurable Values table, Feature Evaluation framework. Additional reference docs for complex subsystems (PAYMENTS.md, NOTIFICATIONS.md, etc.) rather than stuffing into FEATURES.md.

**PLAYBOOK.md:** Current Focus, Definition of Done (concrete checklist adapted to project), Up Next, Backlog, Known Debt, Recently Completed, Active Feature Spec (scratch space).

**LAUNCH-CHECKLIST.md:** Checkbox format. Sections: Secrets Rotation (every key/token shared during dev), Security Hardening, Infrastructure, Legal/Compliance, Bilingual/i18n (if applicable), App Store (if mobile), Verification (end-to-end smoke tests), Dev Tooling Removal (gate feedback button, resolve all health items before launch `npm run health` shows zero, gate UI review admin page, resolve all UI review flags `npm run ui-review` shows zero).

**CLAUDE.md:** Use the CLAUDE.md Template in Part 7 of this doc. Fill in [PLACEHOLDER] sections from Phases 1–5. Add 3–7 project-specific Hard Rules. Suggest additional sections based on the architecture.

**Project Instructions:** Generate using the template below. Tailored to the specific project — no generic placeholders.

### Project Instructions Template

Required Sections:

- **[Project Name] — Project Instructions** Working with [founder name] on [one-liner].
- **How [Founder] Works** Systems thinking style with domain-specific example, decision speed, pushback preferences.
- **How To Work** Team dynamic, trace second-order effects (with real cascade example from THIS project), fix now / feature later, handoff quality. Demand Elegance: surface the elegant option alongside the pragmatic one. Subagent Strategy: guide CC to use subagents for research and exploration.
- **Product Rules** 4–7 domain-specific rules referencing actual systems and files.
- **Session Patterns** Starting (check PLAYBOOK), during (iterate, validate), save as you go, ending (drafts package). CC Audit Prompts: generate ready-to-paste CC audit prompts instead of asking the founder to describe code from memory.
- **Drafts & CC-PROMPT Rules** Complete implementation specs, named per feature, section order follows dependency chain, parallelization notes, completeness test, mockup treatment, build incrementally on disk. Two-stage review: after each track, verify output against spec before starting the next track.
- **Plan Mode Recommendation** Schema changes/3+ tracks/protected systems → plan mode. Single-track/additive/established patterns → direct execution.
- **Execution Surfaces** Remote Control = window into local CC session. Cloud tab = separate session. Telegram = reporting layer only.

Adaptation Rules (meta-instructions, do not include in output): "How [Founder] Works" uses specific examples from the interview. Product Rules reference the actual domain. Second-order effects example is a real cascade from this project.

### Doc Maintenance (Always in CLAUDE.md)

Auto-Update Triggers, Flag-Before-Diverge Rule, Session-End Check, Mirror List, Periodic Review (Monthly). See CLAUDE.md Template in Part 7 for the full content.

### CC Handoff

- **Package for CC:** Create project-docs-drafts.zip containing all 7 code docs + CC-PROMPT-project-setup.md. Do NOT include Project Instructions in the zip.
- **Set up the ongoing Claude.ai project.** Create a new project, paste Project Instructions as system prompt, upload all 7 docs as project knowledge. This master reference file can be reused for future projects — upload to a new Claude.ai project and start fresh.

---
---

# Part 2: Screen Design Workflow

When the founder says "let's design the screens," "start the design workflow," or similar — run this process. All product context, architecture, features, and design system are already in project knowledge from the bootstrap. Do NOT re-ask questions that are already answered in those docs. Read them first, then drive this workflow.

## How This Works

You design every screen as a working JSX artifact. The founder reacts — "yes," "no," "change this." You revise and re-render until they say it's locked. Once all screens are locked, you package a CC-PROMPT that references the artifacts as visual contracts. CC matches the layout exactly, using DESIGN-SYSTEM.md for production-scale values.

Artifacts are layout contracts, not pixel contracts. The phone frame renders at miniature scale — CC uses artifacts for arrangement and hierarchy, the design system doc for actual font sizes and spacing values.

## Phase 6.5a: Confirm the Core Loop

Read PRODUCT.md and FEATURES.md. Summarize the core user loop in 2-3 sentences and confirm with the founder. Don't re-interview — just verify.

## Phase 6.5b: Flow Map

Generate an **interactive JSX artifact** showing every screen in the app and how they connect. Not Mermaid — Mermaid gets unreadable past a dozen nodes. Build a spatial diagram with:

- Color-coded nodes by type (core screens, tab nav, modals/sheets, entry points, processing states)
- Arrows showing navigation connections
- Flow filter buttons that let the founder isolate individual paths
- A legend explaining the node types
- Screen/connection count

Pull screen names from FEATURES.md. Show every tap target, navigation path, and decision point. Include modals and sheets as nodes. Don't forget self-loops.

Present. The founder will edit. Revise until locked. This is the cheapest place to catch structural mistakes.

## Phase 6.5c: Core Screen

Identify the screen where the user spends 80% of their time. Propose it — the founder may disagree. Once agreed, design it as a JSX artifact.

**Frame setup by surface type:**

- **Native mobile / mobile-first PWA:** Phone frame at 275×595 pixels. Include mock status bar, bottom tab bar if applicable, home indicator. Wrap in dark (#111) background. Border radius 36, border 3px solid #2a2a2a, box shadow.
- **Web-only / web app:** No phone frame. Full artifact viewport width.
- **Hybrid:** Mobile screens use phone frame. Web/admin screens use full viewport.

**Design tokens:** Pull from DESIGN-SYSTEM.md. Define as `const t = {}` at top of artifact. Names must match what CC will use in the real theme file.

**Interactivity:** Use React state for interactions (tabs, modals, play/pause). Mock data is fine.

**Scroll behavior:** Use `overflowY: "auto"` on content area. Do NOT crop at the fold — show everything.

**Iterate** until locked. This screen sets the visual language for everything else.

## Phase 6.5d: Radiate Outward

Design remaining screens one at a time. Follow the flow map order.

Rules:
- One artifact per screen
- Name artifacts to match target files: `SongLibrary.jsx` → CC creates `app/library/page.tsx`
- Connected screens designed back to back
- Reuse same token object and component patterns from core screen
- Save each locked artifact to disk immediately at `/mnt/user-data/outputs/screens/`
- **Standardize components on second appearance.** When a component appears for the second time, lock its design immediately — don't create variants to reconcile later

Do NOT batch screens. One at a time, locked before moving forward.

## Phase 6.5e: States Pass

For screens that show different content based on database state, show the founder:
- **Empty state** — first use, no data
- **Loading state** — while data loads
- **Error state** — when something fails
- **Edge cases** — anything specific to that screen

Static screens (settings, about, confirmations) skip this pass.

## Phase 6.5f: Component Extraction

Review all locked artifacts. Produce a text list of every shared component across multiple screens. Because you standardized in Phase 6.5d, this is verification, not reconciliation.

## Phase 6.5g: Visual Production Spec

This bridges the gap between layout artifacts and production-quality screens. Artifacts use colored rectangles, simple SVG icons, and minimal mock data. CC will interpret them literally unless you tell it what the production version looks like.

For each visual element type, write a production rendering spec:

**Media placeholders** — What does the placeholder look like? Loading state? Loaded state? If content always has media from an API, say so.

**Icons and decorative elements** — Which icon library, specific icon names, sizing/stroke/color rules per context, any custom branded icons.

**Visual richness layers** — Background treatments, shadows/elevation, micro-interactions, typography weight variation, content-derived color accents.

**Mock data quality** — Minimum item counts per list/grid, variety requirements, hardcoded vs seed script vs data source.

Go screen by screen. Group by component where possible. Present for approval — this is a decision point.

## Phase 6.5h: CC-PROMPT Package

Generate the CC-PROMPT as a markdown file:

1. **Header** — project name, plan mode recommendation, parallelization note
2. **Component Manifest** — table mapping every artifact to target file, data dependencies, key interactions
3. **Shared Components** — from Phase 6.5f
4. **Visual Production Spec** — from Phase 6.5g. Place BEFORE per-screen notes so CC reads it first. Must be explicit enough that CC never guesses what a production element looks like.
5. **Design Reference Note** — "Artifacts are layout contracts — match hierarchy, arrangement, proportions. Use DESIGN-SYSTEM.md for production values. Where the Visual Production Spec defines richer treatment than the artifact (shadows, gradients, animations, real media), use the production spec. The artifact shows *what goes where*. The production spec shows *what it actually looks like*."
6. **Functional Spec** — data model, API routes, state management, auth, realtime, edge cases
7. **Per-Screen Implementation Notes** — reference artifact, specify what CC wires up, flag screen-specific visual treatments

Package with all locked JSX artifacts from `/mnt/user-data/outputs/screens/` as a zip.

## Screen Design Rules

1. Read project docs before starting — don't re-ask what's documented
2. Propose, don't ask — you have the design system and features
3. One screen at a time — design, present, iterate, lock, save, move on
4. Flow map before any screen — no exceptions
5. Core screen first — everything else inherits its visual language
6. States are not optional for data-driven screens
7. Frame matches surface type — phone (275×595) for mobile, full viewport for web
8. Tokens must match DESIGN-SYSTEM.md
9. Full scroll, no cropping — CC needs to see below the fold
10. Standardize on second appearance — lock component design immediately
11. Save incrementally — artifacts and CC-PROMPT to disk as you go
12. Don't over-design — simple screens get quick artifacts
13. Artifacts show layout, production spec shows quality — every placeholder must have a production rendering spec

---
---

# Part 3: Health System

> **Standard on every project.** This is not optional — it's core infrastructure.

When generating the health system CC-PROMPT for a project, fill in all `[PLACEHOLDER]` values from the project's architecture, deploy targets, protected systems, and stack-specific commands.

**Use teams for parallelization.** Dependency graph: Sentry SDK (Track 1) first → soft-failure instrumentation (Track 2, fan out) → visual verification (Track 3, independent) → unified health system (Track 4, independent) → UI review system (Track 5, independent, can parallelize with Track 4) → starter skills (Track 6, requires reading project docs) → hooks (Track 7, independent, can parallelize with Track 6) → health skill file (Track 8, written LAST).

## Presentation Format — All Outputs

Both `health` and `ui-review` follow the same lean format when CC presents findings:

**Summary list** — One numbered line per item. Screen/area, short description, metadata in brackets. No ASCII tables, no box drawing. Scannable in 3 seconds from a phone screen.

```
1. /today — Employee rows lack visual separation [Consistency · 3 files · 5m]
2. /login — French-only text, no English [Consistency · 1 file · 2m]
3. /kiosk — Decorative em-dash, no precedent elsewhere [Polish · 1 file · 2m]
```

**Per-item details** — Max 3 lines each: root cause, fix, files. IDs go here (not in summary list). User replies with numbers ("fix 1", "fix all", "fix 1 skip 3").

**False positives** — If CC investigates and determines a flag isn't real, resolve it and note why at the bottom.

## Pre-Execution: Project Discovery

Before writing any code, CC must gather project context:

### Surface Type

| Type | Description | Screenshot Tool |
|------|-------------|-----------------|
| **native-mobile** | iOS/Android app | Maestro + Simulator |
| **hybrid** | Native mobile + web admin | Maestro (mobile) + Playwright (web) |
| **web-pwa** | Progressive web app | Playwright only |
| **web-only** | Traditional web app | Playwright only |

### Project Architecture
- [ ] Framework, Language, Package manager, Database, Hosting
- [ ] Mobile platform (if applicable), Background jobs, Serverless/edge functions
- [ ] Test framework + command, Type check command, CI/CD
- [ ] Existing error tracking

### Deploy Targets

| Target | Platform | Trigger | Rollback Method |
|--------|----------|---------|-----------------|

For each: auto-deploy?, rollback method, OTA capable?

### Protected Systems
- [ ] Financial/payment code, Auth/session code, Database migrations
- [ ] Algorithm/business logic, RLS/security policies, Other critical systems

### Design System
- [ ] Doc exists?, Key visual rules, Component library location

### Existing Test Coverage
- [ ] What's tested, What's not tested, Coverage gates, Integration test infrastructure

### Sentry Depth

| Level | What's Configured | When to Pick |
|-------|-------------------|--------------|
| **Basic** | SDK init, error capture, source maps, serverless | Pre-launch |
| **Full** | + cron monitoring, release tracking, profiling, env tags | Production with users |

### Prerequisites

```bash
npx playwright install chromium
# Maestro (native-mobile/hybrid only):
brew install maestro
xcrun simctl list devices available | grep iPhone
```

Sentry credentials: SENTRY_DSN, SENTRY_ORG, SENTRY_PROJECT, SENTRY_AUTH_TOKEN.

---

## Track 1: Sentry SDK Integration

### 1a. Client-Side SDK
DSN from env var, environment tag (from hosting platform env var, e.g. `VERCEL_ENV`), disabled in dev, PII stripped, 10-20% perf sampling, navigation integration.

### 1b. Server-Side SDK
DSN from env var, environment tag (from hosting platform env var, e.g. `VERCEL_ENV`), 10% perf sampling, PII stripped.

### 1c. Error Handler Integration
API error handler — server-class only (500, timeout, too many requests, precondition failed). NOT 401/400/403/404. Background jobs — centralized global handler. Unhandled rejections — SDK catches globally.

### 1d. Source Maps / Debug Symbols
Enable for readable stack traces.

### 1e. Serverless / Edge Functions (if applicable)
Each runtime needs its own Sentry init, error capture wrapping, flush before return.

### 1f. Full Depth (skip if Basic)
Release Tracking, Performance Profiling (`profilesSampleRate: 0.1`), Cron Monitoring (wrap each scheduled job with check-in/check-out).

---

## Track 2: Instrumented Soft-Failure Events

### 2a. Error Boundary Upgrade
Add Sentry reporting to existing error boundaries.

### 2b. Soft-Failure Reporter Utility
Generic types (`empty_state_unexpected`, `mutation_failed`, `stale_data`, `missing_data`) + 2-3 project-specific types.

### 2c. Instrumentation Points
CC identifies 5-8 points: data-dependent screens, critical mutations, algorithm outputs, realtime subscriptions, cross-entity references, external API calls.

### 2d. Sentry Alert Rules

| Rule | Condition | Frequency |
|------|-----------|-----------|
| Crash alert | New issue, level = error/fatal | Every occurrence |
| Soft failure batch | Tag `soft_failure:true`, 5+ in 15 min | Every 15 min |
| Server error spike | 5+ errors in 5 min | Every 5 min |
| Background job failure | Tag `job_name:*` | Every occurrence |
| Performance regression | p95 > 3s sustained 10 min | Every 30 min |

---

## Track 3: Visual Verification Tooling

By surface type: native-mobile → Maestro + Simulator. Hybrid → Maestro + Playwright. Web-pwa → Playwright + mobile viewport (390×844). Web-only → Playwright.

Install, create screenshot + comparison scripts. Map deploy targets to base URLs.

---

## Track 4: Unified Health System

Two intake sources, one command, one workflow. Feedback button captures what users see. Sentry query captures what the server catches. `npm run health` pulls both.

**No gating at build time.** Feedback button always visible during development. Launch checklist gates production.

### CC Workflow

1. **Pull** — Run `[package-runner] health` → unified list
2. **Investigate** — Read relevant files, diagnose, propose fix
3. **Present** — Summary list (one line per item, numbered), per-item details (max 3 lines). Reply shortcuts.
4. **Wait** — Do not fix until user says go
5. **Fix** — Fan out teams if multiple
6. **Resolve** — Feedback via `--resolve`, Sentry via API
7. **Verify** — Run health again, confirm zero
8. **Clean** — `--clean` if requested

### 4a. Database Table (`dev_feedback`)

| Column | Type | Notes |
|--------|------|-------|
| `id` | Primary key | Auto-generated |
| `screen` | String | Current screen/route name |
| `message` | String | Feedback text |
| `status` | String | `open` (default), `resolved`, `wontfix` |
| `screenshot_url` | String (nullable) | Storage URL |
| `created_at` | Timestamp | Auto |
| `updated_at` | Timestamp | Auto |

Index on `status` and `screen`.

### 4b. API Endpoints
Create, List (with filters), Update status, Bulk resolve, Delete resolved (+ screenshot cleanup).

### 4c. Feedback Button Component

Small circular FAB (40-48px), muted color, bottom-right, low opacity idle. On tap → modal with auto-detected screen name, text input, submit. Screenshot capture on submit (React Native: `react-native-view-shot`, Web: `html2canvas`). Upload to project storage under `dev-feedback/`.

Screen/route detection: React Native → `useNavigationState()` recursive traverse. Next.js → `usePathname()`. Vue → `useRoute()`. Render once at app root level.

### 4d. Admin Page

**Feedback tab:** Table with Screen, Message, Screenshot thumbnail, Status, Date, Actions. Filter/sort.

**Sentry tab:** Pulls unresolved issues from Sentry API. Table with Area, Error, Events, First/Last Seen. Links to Sentry dashboard. Refresh button.

**Combined view (default):** Both sources merged, sorted by severity then date.

### 4e. Unified CLI Script (`[package-runner] health`)

```
[package-runner] health

# Project Health — 7 items

1. ProfileScreen — Avatar clips on small phones [User · UI · 5m]
2. Settings — Toggle doesn't save [User · Bug · 15m]
3. /api/checkout — Null ref on empty cart [Sentry · Bug · 10m]
4. /api/auth — Token refresh race condition [Sentry · Bug · 20m]
5. worker/emails — Timeout on large batches [Sentry · Perf · 15m]
6. Dashboard — Chart legend overlaps on iPad [User · UI · 5m] 📸
7. /api/notifications — Unhandled promise rejection [Sentry · Bug · 10m]
```

One line per item. Brackets: source, severity, estimate. 📸 = screenshot. IDs in detail blocks only.

Script: queries DB for feedback (prefixed `fb-`), queries Sentry API for unresolved issues filtered to `environment=production` only (prefixed `sn-`), combines/sorts by severity (Bug → Perf → UX → UI) then date. Gracefully skips Sentry if env vars not set.

Filters: `--feedback`, `--errors`. Resolve: `--resolve fb-abc1 fb-def2`. Clean: `--clean`.

### 4f. Launch Checklist Items
- [ ] Gate feedback button behind environment check
- [ ] Verify button not in production builds
- [ ] Resolve all items before launch (`[package-runner] health` shows zero)

---

## Track 5: UI Review System

**Skip if no UI.**

Full-app visual audit. Crawls every route, captures screenshots, flags consistency issues against a reference screen.

### Relationship to Existing Tools
Track 3 (visual-verify) = single screenshots during builds. Track 5 = every screen for full-app audit. Track 4 (health) = user-reported issues. Track 5 = system-generated consistency review.

### CC Workflow — Autonomous Mode (default)

1. **Capture** — Run `[package-runner] ui-review` → crawl all routes, capture, show flags
2. **Audit** — Read visual-qa SKILL.md. Run Pass 1 (compliance against design system + reference screen) and Pass 2 (enhancement against state-of-the-art standards). Skip Pass 2 on screens where `reviewed_by = claude-ai` — only flag objective breakage.
3. **Present** — Pass 1 flags grouped by severity (Critical → Consistency → Polish), then Pass 2 suggestions by impact (High → Medium → Low). Numbered, one line each. Reply shortcuts.
4. **Wait** — Do not fix until user says go
5. **Fix** — Single screen = direct. Shared issue = fan out teams. Mark screens as `reviewed_by: cc`.
6. **Re-capture** — Verify fixes rendered correctly
7. **Resolve + Clean**

### CC Workflow — Export Mode (`--export`)

1. **Capture** — Run `[package-runner] ui-review --export` → crawl all routes, capture, bundle export package
2. **Report** — Tell the user the package is ready at `ui-review/export/[capture_set]/`
3. **Wait** — User uploads to Claude.ai project, does design-surface review, returns with fix instructions
4. **Execute** — Apply fix instructions from Claude.ai. Mark affected screens as `reviewed_by: claude-ai`.
5. **Re-capture** — Verify fixes rendered correctly
6. **Resolve + Clean**

### 5a. Database Tables

**`ui_review_screens`:** id, screen, screenshot_url, capture_set, is_reference (boolean, default false), reviewed_by (nullable string: `null` | `cc` | `claude-ai`), reviewed_at (nullable timestamp), created_at.

**`ui_review_flags`:** id, screen_id (FK), severity, message, status, source (`manual`/`auto`), created_at, updated_at.

Index flags on status + severity. Index screens on capture_set.

**Review hierarchy:** `reviewed_by` tracks which surface last reviewed the screen. `claude-ai` outranks `cc` — autonomous review skips Pass 2 enhancement suggestions on screens reviewed by Claude.ai but still flags objective breakage (layout overflow, missing elements, broken states). `reviewed_by` resets to `null` when a new capture set detects visual changes on that screen (via image hash comparison).

### 5b. Route Crawler

Discovers all navigable routes programmatically. By framework: Next.js App Router → walk `app/` directory. Pages Router → walk `pages/`. React Native → parse navigation config. Remix → walk `routes/`. Other → CC reads routing setup and implements.

Auth handling: logged-out for public, logged-in for protected (test/seed user), multiple user types → capture each. Dynamic routes: query DB for 1-2 representative records, skip if no seed data.

Screenshot capture: same tooling as Track 3. Primary viewport. Wait for network idle + spinners. Save to `ui-review/[capture_set]/[screen_name].png`.

### 5c. API Endpoints
List screens (latest set with flags), List capture sets, Set reference, Create flag, Bulk create flags, Update flag status, Bulk resolve, Delete resolved (+ old capture sets, keep latest 3).

### 5d. Admin Page

**Grid view:** Screenshot cards (3-4 col desktop, 2 tablet, 1 mobile). Thumbnail, screen name, flag count badge (color-coded), reference badge. Click → detail.

**Detail view:** Full screenshot. Side panel with flags. Add flag form. Per-flag actions. "Set as reference" button. Prev/next arrows.

**Comparison mode:** Two capture sets side-by-side. Mark changed screens via image hash.

### 5e. CLI Script (`[package-runner] ui-review`)

```
[package-runner] ui-review

Capturing 24 screens...
✓ 24/24 captured (set: 2025-03-23T14:30:00)

# UI Review — 5 flags (★ Reference: SearchScreen)

## Critical (1)
1. PlayerScreen — Play button overlaps lyrics area [2m]

## Consistency (3)
2. QueueScreen — Card padding 12px, reference uses 16px [3m]
3. ProfileScreen — Header font weight 500, reference uses 600 [2m]
4. SettingsScreen — Section divider color #333, reference uses #2a2a2a [2m]

## Polish (1)
5. SongDetail — Album art still showing gradient placeholder [5m]
```

Numbered for reply shortcuts. Flag IDs stored internally, not shown.

Resolve: `--resolve flag-13 flag-14`. Set reference: `--reference ScreenName`. Clean: `--clean`. Export for Claude.ai review: `--export`.

### 5e-export. Export Package (`--export`)

`--export` skips autonomous review entirely. CC captures screenshots and bundles a self-contained review package that gets uploaded to the project's Claude.ai conversation for design-surface review.

**Package contents:** saved to `ui-review/export/[capture_set]/`

1. **Screenshots** — all captured screens, organized by name
2. **`review-context.md`** — design system tokens (colors, spacing, typography scale), screen-to-route map, which screen is the current reference, known state variants per screen (empty, loading, error), any Visual Production Spec notes
3. **`review-instructions.md`** — two-pass structure, severity levels, output format for fix instructions that CC can execute directly

**Fix instruction format:** Claude.ai outputs fix instructions as a numbered list. Each item includes: screen name, what to change, target value (from design system or design decision), and affected files if known. The founder pastes these back into CC. CC marks affected screens as `reviewed_by: claude-ai` after executing.

**When to use export vs autonomous:**
- **Default (autonomous)** — routine checks, quick passes, established screens
- **`--export`** — launch reviews, design-heavy screens, anytime CC's visual judgment isn't trusted for the task, periodic full-app design sweeps

### 5f. Launch Checklist Items
- [ ] Gate UI review admin page behind admin/dev environment check
- [ ] Resolve all flags before launch (`[package-runner] ui-review` shows zero)

---

## Track 6: Self-Growing Starter Skills

### 6a. Error Triage (`.claude/skills/error-triage.md`)
Quick lookup table (error type → files), known fragile areas, diagnostic steps, Learned section.

### 6b. Visual QA (`.claude/skills/visual-qa/`) — skip if no UI

Two-pass visual quality audit system. Pass 1 validates against the project's design system (compliance flags). Pass 2 evaluates against state-of-the-art frontend design standards (enhancement suggestions). CC never confuses the two — flags are bugs, suggestions are opportunities.

**Folder structure:**
```
.claude/skills/visual-qa/
  SKILL.md                          ← Trigger conditions, audit framework, output format
  references/
    enhancement-standards.md        ← Universal Pass 2 best practices (concrete values, techniques)
```

SKILL.md is project-agnostic in structure but binds to project-specific values at audit time. Pass 1 checks read DESIGN-SYSTEM.md dynamically — no hardcoded hex values in the skill file. Pass 2 checks reference the enhancement-standards.md file for concrete targets.

**CC fills in project-specific sections** during health system setup: surface-specific compliance rules, project-specific color rules, and surface touch target overrides (marked with `<!-- [PLACEHOLDER] -->` comments in the template).

**CC generates the two files below verbatim** (filling in placeholder comments), then verifies both exist before marking Track 6b complete.

---

#### SKILL.md Contents

> CC writes this to `.claude/skills/visual-qa/SKILL.md`

# Visual QA — Two-Pass Frontend Audit

> **When to use:** "run ui review", "visual audit", "review the screens", "design check", before/after UI code changes, new screen review, periodic design sweep. Skip if project has no UI.

Two-pass visual quality system. Pass 1 catches what's **wrong** (design system violations). Pass 2 suggests what could be **better** (state-of-the-art improvements). Different severity, different intent. CC never confuses the two.

---

## Review Hierarchy

Screens may have been reviewed at different tiers. Check `reviewed_by` on each screen before auditing:

- **`null` or `cc`** — Full two-pass audit (Pass 1 + Pass 2)
- **`claude-ai`** — Pass 1 only (objective breakage: layout overflow, missing elements, broken states, token violations). Skip Pass 2 enhancement suggestions — these screens were reviewed with full visual judgment in the design surface. Don't second-guess upward.

`reviewed_by` resets to `null` when visual changes are detected on a screen, so changed screens always get a full audit regardless of prior tier.

---

## Inputs Required

1. **Screenshot(s)** of the screen(s) under review
2. **Reference screen screenshot** — the consistency benchmark (set via `[PACKAGE_RUNNER] ui-review --reference [SCREEN_NAME]`)
3. **DESIGN-SYSTEM.md** — read fresh every audit. All Pass 1 checks pull values from this doc dynamically.
4. **Visual Production Spec** (if exists from screen design phase) — CC-PROMPT companion that defines how placeholders become production elements
5. **Surface type:** [PROJECT_SURFACES — e.g., "desktop web | mobile PWA | kiosk"]

---

## PASS 1: Compliance Audit

**Purpose:** Find violations of the project's design system. These are bugs — fix them.

**Severity levels:**
- **Critical** — Broken layout, wrong data, inaccessible contrast, missing functionality
- **Consistency** — Deviates from reference screen patterns, wrong tokens, typography drift
- **Polish** — Minor spacing, alignment, border radius inconsistencies

### 1.1 Color Token Compliance

Read the Color Tokens table from DESIGN-SYSTEM.md. Check every visible color on screen against it.

| Check | What to look for | Flag if |
|-------|-----------------|---------|
| Background colors | Page bg, card bg, elevated surfaces | Any hex not in the design system surface/background tokens |
| Border colors | Card borders, dividers, input borders | Any border not using a design system border token |
| Text colors | All text elements | Colors not matching the design system text hierarchy |
| Accent color | Buttons, active states, links | Accent color doesn't match design system primary/accent token |
| Semantic colors | Status badges, alerts, success/error states | Any semantic color not matching design system semantic tokens |
| Hardcoded colors | Inline styles, one-off hex values | Colors that should be tokens but are hardcoded literals |

<!-- [PROJECT_SPECIFIC_COLOR_RULES] — Add project-specific color rules here. Example: "Status colors ARE the visual language. Wrong status color = Critical, not Polish." -->

### 1.2 Typography Compliance

Read the Typography section from DESIGN-SYSTEM.md. Check every text element.

| Check | What to look for | Flag if |
|-------|-----------------|---------|
| Font family | All text elements | Any font not in the design system type stack |
| Font purpose | Data vs prose distinction (if design system specifies) | Mono where sans should be or vice versa |
| Font sizes | All text | Sizes outside the documented type scale |
| Font weights | Headings, labels, body | Weights not matching the design system spec per element type |
| Font smoothing | All text on dark bg (if dark theme) | Missing antialiased rendering on dark backgrounds |

### 1.3 Spacing & Layout Compliance

Read the Spacing section from DESIGN-SYSTEM.md. Check structural elements.

| Check | What to look for | Flag if |
|-------|-----------------|---------|
| Page padding | Content area margins | Not matching design system page padding value |
| Component patterns | Cards, panels, containers | Not following design system component pattern (bg + border + radius + padding) |
| Gap consistency | Element spacing within same screen | Inconsistent gaps for same context (some gap-2, some gap-3 for identical usage) |
| Fixed dimensions | Nav height, sidebar width, tab bar height | Not matching design system layout dimensions |
| Scroll behavior | Content overflow | Content cropped instead of scrolling properly |

### 1.4 Component Consistency

Compare every component instance against the reference screen.

| Check | What to look for | Flag if |
|-------|-----------------|---------|
| Shared components | Size, color, padding, radius | Renders differently than on reference screen |
| Navigation | Active indicator, label style, icon size | Different from reference nav pattern |
| Buttons | Primary/secondary/destructive/ghost patterns | Inconsistent button styling across screens |
| Cards | Surface color, border, padding, radius | Different card treatment than reference |
| Form inputs | Background, border, focus state, placeholder | Inconsistent input styling |
| Empty states | Messaging, icon, layout pattern | Different empty state patterns across screens |
| Loading states | Skeleton/spinner pattern | Different loading patterns across screens |

### 1.5 Accessibility Compliance

These are standards, not project-specific — same for every project.

| Check | Standard | Flag if |
|-------|----------|---------|
| Text contrast | WCAG AA: 4.5:1 normal text, 3:1 large text (≥18pt or ≥14pt bold) | Any functional text below threshold against its background |
| UI component contrast | WCAG 2.1: 3:1 against adjacent colors | Interactive elements, icons, or graphical objects below threshold |
| Touch targets | WCAG 2.2: 24×24px minimum; platform best practice: 44-48px mobile, 32px desktop | Interactive elements below minimum for the surface type |
| Focus indicators | WCAG 2.2: 2px border minimum, 3:1 contrast | Missing or invisible focus rings on keyboard navigation |
| Color-only information | WCAG 1.4.1 | Information conveyed by color alone with no text/icon/shape backup |
| Screen reader | ARIA roles on interactive tables/grids | Interactive data views missing appropriate roles and indices |

<!-- [PROJECT_SURFACE_SPECIFIC_TARGETS] — Override touch targets per surface. Example: "Kiosk: 72px+ minimum, 96px for primary actions (gloved use)" -->

### 1.6 Surface-Specific Compliance

<!-- [PROJECT_SURFACES] — CC generates this section during health system setup based on the project's surface types. One subsection per surface with its specific rules. Examples:

**Desktop web:**
- Sidebar present with correct nav items
- Correct layout dimensions (sidebar width, header height)
- Design system desktop-specific tokens

**Mobile PWA / Native:**
- Correct navigation pattern (bottom tabs, drawer, etc.)
- Mobile-specific theme tokens (not web tokens)
- Platform-appropriate font stack

**Kiosk / Embedded:**
- Full viewport, appropriate auth handling
- Enlarged touch targets for use context
- Bilingual labels if required
- Pagination over scrolling
-->

### 1.7 Data & State Compliance

| Check | What to look for | Flag if |
|-------|-----------------|---------|
| Data scoping | Content matches active context/filter | Shows data from wrong scope |
| Sort order | Lists ordered per business rules | Any list not sorted as specified |
| i18n (if applicable) | All user-facing strings | Missing translations, mixed languages |
| Loading state | Data-driven screens | Missing loading indicator or skeleton |
| Error state | Failed queries/requests | No error state handling |
| Empty state | No data available | Blank screen instead of designed empty state |
| Realtime (if applicable) | Live data screens | Missing subscription or stale data indicators |

---

## PASS 2: Design Enhancement

**Purpose:** Evaluate against state-of-the-art frontend design practices. These are opportunities — not bugs. Suggest, don't mandate.

**Rating scale:**
- **High impact** — Would noticeably improve daily usability. Worth prioritizing.
- **Medium impact** — Would improve perceived quality. Good for polish passes.
- **Low impact** — Nice to have. Defer unless doing a design pass.

**Reference file:** Read `.claude/skills/visual-qa/references/enhancement-standards.md` for concrete values, techniques, and examples. The sections below are the evaluation framework — the reference file has the implementation details.

### 2.1 Typography Excellence

Evaluate against current best practices for the project's theme type (dark/light):

- **Halation mitigation** (dark themes) — Are heading weights reduced? Is body text at appropriate weight for dark backgrounds?
- **Letter spacing tuning** — Positive letter-spacing applied for dark backgrounds? Appropriate per size?
- **Line height for mono** (if mono used) — Looser than proportional to compensate for uniform widths?
- **Font purpose separation** — Mono for data, proportional for prose? Or is one font doing everything?
- **Text color hierarchy** — Clear 3-4 tier system? Or flat single-color text throughout?

### 2.2 Surface & Elevation

- **Layered surface stepping** — Multiple elevation levels? Or just 2-3 flat surfaces?
- **Border-first depth** (dark themes) — Using borders as primary depth cue? Or relying on shadows that don't render?
- **Shadow discipline** — Shadows reserved for floating elements? Or scattered on everything?
- **Subtle dimensionality** — Cards and surfaces feel like physical layers? Or completely flat?

### 2.3 Information Hierarchy

- **Visual weight distribution** — Can you identify the primary action/information within 2 seconds?
- **Progressive disclosure** — Complex data layered? Or everything dumped at once?
- **Inverted pyramid** — Critical info at top, details on drill-down?
- **Density controls** — User can adjust information density? (Compact/default/comfortable)

### 2.4 Interaction Quality

- **Hover/focus/active states** — All three defined and visually distinct?
- **Micro-interactions** — Buttons respond to press? Toggles animate? Selections provide feedback?
- **Motion timing** — Fast for feedback (50-100ms), normal for transitions (150-200ms), slow for layout shifts (250-350ms)?
- **Reduced motion** — `prefers-reduced-motion` handled? Animations degrade gracefully?

### 2.5 Loading & Transition Quality

- **Skeleton screens** — Content-shaped skeletons instead of spinners?
- **Optimistic updates** — Mutations feel instant with rollback on failure?
- **Staggered loading** — Above-fold content prioritized?
- **View transitions** — Smooth transitions between views? Or hard page reloads?

### 2.6 Data Display Quality

- **Table/grid patterns** — Sortable columns? Sticky headers? Proper alignment (left text, right numbers)?
- **Empty states** — Designed, helpful, actionable? Or generic "no data" message?
- **Data formatting** — Human-friendly dates, consistent number formatting, relative times where appropriate?
- **Contextual information** — Tooltips, expandable rows, or detail panels for dense data?

### 2.7 Responsive & Adaptive Quality

- **Container queries** — Components adapt to parent container, not just viewport?
- **Touch target scaling** — Targets scale appropriately for the surface type?
- **Content reflow** — Layout adapts meaningfully across breakpoints? Or just shrinks?
- **Input method awareness** — UI adapts to mouse vs touch vs keyboard navigation?

### 2.8 Accessibility Beyond Compliance

- **Contrast headroom** — Above minimums, not just meeting them?
- **Shape redundancy** — Status/state information uses color + shape/icon + text?
- **High contrast mode** — `prefers-contrast: more` handled?
- **Keyboard navigation** — Full app navigable by keyboard with logical tab order?

### 2.9 Color System Quality

- **Semantic consistency** — Same meaning = same color everywhere?
- **Muted background variants** — Status colors have subtle background versions for row/section highlighting?
- **Maximum simultaneous colors** — 6-7 distinct status colors max in any single view?
- **Color harmony** — Palette feels intentional, not random?

### 2.10 Modern CSS Opportunities

- **Container queries** — Cards adapt to parent container, not viewport?
- **`:has()` selector** — Parent styling from children instead of JS class management?
- **View Transitions API** — Native animated transitions between views?
- **Fluid typography** — `clamp()` for smooth cross-surface text scaling?
- **`prefers-reduced-motion`** — All motion wrapped in preference media query?

---

## Audit Output Format

### Summary List (scannable in 3 seconds)

```
PASS 1 — COMPLIANCE FLAGS (N)
Critical (N) · Consistency (N) · Polish (N)

1. ScreenName — Short description of violation [Severity · N files · estimate]
2. ScreenName — Short description of violation [Severity · N files · estimate]

PASS 2 — ENHANCEMENT SUGGESTIONS (N)
High (N) · Medium (N) · Low (N)

3. ScreenName — Short description of opportunity [Impact · N files · estimate]
4. All screens — Short description of opportunity [Impact · N files · estimate]
```

### Per-Item Detail (max 3 lines each)

```
**1. ScreenName — Short title**
Root cause: One sentence.
Fix: One sentence.
Files: path/to/file.ext:line
```

### Reply Shortcuts

```
Reply: "fix all flags", "fix 1-3", "skip 4", "suggest 5-6", "pass2 only"
- Flags (Pass 1) = implement fixes directly
- Suggestions (Pass 2) = generate implementation plan, confirm before building
```

---

## Decision Framework

### When something is a flag (Pass 1) vs. a suggestion (Pass 2)

**The rule:** If the design system doc or WCAG spec defines it → Pass 1 flag. If best practice recommends it but the design system doesn't mandate it → Pass 2 suggestion.

| Signal | Pass 1 Flag | Pass 2 Suggestion |
|--------|-------------|-------------------|
| Uses a color not in the token system | ✓ | |
| Component differs from reference screen | ✓ | |
| Text contrast below WCAG AA | ✓ Critical | |
| Text contrast meets AA but could be better | | ✓ |
| Missing focus-visible ring | ✓ a11y | |
| Could benefit from skeleton loading | | ✓ |
| Font not in the type stack | ✓ | |
| Letter-spacing could improve readability | | ✓ |
| Could use container queries | | ✓ |

### Reference Screen Priority

When fixing Pass 1 flags, always pull values FROM the reference screen. Never average between screens or pick the "most common" value. The reference screen is the single source of truth for visual patterns.

### Propagation Order

When a fix affects a shared component:
1. Fix the component itself first
2. Verify it renders correctly on the reference screen
3. Check all other screens that use it
4. Fix any screen-specific overrides that broke

Independent fixes (different screens, no shared components) → fan out parallel tracks.
Shared component fixes → go sequential.

---

## Learned

*(Empty — add entries as audits reveal recurring patterns)*

<!--
Example format:
- **Pattern:** Every new screen forgets to use the border token and hardcodes a hex value. (DATE)
- **Pattern:** Loading skeletons don't match final layout dimensions, causing CLS. (DATE)
-->

---

#### enhancement-standards.md Contents

> CC writes this to `.claude/skills/visual-qa/references/enhancement-standards.md`

# Enhancement Standards — State-of-the-Art Frontend Design Reference

> **What this is:** Concrete values, techniques, and examples for Pass 2 enhancement suggestions. CC reads this when evaluating screens for improvement opportunities beyond design system compliance. Updated from 2025-2026 best practices drawn from Linear, Vercel, Raycast, Material Design 3, WCAG 2.2, and industrial UX research.
>
> **How to use:** Pass 2 of the visual-qa SKILL.md defines the evaluation framework (what to check). This file provides the implementation details (what good looks like, what values to target). CC reads this file, then evaluates each screen against these standards relative to the project's current state.

---

## 1. Dark Theme Typography

Dark backgrounds cause **halation** — the iris opens wider, making light text appear optically heavier and edges bleed. Compensate with these adjustments:

### Weight Reduction
- Headings: **600** (not 700) on dark backgrounds
- Body: **400**, never below 300
- Light text appears heavier — always go one weight step lighter than you would on white

### Letter Spacing
Light text crowds together on dark backgrounds. Apply positive letter-spacing:

| Size | Spacing | Why |
|------|---------|-----|
| 14px body | +0.005em | Minimal opening for readability |
| 12-13px captions | +0.01em | Small text needs more breathing room |
| All-caps overlines | +0.05em | Standard for uppercase tracking |

### Line Height for Monospace
Monospace fonts have uniform character widths and large x-height — they need more vertical breathing room than proportional fonts:
- **1.6** for 14px mono body text (22.4px)
- On dark backgrounds specifically, add +0.1 if readability feels tight

### Font Purpose Separation
Modern practice separates data fonts from prose fonts:
- **Monospace** for: IDs, timestamps, codes, numbers, tabular figures, data labels
- **Proportional (sans)** for: names, descriptions, natural language, navigation labels, button text, headings
- Improves scan speed — the brain processes each category faster when the font signals the content type

### Text Color Hierarchy
Never use pure `#FFFFFF` on dark backgrounds — 18.4:1 contrast against `#111` is excessively harsh and causes eye strain. Use a tiered system:

| Role | Target contrast | Usage |
|------|----------------|-------|
| Primary | ~16:1 | Active content, data values, primary text |
| Secondary | ~7:1 (AAA) | Labels, headers, descriptions |
| Muted | ~4:1 | Large text only — timestamps, metadata |
| Disabled | ~2.8:1 | Decorative only, never functional text |

Example values for `#111113` base: Primary `#EDEDED`, Secondary `#A0A0A5`, Muted `#6B6B70`, Disabled `#555558`.

### Font Smoothing (Critical for Dark Themes)
Three CSS properties are non-negotiable on dark backgrounds:
```css
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
text-rendering: optimizeLegibility;
```
Without antialiased rendering, macOS renders light-on-dark text visibly bolder than intended.

---

## 2. Light Theme Typography

Light themes have the opposite problem — text can appear too thin, and low-contrast combinations are the #1 accessibility violation (83.6% of websites per WebAIM 2024).

### Weight Adjustment
- Body text: **400-450** weight minimum for comfortable reading
- Don't go below 300 for any functional text
- Gray text on white needs more weight than you think

### Contrast Discipline
- Body text: minimum 7:1 against background (aim for AAA, not just AA)
- Secondary text: minimum 4.5:1, never lighter than `#767676` on white
- Placeholder text: at least 3:1 against input background

---

## 3. Surface & Elevation Systems

### Dark Theme: Color Stepping (Not Shadows)
Shadows are invisible against dark backgrounds. Modern dark UIs (Linear, Vercel, shadcn/ui) use **surface color stepping** — higher elevation = lighter surface.

**6-level system (each step ~2% lightness increase):**

| Level | Name | Use case |
|-------|------|----------|
| -1 | Sunken | Recessed wells, kanban board backgrounds |
| 0 | Base | Page background |
| 1 | Surface | Cards, sidebar, panels |
| 2 | Elevated | Hover states, dropdown menus |
| 3 | Raised | Modals, floating panels |
| 4 | Overlay | Tooltips, popovers, command palette |

Example for `#111113` base: `#0A0A0C` → `#111113` → `#161618` → `#1C1C1F` → `#232326` → `#2A2A2D`

### Border-First Depth (Dark Themes)
Borders replace shadows as the primary depth cue:
- Subtle: `rgba(255, 255, 255, 0.06)` — dividers, subtle edges
- Prominent: `rgba(255, 255, 255, 0.10)` — card borders, container edges
- Reserve solid borders for card edges only
- Reserve shadows exclusively for floating elements: `0 8px 30px rgba(0, 0, 0, 0.5)`

### Subtle Dimensionality
- Card top gradient: `linear-gradient(180deg, rgba(255,255,255,0.02) 0%, transparent 100%)` — adds depth without distraction
- Active/selected glow: `box-shadow: 0 0 0 1px rgba(accent, 0.3), 0 0 15px rgba(accent, 0.1)`
- Glassmorphism: use sparingly — increases render cost and reduces legibility. Only on non-critical decorative elements.

### Light Theme Elevation
Light themes can use shadows effectively:
- Cards: `0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.06)`
- Floating: `0 10px 25px rgba(0,0,0,0.1), 0 6px 10px rgba(0,0,0,0.08)`
- Still use surface color stepping for visual hierarchy (white → off-white → light gray)

---

## 4. Information Hierarchy & Data Density

### Inverted Pyramid Layout
Critical information first, details on demand:
1. **KPIs / summary** at top — answer the primary question in 5 seconds
2. **Trends / patterns** in the middle — what's changing?
3. **Detailed drill-downs** at bottom — full data tables, logs

### Progressive Disclosure
Don't dump everything at once:
- Primary actions visible, secondary in menus/overflow
- Details expand on interaction (accordion, drawer, modal)
- New users see less, power users can reveal more

### Density Controls
Offer 3 tiers (Gmail pattern):

| Tier | Row height | When |
|------|-----------|------|
| Compact | 32-36px | Power users, large datasets |
| Default | 40-44px | Standard use |
| Comfortable | 48-52px | Casual browsing, accessibility |

### Data Table Best Practices
- Horizontal dividers only (`1px solid rgba(color, 0.08)`), no vertical lines, no heavy borders
- Left-align text columns, right-align numeric columns
- Sticky headers and first column for large datasets
- Sortable columns with clear sort indicator
- Selected rows: accent tint at ~10% opacity
- Human-friendly date formats ("12 Jun 2025" not "2025-06-12"), relative dates for recent items

---

## 5. Interaction Quality

### State Coverage
Every interactive element needs all four states defined:
- **Default** — resting appearance
- **Hover** — mouse over (desktop) — subtle background shift or border change
- **Active/Pressed** — during click/tap — slight scale or color change
- **Disabled** — unavailable — reduced opacity (0.5) or muted colors, `cursor: not-allowed`

Plus for form elements:
- **Focus** — keyboard navigation — visible focus ring (2px, 3:1 contrast minimum)
- **Error** — validation failure — border color + message
- **Success** — validation pass — subtle confirmation

### Motion Timing Curves

| Category | Duration | Easing | Use |
|----------|----------|--------|-----|
| Fast | 50-100ms | `cubic-bezier(0.4, 0, 0.2, 1)` | Button press, active states, color changes |
| Normal | 150-200ms | `cubic-bezier(0.4, 0, 0.2, 1)` | Hover transitions, fade in/out |
| Slow | 250-350ms | `cubic-bezier(0, 0, 0.2, 1)` | Layout shifts, modals, page transitions, accordion expand |

### Reduced Motion
Wrap all motion in a preference check:
```css
@media (prefers-reduced-motion: no-preference) {
  /* animations go here */
}
```
Fallbacks: opacity fades instead of slide/scale, static pulse instead of shimmer, instant positioning instead of animated drag-and-drop.

### High Contrast Mode
Support `prefers-contrast: more`:
- Increase border widths from 1px to 2px
- Remove gradients
- Boost focus indicators
- Increase text contrast to AAA levels

---

## 6. Loading & Transition Patterns

### Skeleton Screens (Preferred Over Spinners)
- Shape matches final content layout exactly (prevents CLS)
- Show after **300ms delay** (prevent flash on fast loads)
- Subtle shimmer animation: 1.5s infinite linear
- Dark theme skeleton colors: bone `#374151`, shimmer `#4B5563`
- Light theme: bone `#E5E7EB`, shimmer `#F3F4F6`

### Optimistic Updates
- Mutations apply instantly to UI, revert on server failure
- Show subtle "saving" indicator (not blocking)
- Error toast with undo option on failure

### View Transitions
- Native View Transitions API for cross-view animation
- Fade as default, slide for drill-down/back navigation
- Duration: 200-300ms maximum

### Content Loading Priority
- Above-fold content renders first
- Below-fold lazy-loaded with intersection observer
- Images: placeholder → low-res → full-res (progressive)

---

## 7. Responsive & Adaptive Design

### Container Queries (Modern Standard)
Components should adapt to their parent container, not the viewport. Essential for dashboard layouts where the same card appears in sidebar vs. main content at different widths.

### Touch Target Minimums by Surface

| Surface | Minimum | Recommended | Notes |
|---------|---------|-------------|-------|
| Desktop (mouse) | 24×24px (WCAG) | 32×32px | Mouse precision allows smaller targets |
| Mobile | 44×44px (Apple HIG) | 48×48px (Material) | Finger precision, one-handed use |
| Tablet | 44×44px | 44×44px | Same as mobile |
| Kiosk / Industrial | 72×72px | 96×96px for primary | Gloved use, imprecise touch, viewing distance |

Between targets: minimum 8px spacing (WCAG 2.5.8 allows 24px total including target).

### Fluid Typography
Smooth cross-surface scaling with `clamp()`:
```css
--text-base: clamp(1rem, 0.9rem + 0.25vw, 1.25rem);
```
Adapts 16px-20px based on viewport. Override for extreme surfaces (kiosk, watch).

---

## 8. Accessibility Beyond Compliance

### Contrast Targets (Aim Above Minimums)

| Element | WCAG AA Minimum | Recommended Target |
|---------|----------------|-------------------|
| Normal text (<18pt) | 4.5:1 | 7:1+ |
| Large text (≥18pt) | 3:1 | 4.5:1+ |
| UI components | 3:1 | 4.5:1+ |
| Kiosk / Industrial | 4.5:1 | 7:1+ (AAA) |

### Shape Redundancy
Never rely on color alone to convey information (WCAG 1.4.1). Every status indicator should use at least two of:
- Color
- Shape/icon (circle, triangle, diamond, dash, square)
- Text label

Critical for the ~8% of male users with red-green color deficiency.

### Maximum Simultaneous Colors
In any single view, show maximum **6-7 distinct status/semantic colors**. Group rare statuses. Cognitive overload sets in above this threshold (IBM Carbon and Astro UXDS research).

### Keyboard Navigation
- Full app navigable via Tab, Enter, Space, Escape, Arrow keys
- Logical tab order matching visual flow
- Skip links for long navigation
- Focus trap in modals/dialogs
- Escape closes any overlay

### Screen Reader Support for Data
- `role="grid"` on interactive tables with `aria-rowcount`/`aria-colcount`
- `aria-rowindex`/`aria-colindex` on each cell (especially in virtualized grids)
- `aria-live="polite"` for real-time data updates
- `aria-sort` on sortable column headers

---

## 9. Toast & Notification Patterns

### Dark Theme Toast Colors

| Type | Border | Background |
|------|--------|------------|
| Success | `#4ADE80` | `#052E16` |
| Error | `#F87171` | `#450A0A` |
| Warning | `#FBBF24` | `#451A03` |
| Info | `#60A5FA` | `#172554` |

### Light Theme Toast Colors

| Type | Border | Background |
|------|--------|------------|
| Success | `#16A34A` | `#F0FDF4` |
| Error | `#DC2626` | `#FEF2F2` |
| Warning | `#D97706` | `#FFFBEB` |
| Info | `#2563EB` | `#EFF6FF` |

### Behavior
- Auto-dismiss after 5s (success/info), persist until dismissed (error/warning)
- Stack from bottom, max 3 visible
- Action button for undo/retry where applicable
- `role="alert"` for errors, `role="status"` for success/info

---

## 10. Modern CSS Patterns Worth Adopting

| Pattern | What it replaces | Impact |
|---------|-----------------|--------|
| Container queries | Media queries for component sizing | Cards adapt to parent, not viewport |
| `:has()` selector | JS class toggling for parent styling | Cleaner code, fewer re-renders |
| View Transitions API | JS animation libraries for page transitions | Native, smoother, less code |
| OKLCH color functions | Manual color palette generation | Perceptually uniform color manipulation |
| `clamp()` fluid typography | Fixed + breakpoint font sizes | Smooth scaling, fewer breakpoints |
| `prefers-reduced-motion` | Ignoring motion preferences | Required for accessibility |
| `prefers-contrast: more` | Ignoring contrast preferences | Better a11y with minimal effort |
| Scroll-driven animations | JS scroll event listeners | GPU-accelerated, performant |

---

## 11. Performance Design Targets

These directly affect perceived quality:

| Metric | Target | Why |
|--------|--------|-----|
| LCP (Largest Contentful Paint) | <2.5s | Primary content visible quickly |
| INP (Interaction to Next Paint) | <200ms | Every tap/click responds fast |
| CLS (Cumulative Layout Shift) | 0 | No content jumping after load |

Implementation patterns:
- Skeleton screens matching final layout dimensions (prevents CLS)
- Pre-render above-fold content
- Lazy-load below-fold
- Optimistic updates for mutations

---

## 12. Surface-Specific Guidance

### Large Format / Kiosk (40"+ displays)
- Body text: **28-32pt** at 55 PPI (1080p/40")
- Headlines: **48-60pt**
- Glance-distance headlines: **72pt+** for 10-foot readability
- Pagination over scrolling
- No hover states (touch-only)
- Audio feedback unreliable in noisy environments — rely on visual + haptic

### Mobile / PWA
- Bottom navigation for primary actions (thumb zone)
- Pull-to-refresh for lists
- Swipe gestures as shortcuts (not sole method)
- Safe area insets for notch/home indicator
- 44-48px touch targets minimum

### Desktop Web
- Keyboard shortcuts for power users
- Right-click context menus
- Multi-select with Shift/Cmd
- Hover tooltips for information density
- Sidebar navigation for 5+ top-level sections

---

*Last updated from 2025-2026 research: Linear theming, Vercel Geist system, Material Design 3, WCAG 2.2, Astro UXDS, IBM Carbon, industrial WMS case studies.*

### 6c. Fix Guardrails (`.claude/skills/fix-guardrails.md`)
Pre-change verification, scope limits, protected patterns, rollback lessons, Learned section.

---

## Track 7: Hooks

Three standard hooks enforced via `.claude/settings.json` with scripts in `.claude/hooks/`. These are deterministic — they fire every time, no token cost, no LLM judgment.

### Hook Configuration (`.claude/settings.json`)

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "if": "Bash(git push*) || Bash(git merge*) || Bash(git add .)",
        "hooks": [
          {
            "type": "command",
            "command": "$CLAUDE_PROJECT_DIR/.claude/hooks/git-guard.sh"
          }
        ]
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Write|Edit|MultiEdit",
        "if": "Write(**/*.{ts,tsx,js,jsx,css,json,md}) || Edit(**/*.{ts,tsx,js,jsx,css,json,md}) || MultiEdit(**/*.{ts,tsx,js,jsx,css,json,md})",
        "hooks": [
          {
            "type": "command",
            "command": "$CLAUDE_PROJECT_DIR/.claude/hooks/auto-format.sh"
          }
        ]
      }
    ],
    "FileChanged": [
      {
        "matcher": "schema.prisma|schema.ts|migrations|routes|.env|.env.local|.env.example|demo-sequence.json",
        "hooks": [
          {
            "type": "command",
            "command": "$CLAUDE_PROJECT_DIR/.claude/hooks/doc-drift-reminder.sh"
          }
        ]
      }
    ]
  }
}
```

### 7a. git-guard (`.claude/hooks/git-guard.sh`)

**Event:** `PreToolUse` on `Bash` commands, filtered by `if` to only fire on git push, git merge, and `git add .`

**Blocks:**
- Push to `main` or `demo` (any form: `git push origin main`, `git push` when on main/demo)
- Merge to `main` or `demo` (any form: `git merge` when on main/demo, merge PR to main/demo)
- Force push (`--force` or `--force-with-lease`)
- `git add .` (must use selective staging)

**Output:** Exit code 2 with stderr message explaining what was blocked and why. CC sees the message and adjusts.

### 7b. auto-format (`.claude/hooks/auto-format.sh`)

**Event:** `PostToolUse` on `Write|Edit|MultiEdit`, filtered by `if` to only fire on source files (not node_modules, not build output, not binary files).

**Action:** Runs the project's formatter (Prettier, Biome, Black, etc.) on the changed file. Uses `$CLAUDE_TOOL_INPUT_FILE_PATH` to target the specific file.

**Behavior:** Silent on success. If formatter not installed, exits 0 silently (non-blocking). CC doesn't need to know formatting happened.

### 7c. doc-drift-reminder (`.claude/hooks/doc-drift-reminder.sh`)

**Event:** `FileChanged` — fires only when watched files actually change on disk. The `matcher` field specifies which filenames to watch (pipe-separated basenames).

**Watches:** Schema files, route files, env files, migration files — whatever files in this project would cause doc drift if changed without updating docs. Route file changes also trigger a reminder to check `demo-sequence.json`.

**Action:** Exits 0 and prints a JSON object with `additionalContext` reminding CC which docs might need updating based on which file changed. Example: schema change → remind about ARCHITECTURE.md data model section.

**Why FileChanged instead of PostToolUse:** PostToolUse fires after every tool call, then the script has to check if the file was relevant. FileChanged fires only when the specific watched files change — no wasted hook executions. Cleaner, faster, less noise in long sessions.

### 7d. Hook Scripts Setup

All scripts in `.claude/hooks/` must be executable (`chmod +x`). Use `$CLAUDE_PROJECT_DIR` prefix for all paths — hooks must work regardless of CWD within the project.

CC generates the three scripts during health system setup, filling in project-specific values:
- **git-guard:** No project-specific values needed — same logic everywhere
- **auto-format:** Formatter command varies by project (Prettier, Biome, etc.)
- **doc-drift-reminder:** Watched files and corresponding doc reminders vary by project

### 7e. Adding Custom Hooks

Projects can add more hooks beyond the standard three. Common additions:
- **test-on-change:** `FileChanged` watching test files → run relevant test suite
- **type-check:** `PostToolUse` on `Write|Edit` for `.ts` files → run `tsc --noEmit`
- **deploy-guard:** `PreToolUse` on `Bash` with `if` matching deploy commands → block in dev, allow in CI

The `if` field uses permission rule syntax: `ToolName(glob-pattern)` with `||` for OR and `&&` for AND. This replaces the old pattern of writing bash scripts to filter tool inputs.

---

## Track 8: Health Skill File (WRITE LAST)

**New file:** `.claude/skills/project-health.md`

**HEALTH CHECK** — When user says "run health", "check health", "what's broken": Run health → investigate each item → present summary list (numbered, one line each, no tables) → per-item details (max 3 lines) → reply shortcuts → wait → fix → resolve → verify → clean.

**UI REVIEW** — When user says "run ui review", "review the screens", "visual audit": Run ui-review → read visual-qa SKILL.md → run Pass 1 (compliance flags against design system + reference) and Pass 2 (enhancement suggestions against standards) → present Pass 1 by severity then Pass 2 by impact (numbered, one line each) → wait → fix flags → re-capture → resolve → clean. Reference screen is source of truth. Suggestions require confirmation before building.

**FIX WORKFLOW** — Read skills before investigating. Verify scope against Protected Systems. Trace second-order effects. Test before marking done.

**DEPLOY & ROLLBACK** — Auto-deploy: merge PR → done. Manual: merge → deploy → monitor. New errors → platform rollback first, git revert fallback.

**LEARNING** — Read before investigating, append after resolving.

---

## Health System Files Summary

### New Files
| File | Purpose |
|------|---------|
| `[lib]/softFailure.[ext]` | Soft-failure reporter |
| `scripts/visual-verify.[ext]` | Screenshot utility |
| `scripts/visual-compare.[ext]` | Before/after comparison |
| `[components]/DevFeedbackButton.[ext]` | Floating feedback FAB |
| `[api]/health.[ext]` | Feedback CRUD endpoint |
| `scripts/health.[ext]` | Unified health CLI |
| `[admin]/health/page.[ext]` | Health admin (feedback + Sentry tabs) |
| `scripts/ui-review.[ext]` | Route crawler + screenshot CLI |
| `[api]/ui-review.[ext]` | UI review CRUD endpoint |
| `[admin]/ui-review/page.[ext]` | Visual review admin |
| `.claude/skills/project-health.md` | Health + UI review workflow |
| `.claude/skills/error-triage.md` | Error diagnosis |
| `.claude/skills/visual-qa/SKILL.md` | Two-pass frontend audit (compliance + enhancement) |
| `.claude/skills/visual-qa/references/enhancement-standards.md` | Universal Pass 2 design best practices |
| `.claude/skills/fix-guardrails.md` | Safe fix rules |
| `.claude/hooks/git-guard.sh` | Blocks push/merge to main, force push, git add . |
| `.claude/hooks/auto-format.sh` | Runs formatter on changed source files |
| `.claude/hooks/doc-drift-reminder.sh` | Reminds CC to update docs when schema/routes/env change |

### Environment Variables
| Variable | Where |
|----------|-------|
| `SENTRY_DSN` | Server + client |
| `SENTRY_ORG` | Build + runtime |
| `SENTRY_PROJECT` | Build + runtime |
| `SENTRY_AUTH_TOKEN` | Build + runtime |

---
---

# Part 4: Ops Pipeline (Optional — Telegram Layer)

> **Requires the health system first.** This adds remote management via Telegram. Without it, the health system still works — you just trigger checks yourself.

## What It Adds

- **Build Mode** — CC reports done/waiting/deviation/blocked to Telegram. Away Mode for when you step out.
- **Dispatch Mode** — Multiple tasks fan out to Agent Teams. Emoji identifiers. Plan verification before relay.
- **Heal Mode** — Sentry alerts flow into Telegram. CC investigates automatically.
- **Review Mode** — UI review results reported to Telegram.
- **Maintain Mode** — Renovate PR summaries.

## Skill Files

### Ops Pipeline Skill (`.claude/skills/ops-pipeline.md`)

BUILD MODE, DISPATCH MODE, PLAN VERIFICATION, HEAL MODE, REVIEW MODE, MAINTAIN MODE, LEARNING, GLOBAL RULES (no auto-fix without approval, no code in Telegram, flag protected systems, never skip tests, input resolution from any surface).

### Plan Verification Skill (`.claude/skills/plan-verification.md`)

Before relaying any teammate plan: scope check, protected systems, second-order effects, test plan, design system, elegance. Reject failed plans.

## Renovate Integration (Optional)

Skip if no `renovate.json` / `.renovaterc`. CC manages PRs via `gh pr list --author renovate`.

## Setup Walkthrough

CC writes the skill files, then walks the founder through:

1. **Enable Agent Teams** — Add to `~/.claude/settings.json`
2. **Create Telegram Bot** — @BotFather → `/newbot` → copy token → create ops group
3. **Configure CC Channels** — Install plugin at project scope, configure with bot token
4. **Pair** — DM bot → code → `/telegram:access pair` → allowlist policy → add group
5. **Make Channels Default** — Shell alias
6. **Persistent Session** — tmux or always-on machine. Enable Remote Control.
7. **CC Permission Rules** — Allow read/write/test/git/screenshots/health/ui-review/gh. Deny production build/migration deploy/rm -rf/force push/push to main or demo/merge to main or demo.
8. **Sentry → Telegram Alert Rules** — CC generates Sentry API curl commands
9. **Test** — Verify pairing, heal mode, build mode, screenshot report, full fix cycle

## Ops Pipeline Files

| File | Purpose |
|------|---------|
| `.claude/skills/ops-pipeline.md` | Build/Dispatch/Heal/Review/Maintain/Away modes |
| `.claude/skills/plan-verification.md` | Teammate plan verification |

---
---

# Part 5: Demo Navigator (Optional)

> **Requires screens and features to exist.** This adds a live interactive presentation mode to the app — like PowerPoint, but running the real app with real data. Define a route sequence, run `npm run demo`, and a floating pill guides you screen by screen.

## What It Is

A presentation mode overlay that sits on top of the running app. You define the order of screens and a one-line reminder for each. During the demo, a small pill shows you what to talk about and a Next button auto-navigates to the next screen. The audience sees a live, fully functional app. You never fumble the order or forget a feature.

**This is not a slideshow.** The app is real. Buttons work. Data is live. If someone asks "can it do X?" you can try it right there.

## How It Works

### Demo Branch & Deployment

Add a `demo` branch alongside `main` and `dev`:

- **`main`** → production
- **`dev`** → preview/staging
- **`demo`** → demo URL (e.g., `demo.yourapp.com` or Vercel branch URL)

In the hosting platform's environment settings for the `demo` branch, set `DEMO_MODE=true` and point at a dedicated demo database (a Supabase/Neon branch or a dedicated free-tier instance). The demo database gets seeded with good-looking Faker data.

The demo branch stays frozen on whatever version was last pushed. Update it by cherry-picking from `dev` or merging `dev` → `demo` when the app is in a good state for demoing. CC never pushes to `demo` directly — the founder controls when the demo version updates.

### Demo Sequence File (`demo-sequence.json`)

A simple JSON file defining the route order and presenter notes:

```json
{
  "title": "Shift Board — Investor Demo",
  "pin": "1234",
  "steps": [
    { "route": "/", "note": "Dashboard — weekly overview at a glance" },
    { "route": "/schedule", "note": "Empty schedule — show the pain" },
    { "route": "/schedule", "action": "click #auto-schedule-btn", "note": "One tap — auto-fills the whole week" },
    { "route": "/schedule/week", "note": "Weekly view, drag-to-swap any shift" },
    { "route": "/employees", "note": "103 employees, availability badges" },
    { "route": "/employees/maria-santos", "note": "Individual profile, shift preferences" },
    { "route": "/kiosk", "note": "Kiosk mode — clock in/out" },
    { "route": "/settings", "note": "Settings — roles, rules, constraints" }
  ],
  "unplaced": []
}
```

**Fields:**

- **`title`** — shown on the start card before the demo begins
- **`pin`** — required to access the reset button (prevents audience from accidentally wiping demo data)
- **`steps`** — ordered array of screens to present
  - `route` — the URL path to navigate to
  - `note` — your private reminder of what to talk about (the audience sees this too, but it's shorthand — they'll be watching you, not reading the pill)
  - `action` (optional) — a DOM action to execute on arrival (e.g., click a button to trigger a feature). Format: `click [selector]`, `scroll [selector] [distance]`, `type [selector] [text]`. Most steps don't need this — it's for moments where you want the app to do something dramatic while you narrate.
- **`unplaced`** — routes CC has added from new features that haven't been ordered into the sequence yet (see Maintenance below)

### The Navigator Pill

A small floating component fixed to the bottom-right of the viewport:

- **Size:** ~280px wide, 48px tall. Semi-transparent dark background (`rgba(0,0,0,0.85)`), rounded corners, subtle border.
- **Contents:** Step counter (`3/8`), the note text (truncated if long, full text on hover/tap), Back (←) and Next (→) buttons.
- **Keyboard support:** Left/right arrow keys, space bar for Next.
- **Behavior:** Tapping Next calls `router.push()` to navigate to the next step's route. If the step has an `action`, it executes after navigation settles (500ms delay). Back goes to the previous step.
- **Collapse:** The pill collapses to a small circle showing just the step counter when the user is interacting with the app (click/tap anywhere outside the pill). Expands on hover/tap on the pill. This keeps it out of the way during freeform exploration.
- **Off-script navigation:** If the user navigates manually (someone asks to see a specific screen), the pill stays put at the current step. Tapping Next resumes the sequence from where it left off.

### Start Card

Before step 1, the app shows a full-screen start card:

- Project title (from `demo-sequence.json`)
- One-line description (from PRODUCT.md or hardcoded)
- Estimated time (calculated from step count × ~15 seconds, rounded to nearest minute)
- "Start Demo" button

Sets expectations for the audience. Tapping Start navigates to step 1.

### Reset Button

Inside the pill's gear menu (or long-press on the pill):

- Enter pin → "Reset Demo Data" button
- Re-runs the seed script via an API endpoint (`/api/demo/reset`)
- Shows a brief loading state, then navigates back to the start card
- The API endpoint is only available when `DEMO_MODE=true`

### Demo Data Seeding

CC writes a seed script using **Faker.js with a fixed seed** (`faker.seed(42)`) so data is reproducible across resets. The seed script:

- Clears all existing data in the demo database
- Populates realistic user names, avatars, emails
- Fills lists and grids with enough data to look alive (minimum counts per the Visual Production Spec if it exists)
- Creates data that tells a story — the demo should show a state that makes the product look compelling
- Seeds bilingual data if the app supports i18n

**Seed script location:** `scripts/demo-seed.[ext]`

**Reset API endpoint:** `[api]/demo/reset.[ext]` — protected behind `DEMO_MODE=true` env check + pin verification. Calls the seed script programmatically. Returns success/failure.

### Environment Gating

The navigator pill, start card, reset endpoint, and all demo infrastructure only load when `DEMO_MODE=true` is set. In production and dev builds, the code is tree-shaken out completely. No demo artifacts leak to users.

## Sequence Maintenance

### CC Auto-Appends New Routes

When CC builds a feature that adds a navigable route, it appends the route to the `unplaced` array in `demo-sequence.json`:

```json
"unplaced": [
  { "route": "/reports", "note": "New — reporting dashboard", "added": "2026-03-28" }
]
```

CC does NOT place routes into the `steps` array — that's a creative decision about demo flow. CC just ensures new routes don't get forgotten.

### Ordering Unplaced Routes

Two paths:

**In Claude.ai:** The founder says "update the demo sequence." Claude.ai reads the current file, sees unplaced routes, and proposes where they fit in the flow. Iterate, lock, save.

**In CC:** The founder tells CC directly: "slot /reports after /employees in the demo sequence." CC moves it from `unplaced` to `steps` at the specified position.

### Doc-Drift Hook Integration

The doc-drift-reminder hook watches route files. When routes change, CC gets reminded to check `demo-sequence.json` alongside the other docs. This is automatic — no additional hook needed.

### Auto-Update Trigger

Added to CLAUDE.md's Auto-Update Triggers table:

| Code Change | Doc to Update | What to Change |
|-------------|---------------|----------------|
| Add/remove a navigable route | `demo-sequence.json` | Append to `unplaced` (new) or remove from `steps` (deleted) |

## Phase 9: Setup

### 9a. Demo Branch

1. Create `demo` branch from current `dev`
2. Configure hosting platform: `demo` branch → demo URL, set `DEMO_MODE=true`
3. Set up dedicated demo database (branch or free-tier instance)
4. Add demo database connection string to `demo` branch env vars

### 9b. Demo Seed Script

CC writes `scripts/demo-seed.[ext]`:
- Faker.js with fixed seed
- Clears and repopulates all core entities
- Makes the app look compelling and realistic
- Respects i18n if applicable

### 9c. Reset API Endpoint

CC creates `[api]/demo/reset.[ext]`:
- Gated behind `DEMO_MODE=true` + pin from `demo-sequence.json` (or env var)
- Calls seed script
- Returns JSON status

### 9d. Navigator Component

CC creates the navigator pill component:
- Reads `demo-sequence.json`
- Manages step state
- Router integration for auto-navigation
- Keyboard support (arrow keys, space)
- Collapse/expand behavior
- Start card before step 1
- Reset button behind pin in gear menu
- Only renders when `DEMO_MODE=true`

Mounts at app root level (same pattern as dev feedback button).

### 9e. Sequence File

Claude.ai authors the initial `demo-sequence.json` during or after the screen design phase. The route order follows the natural product story — not the navigation hierarchy, but the narrative flow that makes the product most compelling.

### 9f. Git Hygiene Update

Update `git-guard` hook to also block push to `demo` branch. CC never pushes to `demo` — the founder cherry-picks or merges when ready.

Update CLAUDE.md branching model to document the three-branch setup.

## Demo Navigator Files

| File | Purpose |
|------|---------|
| `demo-sequence.json` | Ordered route sequence with presenter notes |
| `scripts/demo-seed.[ext]` | Faker.js demo data seeder (shared with video pipeline if both used) |
| `[api]/demo/reset.[ext]` | Pin-protected reset endpoint (demo env only) |
| `[components]/DemoNavigator.[ext]` | Navigator pill + start card + reset UI |

## When to Use This

- Investor meetings (pull up the URL on any device)
- Stakeholder walkthroughs
- Sales demos
- Conference booth / kiosk
- Any time you need to show the product and want to nail the flow without memorizing it

The founder can say "set up demo mode" at any point after screens are built and core features work.

---
---

# Part 6: Demo Video Pipeline (Optional)

> **Requires screens and features to exist.** This generates a polished product demo video. The script is written in Claude.ai, the recording and composition happen in CC via Playwright and Remotion.

## What It Produces

A production-grade product demo video: screen recordings of the app in action, wrapped in device mockups, interleaved with text cards, spring animations, and background music. Rendered via Remotion as MP4 in multiple aspect ratios (16:9 web, 9:16 shorts, 1:1 social).

## How The Split Works

| Surface | Responsibility |
|---------|---------------|
| **Claude.ai** | Write the demo script (narrative arc, scene structure, text overlays, timing). Output: `demo-script.json` |
| **CC** | Seed demo data, record screen interactions via Playwright, compose via Remotion, render final video |

The script is the creative decision layer — what story to tell, what to show, what text to overlay. CC is the execution layer — recording, composing, rendering.

## Phase 10a: Write the Demo Script (Claude.ai)

When the founder says "make a demo video," "create a product video," or similar — this workflow starts here in Claude.ai.

**Inputs:** Read PRODUCT.md, FEATURES.md, DESIGN-SYSTEM.md. Understand the core loops, user personas, and what makes the product compelling.

**Narrative arc:** Every demo follows a 6-segment structure:

| Segment | Duration | Purpose |
|---------|----------|---------|
| **Hook** | 3–8s | Contrarian statement or potent question. Grab attention. |
| **Problem** | 5–15s | Real-world pain the user feels. Cost of inaction. |
| **Turning point** | 3–5s | Introduce the product as the solution. |
| **Feature showcase** | 30–60s | 2–4 key features demonstrated in action. This is the core. |
| **Resolution** | 5–10s | Show the "after" state. Metrics, outcomes, calm. |
| **CTA** | 3–8s | Product name, tagline, next step. |

Scale durations to target length. 60s video = tighter segments. 120s = more breathing room in the showcase.

**Text display timing:** `display_seconds = 3 + (word_count × 0.6)`. A 6-word card ("One click. The entire week scheduled.") needs ~6.6 seconds. Round to nearest half-second.

**Scene types:**

- **text_card** — Full-screen text on dark background. Accent color on key words. Spring scale-in animation.
- **screen_demo** — Screen recording of the app, wrapped in device mockup. Includes interaction description for CC to follow.
- **split** — Text on one side, screen recording on the other. For narrating while showing.

**Output format:** `demo-script.json` — a structured JSON file that CC and Remotion consume directly.

```json
{
  "meta": {
    "project": "Project Name",
    "target_duration_seconds": 90,
    "fps": 30,
    "resolution": { "width": 1920, "height": 1080 },
    "aspect_ratios": ["16:9"],
    "style": {
      "background": "#111113",
      "text_primary": "#fafafa",
      "text_secondary": "#a1a1aa",
      "accent": "#22c55e",
      "font_headline": "Geist Mono, monospace",
      "font_body": "Geist Sans, system-ui, sans-serif"
    }
  },
  "scenes": [
    {
      "id": "hook",
      "type": "text_card",
      "segment": "hook",
      "duration_seconds": 5,
      "headline": "Scheduling 103 employees used to take {hours}",
      "subtitle": null,
      "accent_words": ["hours"],
      "animation": "spring_scale",
      "transition": "fade"
    },
    {
      "id": "auto-schedule-demo",
      "type": "screen_demo",
      "segment": "feature_showcase",
      "duration_seconds": 15,
      "route": "/schedule",
      "interactions": [
        { "action": "click", "target": "#auto-schedule-btn", "wait_after_ms": 1000 },
        { "action": "click", "target": "#confirm-btn", "wait_after_ms": 3000 },
        { "action": "scroll", "target": ".schedule-grid", "direction": "down", "distance": 400 }
      ],
      "playback_rate": 1.5,
      "mockup": "browser",
      "mockup_animation": "slide_up",
      "annotation": "Watch the grid fill in — every slot assigned by seniority"
    }
  ],
  "audio": {
    "background_music": true,
    "music_volume": 0.15,
    "duck_during_text": true,
    "duck_volume": 0.06
  }
}
```

**Style tokens** pull from DESIGN-SYSTEM.md. The `accent_words` array marks which words in headlines render in the accent color. `interactions` are specific enough that CC can replay them with Playwright without ambiguity.

**Iterate the script here.** The founder reviews scenes, adjusts pacing, rewrites headlines, reorders features. Lock the script before handing to CC.

Save the locked script as `demo-script.json` to disk.

## Phase 10b: Demo Data Seeding (CC)

Before recording, the app needs to look good — not empty, not fake-looking.

CC writes a seed script using **Faker.js with a fixed seed** (`faker.seed(42)`) so data is reproducible across recording runs. The seed script populates:

- Realistic user names, avatars, emails
- Enough data to fill lists and grids (minimum counts per the Visual Production Spec if it exists)
- Data that tells a story — the demo should show a state that makes the product look compelling
- Bilingual data if the app supports it

**Seed script location:** `scripts/demo-seed.[ext]`
**Run before every recording session.** Reset to clean state, then seed.

**Shared with Demo Navigator.** If the project has a Demo Navigator set up, this is the same seed script. One script, two consumers — the navigator's reset button calls it via API, the video pipeline calls it directly before recording.

## Phase 10c: Screen Recording (CC)

CC reads `demo-script.json` and records each `screen_demo` scene as a separate video clip.

### Recording Setup

```typescript
const context = await browser.newContext({
  viewport: { width: 1920, height: 1080 },
  recordVideo: { dir: 'recordings/', size: { width: 1920, height: 1080 } },
});
```

**Critical:** Match `recordVideo.size` exactly to viewport. Playwright's default scales down.

### Human-Like Interactions

Install `ghost-cursor-playwright` for natural mouse movement — Bezier curves, Fitts's Law deceleration, random click positions within elements (not dead center).

```typescript
import { createCursor } from 'ghost-cursor-playwright';
const cursor = createCursor(page, { x: 960, y: 540 }, false, { visible: true });
```

**Cursor visibility:** Headless Playwright doesn't render a cursor. `ghost-cursor-playwright` with `visible: true` injects a CSS overlay that follows mouse events. This is required — without it, the recording has no cursor.

**Interaction pacing:**
- Wait 200–500ms before each click (human hesitation)
- Wait 800–1500ms after navigation (let page settle)
- Scroll with decreasing deltaY (200 → 150 → 50) for momentum deceleration
- Type with 50–200ms keystroke delay, occasional 300ms pauses

### Post-Processing

Playwright outputs WebM at a hardcoded 1Mbps. **Always re-encode:**

```bash
ffmpeg -i recording.webm -c:v libx264 -crf 18 -preset slow -movflags faststart -r 30 scene.mp4
```

Save processed clips to `demo-video/clips/[scene_id].mp4`.

### Scene Manifest

After recording, CC generates `demo-video/clips/manifest.json` mapping scene IDs to clip files with actual durations.

## Phase 10d: Remotion Composition (CC)

CC scaffolds a Remotion project (or uses an existing one) and builds the composition from `demo-script.json`.

### Project Structure

```
demo-video/
  remotion/
    src/
      Root.tsx                    ← Registers compositions
      Master.tsx                  ← Main composition, reads demo-script.json
      components/
        TextCard.tsx              ← Text overlay scenes
        ScreenDemo.tsx            ← Device mockup + video playback
        BrowserMockup.tsx         ← Browser chrome frame
        PhoneMockup.tsx           ← Phone frame (if mobile)
        AccentText.tsx            ← Headline with accent-colored words
    public/
      clips/                     ← Screen recording MP4s
      music/                     ← Background audio
      demo-script.json           ← The locked script
    remotion.config.ts
```

### JSON-Driven Rendering

The composition reads `demo-script.json` via `inputProps`. `calculateMetadata()` computes total duration from scene durations. Each scene maps to a `<Sequence>` with the correct frame offset.

```tsx
const metadata: CalculateMetadataFunction<ScriptProps> = async ({ props }) => ({
  durationInFrames: Math.ceil(
    props.scenes.reduce((acc, s) => acc + s.duration_seconds, 0) * props.meta.fps
  ),
  fps: props.meta.fps,
  width: props.meta.resolution.width,
  height: props.meta.resolution.height,
});
```

### Device Mockup Component

Dark rounded rectangle with simulated browser chrome (three dots, URL bar). Screen recording plays inside. CSS `perspective` and `rotateX`/`rotateY` for subtle 3D tilt. Spring-animated entrance (scale 0→0.85, translateY 40→0).

### Text Card Component

Reusable. Takes `headline` string, parses `{accent}` markers to render those words in the accent color. Spring scale-in (0.9→1.0) + opacity (0→1). Word-by-word stagger at 5 frames per word for premium feel.

### Spring Configurations

| Use | Config | Result |
|-----|--------|--------|
| Text card entrance | `{ damping: 20, stiffness: 100, mass: 1 }` | Smooth, no bounce |
| Mockup float-in | `{ damping: 15, stiffness: 120, mass: 0.8 }` | Subtle life |
| Feature callout | `{ damping: 12, stiffness: 200, mass: 0.5 }` | Snappy |
| Any "no bounce" | Add `overshootClamping: true` | Dead stop |

### Audio

Background music via Remotion's `<Audio>` component. Volume at 0.15 baseline. Duck to 0.06 during text cards using a volume callback function:

```tsx
<Audio src={staticFile('music/ambient.mp3')} volume={(f) => {
  const isTextCard = /* check if current frame is in a text_card scene */;
  return isTextCard ? 0.06 : 0.15;
}} />
```

### Multi-Format Export

Register multiple compositions with different aspect ratios:

| Format | Resolution | Use |
|--------|-----------|-----|
| `Master` | 1920×1080 (16:9) | Website, YouTube |
| `Vertical` | 1080×1920 (9:16) | TikTok, Reels, Shorts |
| `Square` | 1080×1080 (1:1) | LinkedIn, Instagram feed |

Vertical and square compositions reframe the content — mockups scale differently, text repositions, scenes may reorder for mobile-first attention patterns.

### Render

```bash
# Preview
npm run dev  # Opens Remotion Studio

# Render
npx remotion render Master out/demo-16x9.mp4
npx remotion render Vertical out/demo-9x16.mp4
npx remotion render Square out/demo-1x1.mp4
```

Local rendering uses hardware acceleration on macOS (VideoToolbox). For faster renders or CI, use Remotion Lambda (parallel across up to 200 functions).

## Phase 10e: Review and Iterate

CC renders a draft. The founder watches it. Two paths:

**Minor timing/text fixes** — Edit `demo-script.json` directly (adjust durations, reword headlines, reorder scenes). CC re-renders. No re-recording needed unless interactions change.

**Re-record a scene** — If an interaction looks wrong or the data doesn't look right, CC re-records just that scene and re-renders.

**Major script changes** — Come back to Claude.ai, revise the script, re-export `demo-script.json`, hand back to CC.

## Demo Video Files

| File | Purpose |
|------|---------|
| `demo-script.json` | Locked scene script (from Claude.ai) |
| `scripts/demo-seed.[ext]` | Faker.js demo data seeder (shared with Demo Navigator if both used) |
| `scripts/demo-record.[ext]` | Playwright recording script |
| `demo-video/clips/` | Recorded + processed MP4 clips |
| `demo-video/clips/manifest.json` | Clip metadata (durations, scene mapping) |
| `demo-video/remotion/` | Remotion project |
| `demo-video/out/` | Rendered final videos |

## When to Use This

- Launch video for landing page or app store
- Social media clips for product marketing
- Async demos (send a video, not a link)
- Any time you need a polished, edited walkthrough with text cards and music

For live demos (investor meetings, stakeholder walkthroughs, conference booths), use the Demo Navigator instead — it's live, interactive, and always current.

The founder can say "make a demo video" at any point after screens are built and features work. The pipeline runs on whatever's currently deployed.

---
---

# Part 7: CLAUDE.md Template

> **CC's per-project operating manual.** Fill in [PLACEHOLDER] sections during Phase 6 doc generation. This is what CC reads every session. Everything below this line until Part 8 is template content — generate it per project.

## [PROJECT_NAME] — Claude Code Reference

[ONE_LINE_DESCRIPTION]

## Read These When Needed

| Doc | When | Purpose |
|-----|------|---------|
| `docs/PRODUCT.md` | Designing features, product decisions | What we're building, why, feature map with status |
| `docs/PLAYBOOK.md` | Session start, evaluating new work | Current focus, up next, process, definition of done |
| `docs/DESIGN-SYSTEM.md` | UI work | Visual rules, tokens, component patterns |
| `docs/FEATURES.md` | Building features that touch multiple systems | Feature connections, configurable values |
| `docs/ARCHITECTURE.md` | Understanding codebase structure | Full system map, data flows, tech debt |
| `docs/LAUNCH-CHECKLIST.md` | Preparing for launch | One-time pre-launch items |
<!-- [ADDITIONAL_DOCS] -->

## Skills

<!-- Health skills are standard. Add project-specific skills as CC encounters repeating patterns. -->

| Skill | When to Read | File |
|-------|-------------|------|
| Project Health | When user says "run health", "check health", or "what's broken" | `.claude/skills/project-health.md` |
| Error Triage | When diagnosing errors or bugs | `.claude/skills/error-triage.md` |
| Visual QA | Before/after UI verification, full-app visual audit, or design check | `.claude/skills/visual-qa/SKILL.md` |
| Fix Guardrails | Before applying any autonomous fix | `.claude/skills/fix-guardrails.md` |
<!-- [STARTER_SKILLS] -->
<!-- Ops Pipeline skills (added when Telegram ops pipeline is set up): -->
<!-- | Ops Pipeline | Before build, heal, maintain, or review operations | `.claude/skills/ops-pipeline.md` | -->
<!-- | Plan Verification | Before relaying teammate plans to Telegram | `.claude/skills/plan-verification.md` | -->

---

## Development Environment

<!-- [FILL_FROM_ARCHITECTURE] -->

**Stack:**
- Frontend: [FRAMEWORK]
- Backend: [FRAMEWORK]
- Database: [DATABASE]
- Hosting: [HOSTING]

**Commands:**
```bash
# Dev
[DEV_COMMAND]

# Test
[TEST_COMMAND]

# Type check
[TYPECHECK_COMMAND]

# Build
[BUILD_COMMAND]

# Project health (pulls user feedback + Sentry errors into one list)
[PACKAGE_RUNNER] health

# UI review (captures all screens, shows open flags for visual audit)
[PACKAGE_RUNNER] ui-review

# Demo mode (launches app with navigator pill — demo branch only)
# [PACKAGE_RUNNER] demo
```

**Production warning:** [DESCRIBE_PROD_DB_SITUATION]

### Project Health (`[PACKAGE_RUNNER] health`)

When user says "run health", "check health", or "what's broken":

1. Run `[PACKAGE_RUNNER] health` — show FULL untruncated output
2. For EACH open item, read relevant files, diagnose root cause, propose fix
3. Present summary list FIRST (one line per item, numbered, scannable in 3 seconds), then per-item details (max 3 lines each). No ASCII tables. User replies with numbers, not IDs.
4. End with reply shortcuts: "fix all", "fix 1", "fix 1 skip 2", "resolve 2", "skip all"
5. Wait for user go-ahead
6. On confirmation, implement fixes (fan out teams if multiple)
7. Resolve feedback items via CLI, Sentry items via API
8. Run health to verify zero remaining
9. Clean if requested

Do NOT just report what the health check says — investigate it.

### UI Review (`[PACKAGE_RUNNER] ui-review`)

When user says "run ui review", "review the screens", "visual audit", or similar:

1. Run `[PACKAGE_RUNNER] ui-review` — captures all screens, shows FULL untruncated output
2. Read visual-qa SKILL.md — check `reviewed_by` per screen, run Pass 1 (compliance) on all screens, run Pass 2 (enhancement) only on screens NOT marked `reviewed_by: claude-ai`
3. Load reference screen — this is the consistency benchmark
4. For EACH screen, compare against reference + DESIGN-SYSTEM.md (Pass 1) and enhancement-standards.md (Pass 2, if eligible)
5. Auto-generate flags (Pass 1) and suggestions (Pass 2)
6. Present findings: Pass 1 flags grouped by severity, then Pass 2 suggestions by impact. Numbered. Per-item details. No ASCII tables. Reply shortcuts.
7. Wait for user go-ahead
8. Implement fixes (fan out for unrelated screens, sequential for shared components)
9. Re-capture and verify
10. Resolve fixed items
11. Clean if requested

Reference screen is source of truth. Always pull values FROM the reference, never average.

### UI Review Export (`[PACKAGE_RUNNER] ui-review --export`)

When user says "export ui review", "export for claude.ai", or runs with `--export`:

1. Run `[PACKAGE_RUNNER] ui-review --export` — captures all screens, bundles export package
2. Report package location — user uploads to Claude.ai project for design-surface review
3. When user returns with fix instructions from Claude.ai, apply them directly
4. Mark affected screens as `reviewed_by: claude-ai` — subsequent autonomous reviews will skip Pass 2 on these screens until visual changes are detected

---

## Conventions

- **Naming:** [e.g., kebab-case files, PascalCase components, camelCase functions]
- **i18n:** [e.g., All user-facing text through t() function]
- **Imports:** [e.g., Absolute imports from @/lib, relative within same feature]

---

## Git Hygiene

### Branching Model

Three branches:

- **`main`** — Production. Deploys to production automatically. CC never pushes here. CC never merges here.
- **`dev`** — Working branch. CC does all work here. Preview/staging deployments trigger automatically from this branch.
- **`demo`** — Demo presentation environment. Deploys to the demo URL with `DEMO_MODE=true`. CC never pushes here. The founder cherry-picks or merges from `dev` when the app is in a good state for demoing.

Merging `dev` → `main` is done by the founder when ready to ship. This is the only deploy gate.

### Commit Rules

1. **Selective staging only.** Never `git add .`. Stage only files changed in the current task. If unrelated changes exist in the working tree (previous session, manual edits), leave them unstaged.
2. **One concern per commit.** If a task touches schema, API, and UI — that's at minimum three commits, not one.
3. **Conventional commit format:**
   - `feat: add dev feedback button` — new functionality
   - `fix: health CLI skipping Sentry when env vars missing` — bug fix
   - `docs: update PLAYBOOK after completing queue feature` — doc changes
   - `refactor: extract shared card component` — restructuring without behavior change
   - `chore: update dependencies` — maintenance
4. **Build check before every commit.** Run `[PACKAGE_RUNNER] build` (or the project's equivalent build command) before committing. If the build fails, fix it first. Do not commit code that breaks the build.
5. **Commit when a logical unit is complete.** Not after every file save, and not one giant commit at the end. A logical unit = a piece of work that leaves the app in a working state. If a feature has three parts and completing part one still leaves the app running, commit part one.
6. **Push after each commit.** Pushing to `dev` is safe — nothing goes to production. Push immediately so work is backed up remotely.

### What CC Never Does

- Push to `main` or `demo`
- Merge to `main` or `demo`
- Force push (`--force` or `--force-with-lease`)
- Commit unrelated files that happened to be in the working tree

---

## Hooks

Three deterministic hooks in `.claude/settings.json` with scripts in `.claude/hooks/`. These fire automatically — no token cost, no LLM judgment.

| Hook | Event | Trigger | What It Does |
|------|-------|---------|-------------|
| git-guard | `PreToolUse` + `if` | Git push/merge/force-push/`git add .` | Blocks prohibited git operations |
| auto-format | `PostToolUse` + `if` | Write/Edit/MultiEdit on source files | Runs formatter on changed file |
| doc-drift-reminder | `FileChanged` | Schema, routes, env files change on disk | Reminds CC which docs to update |

**git-guard** blocks push to main/demo, merge to main/demo, force push, and `git add .`. Exit code 2 with explanation.

**auto-format** runs the project's formatter silently. Non-blocking on failure (formatter not installed = skip).

**doc-drift-reminder** uses `FileChanged` event — only fires when watched files actually change, not after every tool call. Injects `additionalContext` telling CC which doc section to check.

**Adding hooks:** The `if` field uses permission rule syntax (`ToolName(glob-pattern)` with `||`/`&&`) to filter when hooks fire. Add project-specific hooks as needed — see `.claude/settings.json` for the current configuration.

---

## Key Patterns

**Subagent Strategy** — Use subagents to keep the main context window clean. One task per subagent.

<!-- [PROJECT_SPECIFIC_PATTERNS] -->

---

## Environment / Secrets

| Variable | Where | Required |
|----------|-------|----------|
<!-- [ENV_VARS] -->

---

## Hard Rules

1. **Demand Elegance** — For every non-trivial decision, surface the elegant option alongside the pragmatic one.
2. **Never leave docs knowingly stale** — Flag contradictions before implementing.
3. **CC never rewrites domain-expert values** — Copy exactly from CC-PROMPTs.
4. **Trace second-order effects before implementing**
5. **Test before marking done**
6. **Verify each track against the spec before moving on** — After completing a track, check that the output matches the CC-PROMPT spec (correct files, correct behavior, correct integration points). Fix deviations before starting the next track. Don't accumulate drift.
7. **Build must pass before every commit** — Run the build command before committing. Broken builds never get committed, even on `dev`.

<!-- [PROJECT_SPECIFIC_HARD_RULES] -->

---

## Learned Corrections

### Router / API
_(Empty)_

### UI / Components
_(Empty)_

### Database / Queries
_(Empty)_

### Business Logic
_(Empty)_

### Integration / Cross-System
_(Empty)_

### CC-PROMPT Fidelity
_(Empty)_

### Imports / Dependencies
_(Empty)_

<!-- [ADDITIONAL_CATEGORIES] -->

**Self-Growing Skills** — After completing any CC-PROMPT, review what was wrong or redone. If recurring (3+ times), append to the relevant skill's Learned section or create a new skill.

---

## Design Quick Reference

**Full spec:** `docs/DESIGN-SYSTEM.md`

### Philosophy
<!-- [2-3 visual rules] -->

---

## Doc Maintenance

### Auto-Update Triggers

| Code Change | Doc to Update | What to Change |
|-------------|---------------|----------------|
| Add/change/remove a feature | PRODUCT.md | Feature status |
| Complete a feature | PLAYBOOK.md | Move to Recently Completed |
| Change design tokens | DESIGN-SYSTEM.md | Update affected values |
| Change architecture or infra | ARCHITECTURE.md | Update affected section |
| Change feature connections | FEATURES.md | Dependency graph |
| Add/change env vars | ARCHITECTURE.md | Environment section |
| Add a new dependency | ARCHITECTURE.md | Tech stack table |
| Add a new skill | This file (CLAUDE.md) | Skills table |
| Add/change a hook | `.claude/settings.json` | Hooks config |
| Add/remove a navigable route | `demo-sequence.json` | Append to `unplaced` (new) or remove from `steps` (deleted) |
<!-- [PROJECT_SPECIFIC_TRIGGERS] -->

### Flag-Before-Diverge Rule

Flag contradictions before implementing. If confirmed, update code AND doc in same session.

### Session-End Check

Feature behavior changed? → check docs. Feature added/removed? → PRODUCT + FEATURES + demo-sequence.json (append to unplaced). Completed? → PLAYBOOK. Data model? → ARCHITECTURE. Docs updated? → remind user to sync to Claude.ai. Env vars? → ARCHITECTURE. New dependency? → ARCHITECTURE. New skill? → CLAUDE.md skills table. New hook? → `.claude/settings.json`. Route added/removed? → demo-sequence.json. PLAYBOOK stale? → update. Docs disagree? → reconcile.

### Mirror List

| Doc | Mirrored to Claude.ai |
|-----|-----------------------|
<!-- [FILL_FROM_DOCS] -->

### Periodic Review (Monthly)

Run doc health check. Flag anything stale across PLAYBOOK, FEATURES, PRODUCT, ARCHITECTURE, Project Instructions.

---
---

# Part 8: Rules

## Rules for the Bootstrap Project

- **Start the conversation.** When the founder opens this project, introduce yourself briefly and jump into Phase 1.
- **Be direct.** No preamble, no filler. Match a fast-paced founder's energy.
- **Propose, don't ask** (except Phase 1 and 5).
- **Generate visual previews** for the design system.
- **Save to disk as you go.** Write docs incrementally.
- **Don't over-document.** Scale to complexity.
- **If the founder disagrees, adapt.** Make your case once, then execute their decision.
- **The founder can skip anything.** Generate sensible defaults and move on.
