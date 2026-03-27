# Project Audit Checklist

> **Purpose:** Hand this to any existing project's CC session to diff the codebase against the current master reference. CC reads this file, checks each item against what's actually built, and reports what's implemented, what's missing, and what's outdated.
>
> **How to use:** Paste this prompt into CC:
> ```
> Read project-audit.md. For each section, check the codebase and report:
> ✅ Implemented — working as described
> ⚠️ Partial — exists but doesn't match current spec
> ❌ Missing — not implemented
> Then summarize: what's up to date, what needs upgrading, what's not set up yet.
> ```
>
> **Maintained alongside `new-project-master.md`.** When the master doc changes, this checklist must be updated in the same session.

---

## Sentry SDK Integration

- [ ] Client-side SDK initialized (DSN from env, environment tag from hosting platform env var, disabled in dev, PII stripped, perf sampling, navigation integration)
- [ ] Server-side SDK initialized (DSN from env, environment tag from hosting platform env var, perf sampling, PII stripped)
- [ ] Error handler: server-class errors only (500/timeout/429/412, NOT 401/400/403/404)
- [ ] Background job errors captured via centralized global handler
- [ ] Unhandled rejections caught globally
- [ ] Source maps / debug symbols enabled
- [ ] Serverless/edge functions: individual Sentry init + capture + flush (if applicable)

### Sentry Full Depth (for production apps)

- [ ] Release tracking (`release` and `dist` in Sentry.init)
- [ ] Performance profiling (`profilesSampleRate: 0.1`)
- [ ] Cron monitoring on all scheduled jobs

---

## Soft-Failure Instrumentation

- [ ] Soft-failure reporter utility with generic types + project-specific types
- [ ] Error boundaries report to Sentry (if frontend)
- [ ] 5-8 instrumentation points wired in
- [ ] Sentry alert rules configured (crash, soft failure batch, server spike, job failure, perf regression)

---

## Visual Verification

- [ ] Playwright installed and configured (web projects)
- [ ] Maestro installed and configured (native mobile / hybrid)
- [ ] `scripts/visual-verify` screenshot utility
- [ ] `scripts/visual-compare` before/after comparison
- [ ] Deploy targets mapped to base URLs

---

## Dev Feedback System

### Database
- [ ] `dev_feedback` table (id, screen, message, status, screenshot_url, timestamps)
- [ ] Indexed on `status` and `screen`

### Feedback Button
- [ ] Floating FAB component (40-48px, muted color, bottom-right)
- [ ] Renders at app root level globally
- [ ] Auto-detects current screen/route name
- [ ] Screenshot capture on submit → upload to storage → save
- [ ] Gated behind environment variable

### API Endpoints
- [ ] Create feedback
- [ ] List with filters
- [ ] Update status
- [ ] Bulk resolve
- [ ] Delete resolved + screenshot cleanup

### Admin Page
- [ ] Feedback tab with table, filters, actions
- [ ] Sentry tab pulling unresolved issues from API
- [ ] Combined view as default (both sources merged)

---

## Unified Health CLI

- [ ] `health` script registered in package config
- [ ] Queries DB for open feedback items (prefixed `fb-`)
- [ ] Queries Sentry API for unresolved issues (prefixed `sn-`), filtered to `environment=production` only
- [ ] Sorts by severity (Bug → Perf → UX → UI) then date
- [ ] Output: numbered list, one line per item, brackets for metadata (severity · file count · estimate), 📸 for screenshots
- [ ] Gracefully skips Sentry if env vars not set
- [ ] `--feedback` filter
- [ ] `--errors` filter
- [ ] `--resolve` for feedback items
- [ ] `--clean` deletes resolved + screenshots
- [ ] Old `feedback` command aliased to `health --feedback`

---

## UI Review System

### Database
- [ ] `ui_review_screens` table (id, screen, screenshot_url, capture_set, is_reference, reviewed_by, reviewed_at, created_at)
- [ ] `ui_review_flags` table (id, screen_id FK, severity, message, status, source, timestamps)
- [ ] Flags indexed on `status` + `severity`
- [ ] Screens indexed on `capture_set`
- [ ] `reviewed_by` values: `null` (unreviewed), `cc` (autonomous review), `claude-ai` (design-surface review)

### Route Crawler
- [ ] Discovers all routes programmatically (no hardcoded list)
- [ ] Handles auth states (logged-out, logged-in, multiple user types)
- [ ] Seeds dynamic routes with DB records
- [ ] Waits for network idle + spinners before capture
- [ ] Stores screenshots under `ui-review/[capture_set]/`

### API Endpoints
- [ ] List screens (latest set with flags)
- [ ] List capture sets
- [ ] Set reference screen
- [ ] Create flag (manual)
- [ ] Bulk create flags (auto)
- [ ] Update flag status
- [ ] Bulk resolve flags
- [ ] Delete resolved + old capture sets (keep latest 3)

### Admin Page
- [ ] Grid view: screenshot cards, flag count badges (color-coded), reference badge
- [ ] Detail view: full screenshot, flags panel, add flag form, set reference button, prev/next nav
- [ ] Comparison mode: two capture sets side-by-side, changed screens marked

### CLI (`ui-review`)
- [ ] Registered in package config
- [ ] Default: captures all screens + autonomous review + shows open flags
- [ ] Output: count headers per section (e.g. "Critical (6) · Consistency (12) · Polish (4)"), then Pass 1 flags numbered by severity, then Pass 2 suggestions by impact, one line per item with brackets (severity · file count · estimate)
- [ ] `--export` bundles review package for Claude.ai design-surface review (see Export Package below)
- [ ] `--resolve` for flag IDs
- [ ] `--reference` to set reference screen
- [ ] `--clean` deletes resolved flags + old capture sets

### Export Package (`--export`)
- [ ] Creates export directory: `ui-review/export/[capture_set]/`
- [ ] Includes all captured screenshots organized by screen name
- [ ] Generates `review-context.md` containing: design system tokens (colors, spacing, typography scale), screen-to-route map, reference screen markers, known state variants per screen (empty, loading, error)
- [ ] Generates `review-instructions.md` header with two-pass structure, severity levels, fix instruction format for CC
- [ ] Package is self-contained — Claude.ai needs no codebase access to do the review

### Review Hierarchy
- [ ] Autonomous review (`ui-review` default) marks screens as `reviewed_by: cc`
- [ ] Fix instructions from Claude.ai export review mark screens as `reviewed_by: claude-ai`
- [ ] Autonomous review skips enhancement suggestions on screens marked `reviewed_by: claude-ai`
- [ ] Autonomous review still flags objective breakage (layout overflow, missing elements, broken states) on all screens regardless of `reviewed_by`
- [ ] `reviewed_by` resets to `null` when a new capture set detects visual changes on that screen

---

## Self-Growing Skills

- [ ] `.claude/skills/project-health.md` — health check + UI review workflow
- [ ] `.claude/skills/error-triage.md` — error type → files lookup, diagnostic steps, Learned section
- [ ] `.claude/skills/visual-qa/SKILL.md` — two-pass frontend audit (Pass 1: compliance flags against design system, Pass 2: enhancement suggestions against state-of-the-art standards), respects review hierarchy (`claude-ai` reviewed screens skip Pass 2), Learned section
- [ ] `.claude/skills/visual-qa/references/enhancement-standards.md` — universal Pass 2 best practices (typography, elevation, data density, interaction quality, accessibility, motion, modern CSS)
- [ ] `.claude/skills/fix-guardrails.md` — pre-change verification, scope limits, Learned section

---

## Git & Deploy

- [ ] `dev` branch exists and is the default working branch for CC
- [ ] `main` branch is production — CC never pushes or merges to it
- [ ] Hosting platform (Vercel/etc.) configured: only `main` deploys to production
- [ ] Preview/staging deployments trigger from `dev` branch (or all non-main branches)
- [ ] CLAUDE.md contains Git Hygiene section with branching model, commit rules, and prohibitions
- [ ] CC uses selective staging (not `git add .`)
- [ ] CC uses conventional commit format (feat/fix/docs/refactor/chore)
- [ ] CC runs build check before every commit
- [ ] CC pushes after each commit to `dev`
- [ ] Hard Rules include "Build must pass before every commit"

---

## CLAUDE.md Configuration

- [ ] Skills table includes: Project Health, Error Triage, Visual QA, Fix Guardrails
- [ ] Commands block includes `health` and `ui-review`
- [ ] Project Health workflow section (run → investigate → summary list → details → reply shortcuts → fix → resolve → verify → clean)
- [ ] UI Review workflow section (capture → read visual-qa SKILL.md → Pass 1 compliance flags by severity → Pass 2 enhancement suggestions by impact → present → fix flags → re-capture → resolve → clean. Suggestions require confirmation before building. Export mode: `--export` → upload to Claude.ai project → design-surface review → fix instructions back to CC)
- [ ] Presentation format: numbered list, no ASCII tables, IDs in details only, brackets include file count, reply with numbers
- [ ] Doc Maintenance section (auto-update triggers, flag-before-diverge, session-end check, mirror list)
- [ ] Hard Rules include Demand Elegance, verify each track against spec before moving on, + project-specific rules

---

## Launch Checklist Items

- [ ] Dev feedback button gated behind environment check
- [ ] Button does not appear in production builds
- [ ] All health items resolved before launch (`health` shows zero)
- [ ] UI review admin page gated behind admin/dev check
- [ ] All UI review flags resolved before launch (`ui-review` shows zero)

---

## Ops Pipeline — Telegram Layer (Optional)

- [ ] `.claude/skills/ops-pipeline.md` — Build/Dispatch/Heal/Review/Maintain/Away modes
- [ ] `.claude/skills/plan-verification.md` — teammate plan verification checklist
- [ ] Telegram bot created and configured
- [ ] CC Channels installed at project scope
- [ ] Bot paired with allowlist policy
- [ ] Ops group added with `requireMention` false
- [ ] Channels alias set as default
- [ ] Agent Teams enabled in settings
- [ ] Sentry → Telegram alert rules configured
- [ ] CC permission rules set (allow read/write/test/git/screenshots/health/ui-review, deny prod build/migration/rm -rf/force push/push to main/merge to main)
- [ ] Remote Control enabled for all sessions

---

## Demo Video Pipeline (Optional)

### Script
- [ ] `demo-script.json` exists with locked scene structure
- [ ] Follows 6-segment narrative arc (hook, problem, turning point, feature showcase, resolution, CTA)
- [ ] Text card durations follow timing formula: `3 + (word_count × 0.6)` seconds
- [ ] Style tokens in script match DESIGN-SYSTEM.md
- [ ] Scene interactions are specific enough for Playwright replay (selectors, wait times, scroll distances)

### Demo Data
- [ ] `scripts/demo-seed.[ext]` exists
- [ ] Uses Faker.js with fixed seed for reproducible data
- [ ] Data looks compelling (not empty, not obviously fake)
- [ ] Bilingual data seeded if app supports i18n

### Recording
- [ ] `scripts/demo-record.[ext]` exists
- [ ] Playwright viewport matches `recordVideo.size` (both 1920×1080)
- [ ] `ghost-cursor-playwright` installed for human-like mouse movement
- [ ] CSS cursor overlay injected (headless Playwright has no visible cursor)
- [ ] WebM→MP4 re-encode step via FFmpeg (CRF 18, H.264)
- [ ] Clips saved to `demo-video/clips/` with manifest.json

### Remotion Composition
- [ ] Remotion project at `demo-video/remotion/`
- [ ] Master composition reads `demo-script.json` via `inputProps`
- [ ] `calculateMetadata()` computes duration from scene durations
- [ ] TextCard component with accent word parsing and spring animation
- [ ] BrowserMockup / PhoneMockup components with 3D perspective
- [ ] Background music with volume ducking during text cards
- [ ] Spring configs match spec (damping 20/stiffness 100 for text, damping 15/stiffness 120 for mockups)

### Multi-Format
- [ ] 16:9 (1920×1080) composition registered — web/YouTube
- [ ] 9:16 (1080×1920) composition registered — TikTok/Reels/Shorts (if needed)
- [ ] 1:1 (1080×1080) composition registered — LinkedIn/Instagram (if needed)

### Output
- [ ] Rendered videos in `demo-video/out/`
- [ ] H.264 MP4, CRF 18–23, 30fps

---

## Screen Design Artifacts (if screens were designed in Claude.ai)

- [ ] Flow map exists and matches current navigation structure
- [ ] Reference screen (80% screen) identified
- [ ] All screens have locked JSX artifacts saved to disk
- [ ] Visual Production Spec exists (media placeholders, icons, richness layers, mock data quality)
- [ ] States designed for data-driven screens (empty, loading, error)
- [ ] Shared components standardized across screens

---

## Project Documentation

- [ ] PRODUCT.md exists and matches current feature set
- [ ] ARCHITECTURE.md matches current tech stack, data model, env vars
- [ ] DESIGN-SYSTEM.md matches current tokens, typography, components
- [ ] FEATURES.md has dependency map + impact analysis + configurable values
- [ ] PLAYBOOK.md has current focus, up next, definition of done
- [ ] LAUNCH-CHECKLIST.md exists with all sections
- [ ] CLAUDE.md uses current template structure (health skills standard, not commented out)
- [ ] Project Instructions exist in Claude.ai with project-specific content
