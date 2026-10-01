# Changelog

All notable changes to Kramak Lite are documented here.

## [0.1.0-dev] — In Development

> **Target:** First public release.
> **Status:** In development. When ready to release, the `-dev` suffix is dropped and this becomes `[0.1.0]`.

### 2026-10-01 — Quality Amplification: 7 Changes from Comparative Test Forensics

Controlled 4-scenario test (same prompt, with/without Kramak) revealed that Kramak-governed outputs failed while direct prompting succeeded. Root cause analysis identified that the spec optimized for process compliance over functional reality. These changes shift Kramak from a "guardrail system" to a "quality amplification engine" — each phase now actively produces superior results rather than just governing process.

**Preamble — Quality value proposition:**
- Added 5-point quality amplification framing ("This workflow produces results that exceed what unstructured development can achieve") alongside existing failure prevention list. Signals to agents that the goal is excellence, not just rule-following.

**§1 — Verification quality rule (NEW):**
- Added mandatory verification quality guidance to Toolchain Detection. `checkCommands` must verify what users actually experience, not just what the compiler accepts. Explicitly calls out that `node --check` is insufficient for browser apps (the exact failure mode observed). Covers web apps, APIs, CLIs, and libraries.

**§1 — Governance Scope Assessment (NEW):**
- Added SPRINT/CAMPAIGN governance scope mechanism. SPRINT (≤5 WIs, single session) collapses planning/execution/audit into one session. CAMPAIGN (multi-session) retains full governance. Quality mechanisms (architecture-first planning, functional verification, critical review) are non-negotiable in both scopes.
- Added `governanceScope` field to state schema and template.
- Added SPRINT carve-out to §2's one-role-per-agent rule.
- Adjusted Non-Negotiable Planning Minimum to allow session log batch plan notes in SPRINT scope.

**§3.6 — Architecture-first planning (NEW):**
- Before decomposing into WIs, planners must design the integration architecture: entry points, module interfaces, initialization order, and integration contracts. This is the planner's primary value-add.

**§3.6 — Integration coherence rule (NEW):**
- If a WI's acceptance criteria reference a file, that file MUST appear in `files_targeted`. Prevents impossible contracts.

**§3.8 — Integration ownership (NEW):**
- Every batch must end with a functioning, integrated system. Last WI must include orchestrator wiring or be a dedicated integration WI.

**§3.10 — Pre-dispatch checklist expanded:**
- Added integration coherence check and verification adequacy check.

**§3.11 — SPRINT governance path (NEW):**
- First-class SPRINT path: planner proceeds directly to §4 after planning, self-reviews at end of session. Not a shortcut — same quality bar, lighter process.

**§4.2 — Scope enforcement flexibility:**
- Rule 2 now has two exceptions: (a) test co-evolution (test files may be created/updated alongside features), (b) minimal orchestrator wiring (import/instantiation lines in entry points). Prevents the "scope prison" that froze test infrastructure and blocked integration.
- Rule 3 now includes: "If `checkCommands` passes but the application visibly does not work, the verification suite is broken — fix it." Prevents false confidence from passing but meaningless checks.

**§4.3 — Verification honesty:**
- Step 7 now instructs: if checks pass but the change is visibly broken, do NOT proceed.

**§4.7 — Batch integration check (NEW):**
- Before declaring execution complete, verify components work as an integrated system. Individual WI verification ≠ system verification.

**§5 — Functional acceptance test (NEW Step 3):**
- Auditor must verify the application works as a real user would experience it (web: renders + responds; API: endpoints respond; CLI: commands execute). If functional test fails but `checkCommands` passes, verification suite is inadequate.

**§5 — Auditor fix re-verification:**
- After any `fix(audit):` commit, re-run `checkCommands` AND functional acceptance test. Prevents auditor-introduced bugs from escaping.

**§5 — Completion acceptance gate (NEW):**
- Before `phase: "complete"`, application must pass both `checkCommands` and functional acceptance test. "All WIs completed" is necessary but not sufficient.

### 2026-09-29 — Deep Audit: 16 Findings Fixed (F-01 through F-17)

Independent quality audit identified 17 findings across 5 severity levels (3 Critical, 4 High, 4 Medium, 6 Low). F-05 (Cursor `.mdc` empty `globs` field) was determined to be **correct behavior** per Cursor's documented `.mdc` format and was not changed. All remaining 16 findings were fixed:

**Critical (Fixed):**
- **F-02:** SESSION-LOG.md bootstrap gap — added Runtime Artifact Bootstrap subsection to §1 Initialize in spec. Previously, SESSION-LOG.md creation was only mentioned in §3.11 (Handoff), meaning agents that never reached that section wouldn't create the file.
- **F-03:** HUMAN-TASKS.md bootstrap gap — same fix, same subsection. Both cross-session files are now explicitly bootstrapped during initialization.
- **F-01:** Self-assessed competitive scores presented as authoritative — added methodology caveat to README comparison table, added "(Author-Assessed)" to COMPARISON.md subtitle, added pre-release note to README IDE compatibility claim.

**High (Fixed):**
- **F-04:** Competitive score inconsistency (ADR-001: 25/30 vs COMPARISON: 23/30 vs ROADMAP: 23/30) — reconciled all documents to 25/30 reflecting governance protocol evolution (+1 Workflow Rigor, +1 Host/Model Reach per ADR-001 analysis). Updated COMPARISON.md rank, gap analysis, and ROADMAP scoreboard. Marked ROADMAP backlog item #6 as resolved.
- **F-06:** State template missing `lastSession.batchNumber` — added `"batchNumber": 0` to state.template.json.
- **F-07:** FULL-KRAMAK-MAPPING.md coverage counts wrong (claimed ✅=148, actual ✅=150) — programmatic recount verified 150/25/1/0=176. Updated summary table (148→150, 84%→85%), coverage text (173→175, 98%→99%), and bottom summary.

**Medium (Fixed):**
- **F-08/F-08b/F-09:** Stale counts — adapter line count "~65" updated to "~70" across README (×2) and GETTING-STARTED.md. ADR-001 and ADR-003 annotated with "[Note: Subsequently consolidated to 2 adapters]". ADR-003 rule count updated from 173/173 to 175/175.
- **F-10:** State schema lacked conditional validation — added `if/then` block requiring `escalation.reason` when `phase: "escalated"`.
- **F-11:** No contributing guidelines — created CONTRIBUTING.md with issue reporting, PR checklist, ADR process, and project-specific constraints.

**Low (Fixed):**
- **F-12:** `.gitattributes` used CRLF line endings — rewritten with LF endings.
- **F-15:** Session log template said "newest first" but spec said "append" — resolved by changing template to "oldest first (append new entries at the bottom)" to match spec's append instruction.
- **F-17:** State template used empty strings `""` for `model` and `timestamp` (invalid per JSON Schema date-time format) — changed to `null`. Updated state schema to allow `["string", "null"]` for both fields.
- **F-14:** README directory tree showed runtime-created files without explanation — added clarifying note above tree.
- **F-16:** ADR-003 adapter/rule count stale — fixed alongside F-09.
- **F-13:** WI schema placeholder `WI-NNN` — acknowledged as a non-issue (placeholder is universally understood).

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
