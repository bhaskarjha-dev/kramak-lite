# Changelog

All notable changes to Kramak Lite are documented here.

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
- Rule coverage: ~87% → ~95% (of 176 total rules)
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
