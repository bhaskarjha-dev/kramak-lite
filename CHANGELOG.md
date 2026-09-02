# Changelog

All notable changes to Kramak Lite are documented here.

## [2.3.0] - 2026-08-29

### Added — Unified Cross-Session Telemetry & Inbox Template
- **Universal Session Log (`.kramak/templates/session-log.md`)** — Replaces single-purpose planning log with a unified cross-session log. All roles (Planner, Executor, Auditor) append entries, providing full narrative history in `.kramak/SESSION-LOG.md`.
- **Structured Inbox Template (`.kramak/templates/inbox.md`)** — Standardized template with `Unprocessed` and `Processed` sections and explicit item types (`bug`, `direction`, `insight`, `data`, `credential`).
- **Initial Inbox Tracking** — Pre-populated `.kramak/inbox/INBOX.md` and `.kramak/inbox/.gitkeep` in the repository for immediate out-of-the-box onboarding.
- **100% Enforceable Rule Coverage** — Updated mapping to reflect that all 173 enforceable rules from full Kramak are covered (148 full, 25 condensed).

### Changed
- **Executor Handoff (§4.7)** — Added mandatory step 2 to log execution summary (completed/failed WIs, key issues, session gates triggered) to `.kramak/SESSION-LOG.md`.
- **Auditor Handoff (§5)** — Added mandatory step 9 to log audit summary (verdict, fixes applied, strategic concerns, recommendations) to `.kramak/SESSION-LOG.md`.
- **Spec Size** — ~45KB (625 lines), encapsulating the complete autonomous engine and telemetry.

---

## [2.2.0] - 2026-08-29

### Added — Strategic Vision & Meta-Cognitive Perspective Selection
- **5-Lens Strategic Vision System (§3.3)** — Conditional assessment (Quality Retrospective, User Journey Walk, Competitive & Market Scan, Innovation Brainstorm, Architecture Check) triggered at milestones, roadmap depletion, periodic intervals, or planner judgment.
- **PERCEIVE → REASON → DECIDE Loop (§3.4)** — Deep meta-cognitive planning loop with 5 strategic questions and 25+ named perspective archetypes across 5 categories.
- **Perspective History Tracking** — Rolling window of last 5 perspectives stored in `state.perspectiveHistory` with diversity check (3+ consecutive identical = nudge to switch).

---

## [2.1.0] - 2026-08-29

### Added — Rigorous Non-Negotiable Planning & Session Handoffs
- **Non-Negotiable Planning Minimum (§3)** — 6 mandatory planning artifacts required before transitioning to execution (cannot skip for urgency or hackathons).
- **Hard Limit: No Interactive Questions** — Bounded autonomy invariant: agent does not interrupt users with questions; writes to `.kramak/HUMAN-TASKS.md` instead.
- **Cross-Session `nextAction` Invariant** — Every exit path (planner, executor, auditor, circuit breaker, waiting) writes an explicit `nextAction` string to `state.json`.
- **Production Template Suite** — Added templates for batch plans, human tasks, audit reports, and retrospectives.

---


## [2.0.0] - 2026-08-29

### Changed — Autonomous Engine Overhaul

v2.0.0 transforms Kramak Lite from a structured development checklist into a **complete autonomous development engine**. The v1.x series successfully solved IDE system prompt conflicts via constitutional framing but over-corrected — it preserved the skeleton (phases, WIs, state.json) while losing the soul (strategic intelligence, meta-cognition, autonomous decision-making).

This release restores the full autonomous engine from the pre-research Kramak and the research-backed innovations, compressed into the single-file format.

### Added — Strategic Intelligence Layer (~5KB)
- **CTO Empowerment Framing** — opening mandate with bounded freedoms (strategic override, competitive research, strategic thinking budget, question everything) and hard limits (don't skip verification, don't skip reorientation). Constitutional framing preserved — no identity claims, no harness behavior prescriptions.
- **Strategic Vision System (5-lens)** — conditional 5-lens strategic assessment triggered at milestones, roadmap depletion, periodic intervals, first session, or planner judgment. Lenses: Quality Retrospective, User Journey Walk, Competitive & Market Scan, Innovation Brainstorm, Architecture Check.
- **PERCEIVE → REASON → DECIDE meta-cognition** — full meta-cognitive planning loop. PERCEIVE reads situational state. REASON asks 5 strategic questions (biggest risk, biggest opportunity, what's neglected, what hire to make, what users would complain about). DECIDE names the perspective and why.
- **Perspective Archetype System** — 25+ named perspectives across 5 categories (Building, Product, Operational, Growth, Emergent) with diversity check (3+ consecutive same perspective = nudge to switch).
- **Product Phase Priority Ladders** — explicit ordered priority stacks for BUILD (7 tiers), SHIP (6 tiers), ITERATE (8 tiers) with transition criteria and "never planned during BUILD" exclusions.
- **Dynamic Batch Sizing** — replaced hard-coded "3-8 WIs" with "produce until your planning quality degrades." Typical healthy range 3-15, driven by context quality, not arbitrary caps.
- **Batch Plan Document** — `.kramak/plans/PLAN-batch-NN.md` with strategic intent, chosen perspective, stories ordered by dependency, and risk assessment.
- **Capability Self-Assessment** — model evaluates its fit for the current phase (planning/executing/auditing) with decision paths (proceed, warn and proceed, recommend model switch).
- **Branch Management** — explicit branching strategy table (first batch, continuing, new feature, stable merge, experimental).
- **Build Order Awareness** — schema → backend → frontend → integration → polish sequence guidance in executor.

### Changed
- **Preamble** — from "structured workflow" to "autonomous development engine" with full bounded autonomy framing
- **§3 Plan** — expanded from 4-section checklist to 11-section strategic planning engine
- **§5 Audit** — now includes batch plan review for strategic intent verification
- **§4.2 Per Work Item** — executor reads batch plan first for strategic context
- **Adapters** — all 4 adapters now include "Project Authority" section reinforcing strategic empowerment
- **State schema** — added `productPhase`, `lastSession.perspective`, `lastVisionAssessment`, `currentBranch`, `deploymentBlocked`, expanded `lastAudit`

### Added — Structural
- `.kramak/plans/` directory for batch plan documents

### Size
- Spec size: 20.5 KB → ~32 KB (~7,500 tokens)
- Still smaller than pre-research per-session context (31-56 KB)
- Still under 6% of 128K context window — deep in the high-attention primacy zone
- Ratio: 60% autonomy engine / 40% guardrails (v1.x was 10% autonomy / 90% guardrails)

---

## [1.3.0] - 2026-08-21

### Added — 13 additions to reach ~95% rule coverage
- **Strategic Override protocol** — planner can change `productPhase` with documented evidence (prevents stuck phases)
- **Blocked Fallback** — if deployment is blocked by human tasks, switch to BUILD phase and keep working
- **Anti-anchoring reading order** — read roadmap BEFORE `state.json` so planner forms independent assessment
- **Credential inbox type** — handle `credential` type in inbox to unblock dependent work
- **Planner blacklist** — planner must NOT directly edit source code, schemas, or package dependencies
- **Collapse ambiguity principle** — "spend tokens on WHAT and WHY, not code"
- **3-alternative evaluation** — for architectural decisions, evaluate 3 approaches instead of 2
- **Confidence calibration** — rate confidence per WI: High (proceed), Medium (verify first), Low (research + flag)
- **Decision audit trail** — document why approach chosen over alternatives in WI Intent
- **Progressive enhancement** — implement graceful degradation for missing data, not crashes
- **Recovery shortcuts by category** — actionable per-category recovery: code-drift re-scan, scope-exceeded ad-hoc WI, dependency reorder
- **Breaker reset rule** — only reset circuit breaker after fundamentally different strategy
- **Session weight assessment** — light/medium/heavy decision matrix for continue vs fresh session
- **INBOX template** — `.kramak/inbox/INBOX.md` with format examples for user onboarding

### Coverage
- Rule coverage: ~87% → ~92% (162 of 176 total rules; ~95% of enforceable non-CLI rules)
- Spec size: 17.6 KB → 20.5 KB (386 lines, ~5,252 tokens)

---

## [1.2.0] - 2026-08-21

### Added — 8 additions from exhaustive cross-file audit
- **Constitutional framing** — reframed spec from "follow this process" to "this helps you produce better work" (the #1 IDE compatibility fix)
- **Git initialization** — if `.git` missing, run `git init` and create `.gitignore` for detected stack
- **Pre-execution scope intercept** — check file path BEFORE editing, not just after (preventive vs detective control)
- **Neighborhood cleanup** — fix obvious bugs in touched lines within scope, don't open unlisted files
- **Hard stop gates** — replaced vague "behavioral metrics" with concrete thresholds (6 WIs, 20 files, 4 errors, 1 failure)
- **Failure diagnosis format** — structured error trajectory (attempt-by-attempt) gives planner actionable debugging data
- **Tier elevation on retry** — when same area fails, auto-elevate Outcome→Directed→Guided
- **Audit quality gate** — auditor must be at least as capable as executor; execution-grounded, not subjective

### Changed
- All 4 adapters rewritten with constitutional framing + mojibake fixes
- README updated with correct spec sizes and feature comparison
- WI template updated with failure diagnosis section
- Getting Started doc updated for v1.2 features

### Coverage
- Rule coverage: ~80% → ~87%
- Spec size: 15.9 KB → 17.6 KB (357 lines)

---

## [1.1.0] - 2026-08-21

### Added — 12 strategic intelligence gaps closed
- **Strategic Reorientation Check** — 4-question guard against blindly following stale state
- **Product lifecycle awareness** (`productPhase`) — BUILD/SHIP/ITERATE priority guidance
- **Anti-anchoring reading order** — read project docs before state to prevent confirmation bias
- **INBOX processing protocol** — classify by type (bug/direction/insight/data), route appropriately
- **Polish Ceiling Rule** — stop polishing when build passes and linter has 0 errors
- **Pre-dispatch self-audit checklist** — 5-point verification before committing plan to execution
- **Research protocol** — search web for APIs/libraries, read docs, verify current versions
- **Failed batch re-entry** — check for 3+ repeat failures before retrying same strategy
- **Common planning situations** — quick-reference for docs-wrong, need-dependency, schema-change, design-decision
- **Grounded Verification Protocol** — 5-step LOCATE→QUOTE→VERIFY→DESIGN→CROSS-CHECK for Guided WIs
- **Model-type consideration** — recommend fast model for execution if planning with expensive reasoning model
- **Strategic thinking budget** — spend up to half session on analysis, but MUST produce actionable WIs

### Changed
- State schema updated: added `productPhase` enum and `projectStructure` object

### Coverage
- Rule coverage: ~37% → ~80%
- Spec size: 11.2 KB → 15.9 KB (333 lines)

---

## [1.0.0] - 2026-08-21

### Added — Initial release
- Single-file spec: `KRAMAK-LITE.md` (264 lines, 11.2 KB)
- 6-phase state machine: planning → executing → auditing → waiting → escalated → complete
- Goldilocks Rule (Guided/Directed/Outcome detail scaling)
- Circuit breaker (3 consecutive failures = escalate)
- 6-category failure taxonomy
- Scope enforcement via `files_targeted` + git diff check
- Toolchain auto-detection (Node, Python, Rust, Go)
- Work Item template with YAML frontmatter
- State and Work Item JSON schemas
- 4 IDE adapters: Antigravity, Claude Code, Cursor, Generic
- Getting Started guide
- README with comparison table

### Coverage
- Rule coverage: ~37% of full Kramak's 176 rules
- Spec size: 11.2 KB (264 lines)

### Design Decisions
- **Single file over multi-file** — see `docs/ARCHITECTURE.md` for rationale
- **No runtime dependencies** — pure Markdown + JSON schemas
- **Constitutional framing** — avoid identity claims that conflict with IDE system prompts
