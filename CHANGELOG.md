# Changelog

All notable changes to Kramak Lite are documented here.

## [0.1.0-dev] — In Development

> **Target:** First public release.
> **Status:** In development. When ready to release, the `-dev` suffix is dropped and this becomes `[0.1.0]`.

### 2026-09-29 — License Harmonization: Apache 2.0 → MIT

- **License switched to MIT** — Harmonized with full Kramak (MIT). Research confirmed all direct competitors in the AI agent process-control space (GitHub Spec Kit, BMAD-METHOD, Superpowers, GSD Core) use MIT. The skills.sh agent plugin ecosystem and community MCP servers also overwhelmingly favor MIT. Apache 2.0's patent grant provides negligible value for a markdown-based development methodology with no patent portfolio. MIT maximizes adoption for future MCP servers, agent plugins, and ecosystem packaging.
- Updated LICENSE file, README badge, README license section, and ROADMAP open decision (marked resolved).

### 2026-09-29 — Quality Audit Fixes (8 Findings)

- **F-01:** Fixed FAQ adapter size claim (~25 → ~65 lines) in README to match actual AGENTS.md (69 lines) and other README references
- **F-02:** Standardized spec size references to ~56KB across all documentation (README directory tree, ROADMAP ×2, ADR-001). Actual spec: 55,783 bytes ≈ ~56KB
- **F-03:** Defined "fail" audit verdict path — spec §5 now describes when to use `fail` (fundamental misimplementation, all WIs failed, architectural regression), what happens next (re-plan), and how to communicate it. Updated audit-report and session-log templates to include `fail` option
- **F-04:** Updated ROADMAP adapter count from "4 hand-maintained adapters" to "2 adapters (universal AGENTS.md + optional .mdc)" reflecting the adapter consolidation
- **F-05:** Fixed ARCHITECTURE template count from "9 format references" to "11 template files" — was missing conventions.template.md and state.template.json
- **F-06:** Clarified FULL-KRAMAK-MAPPING CLI-only count methodology — 1 rule (174) is fully CLI-only; rules 15 and 159 are condensed with CLI-only sub-aspects replaced by lightweight alternatives. Updated summary table and coverage text
- **F-07:** Fixed .gitignore ledger pattern from `*.md` to `*.jsonl` — spec defines ledger format as JSONL, not Markdown
- **F-08:** Added `ledger/` directory to GETTING-STARTED.md simplified tree

### 2026-09-29 — Universal Adapter Architecture & Track-by-Default Philosophy

Two commits that fundamentally improved the project's distribution model, terminology, and .gitignore philosophy.

#### Adapter Consolidation
- **Universal `AGENTS.md` adapter** — Replaced 4 near-identical per-IDE adapters (Antigravity SKILL.md, Claude Code CLAUDE.md, Cursor .cursorrules, generic AGENTS.md) with one universal adapter. `AGENTS.md` is the industry standard — works natively with all 18+ AI coding harnesses (Claude Code, Cursor, Antigravity, Windsurf, Codex, Cline, Roo Code, Devin, GitHub Copilot, Zed, Amp, Warp, and more).
- **Cursor `.mdc` adapter** — Optional `kramak.mdc` with YAML frontmatter for Cursor-specific priority. Replaces the deprecated `.cursorrules` format.
- **External Orchestrator Integration generalized** — Previously exclusive to the Antigravity adapter, now available universally for any multi-agent framework (Teamwork, Claude Code Agent Teams, Cursor parallel agents, Warp supervisor/worker, Devin parallel instances).

#### .gitignore Philosophy: Track by Default
- **Only `state.json.tmp` is universally ignored** — The WAL crash-recovery temp file is the only truly ephemeral artifact. Everything else in `.kramak/` (state, work items, plans, session logs, audit reports, ledger) is the development process record.
- **Development archaeology** — Tracking Kramak artifacts enables: clone-and-resume on any machine, team visibility into strategic decisions, code review context, crash/machine-death recovery.
- **Distribution repo vs user projects** — This repo ignores dogfooding artifacts; user projects track everything by default. `GETTING-STARTED.md` provides optional lighter-footprint patterns.
- **Spec bootstrap updated** — Git Initialization (§1) now tells the agent to include `.kramak/state.json.tmp` in generated `.gitignore`.

#### Terminology: "Pipeline" → "Workflow"
- Replaced all 13 instances of "pipeline" across spec, templates, INBOX.md, state template, and rule mapping doc.
- Eliminates CI/CD namespace confusion — the same rationale that drove the branch prefix rename from `pipeline/batch-NN` to `kramak/batch-NN`.
- "Specification drift" replaces "pipeline drift" in governance section (more precise).

#### Template & Naming Fixes
- **`AGENTS.template.md` → `conventions.template.md`** — Eliminates naming confusion with `adapters/AGENTS.md`. The template is about project conventions (tech stack, directory structure, code patterns), not about the Kramak adapter.
- **Branch naming: `pipeline/` → `kramak/`** — Self-documenting prefix in `git branch` output. Updated in spec (§3.8, §7.1) and mapping doc.

#### Spec & Schema Fixes
- **Audit verdict enum** — Added `"fail"` to `state.schema.json` verdict enum (was `["pass", "pass-with-fixes"]`). Closes state machine gap.
- **Failure Diagnosis** — Added to Directed and Outcome WI templates (previously only in Guided). All 3 tiers now have consistent failure documentation.
- **Cross-reference fix** — Grounded Verification reference corrected from `§4.2` to `§3.7`.
- **Size standardization** — All documentation references updated from stale `~52KB / ~12,000 tokens` to measured `~56KB / ~14,000 tokens`.
- **Badge fix** — `Dependencies: Zero` → `Runtime Dependencies: Zero` (Git is a tool dependency, not a runtime dependency).
- **`.gitattributes`** — Updated `.cursorrules` line-ending rule to `*.mdc`.
- **Inbox template deduplication** — Removed `templates/inbox.md` (19-byte diff from actual `inbox/INBOX.md`). `INBOX.md` is its own format reference.
- **Spec inbox reference** — Updated bootstrap to reference `inbox/INBOX.md` directly instead of deleted template.

#### Documentation Updates
- **README** — Rewrote Quick Start with universal `AGENTS.md` approach, updated directory tree, comparison table, multi-IDE FAQ.
- **GETTING-STARTED.md** — New Step 3 (`.gitignore` guidance), rewrote Step 2 (adapter installation), updated orchestrator section, renumbered steps.
- **ARCHITECTURE.md** — Updated Adapter Design Pattern section, corrected size/token references (10 locations), updated template count.
- **ROADMAP.md** — Updated adapter reference from SKILL.md to AGENTS.md.

---

## Pre-Release Development History

> The following versions were internal development iterations. They are preserved as a condensed record of the spec's evolution. Version numbers were internal milestone markers.

### Internal 3.0.0 — 2026-09-29 — Governance Protocol Evolution

Evolved Kramak Lite from a session-level playbook into a governance protocol consumable by both humans and orchestrators. Added `executionMode` detection (`manual` | `orchestrated` | `parallel` | `external`), mode-aware role transitions, full parallel dispatch protocol (§7) with safety invariants and merge verification, subagent role prompts (§7.4), and external orchestrator integration (§7.5) for frameworks like Antigravity Teamwork. Backward-compatible — default mode is `manual`. Zero runtime dependencies added.

### Internal 2.3.0 — 2026-08-29 — Unified Cross-Session Telemetry

Added universal session log (all roles append to `SESSION-LOG.md`), structured inbox template with typed items (`bug`, `direction`, `insight`, `data`, `credential`), and executor/auditor handoff logging. Achieved 100% enforceable rule coverage (173 of 173 rules).

### Internal 2.2.0 — 2026-08-29 — Strategic Vision & Meta-Cognition

Added 5-Lens Strategic Vision System (§3.3), PERCEIVE → REASON → DECIDE meta-cognitive loop (§3.4), 25+ perspective archetypes across 5 categories, and perspective diversity tracking.

### Internal 2.1.0 — 2026-08-29 — Non-Negotiable Planning

Added 6 mandatory planning artifacts, hard limit on interactive questions (write to `HUMAN-TASKS.md` instead), cross-session `nextAction` invariant, and production template suite.

### Internal 2.0.0 — 2026-08-29 — Autonomous Engine Overhaul

Transformed Kramak Lite from a structured checklist into a complete autonomous development engine. Added CTO empowerment framing, 5-lens strategic vision, PERCEIVE→REASON→DECIDE meta-cognition, product phase priority ladders (BUILD/SHIP/ITERATE), dynamic batch sizing, capability self-assessment, and branch management. Spec grew from 20.5KB to ~32KB with a 60/40 autonomy/guardrails ratio (v1.x was 10/90).

### Internal 1.0.0–1.3.0 — 2026-08-21 — Foundation & Coverage Sprint

Initial spec (264 lines, 11.2KB) with 6-phase state machine, Goldilocks Rule, circuit breaker, scope enforcement, and 4 IDE adapters. Iterative additions brought rule coverage from ~37% to ~95% through: constitutional framing for IDE compatibility, strategic reorientation, product lifecycle awareness, grounded verification protocol, hard stop gates, failure diagnosis, and pre-dispatch self-audit.

---

<!-- No public release comparison links yet — all versions above are pre-release internal milestones -->
