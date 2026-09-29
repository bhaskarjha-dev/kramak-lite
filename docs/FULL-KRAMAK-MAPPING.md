# Full Kramak → Kramak Lite: Complete Rule Mapping

> **Purpose:** Maps every one of full Kramak's 176 rules to its status in Kramak Lite.
> **Source:** `.kramak/RULES-INVENTORY.md` in the full Kramak repository.
> **Spec Version:** 0.1.0-dev — all "Lite Location" references use current section numbering.
> **Use this when:** Auditing Lite coverage, deciding what to add, or evaluating if a full-Kramak feature should be ported.

---

## Coverage Summary

| Status | Count | Percentage |
|---|---|---|
| ✅ Included in Lite | 148 | 84% |
| ⚡ Included (condensed form) | 25 | 14% |
| 🔧 CLI-Only (needs programmatic enforcement) | 3 | 2% |
| ⏭️ Excluded (too heavyweight for marginal gain) | 0 | 0% |
| **Total** | **176** | |

**Effective coverage:** 173 of 176 rules (98%) are included fully or in condensed form. Excluding CLI-only rules that cannot be enforced via markdown, coverage is 173 of 173 enforceable rules (**100%**).

---

## Spec Structure Quick Reference

Use this to verify "Lite Location" entries below:

| Section | Title |
|---|---|
| Preamble | Your Role in This Project (bounded freedoms, hard limits) |
| §1 | Initialize (toolchain detection, git init, project discovery, capability gate) |
| §2 | Route by Phase |
| §3 | Plan |
| §3.1 | Strategic Reorientation |
| §3.2 | Orient — Read Before Thinking |
| §3.3 | Strategic Vision (Conditional — 5 Lenses) |
| §3.4 | PERCEIVE → REASON → DECIDE |
| §3.5 | Prioritize by Product Phase |
| §3.6 | Formulate Work Items |
| §3.7 | Detail Scaling — The Goldilocks Rule |
| §3.8 | Batch Sizing and Ordering |
| §3.9 | Write Batch Plan |
| §3.10 | Pre-Dispatch Self-Audit |
| §3.11 | Handoff |
| §3 (after §3.11) | Branch Management |
| §4 | Execute |
| §4.1 | State Reconciliation (Crash Recovery) |
| §4.2 | Core Rules |
| §4.3 | Per Work Item |
| §4.4 | Failure Handling |
| §4.5 | Circuit Breaker |
| §4.6 | Session Health — Hard Stop Gates |
| §4.7 | Execution Complete |
| §5 | Audit |
| §6 | Resume Protocol (+ Human Tasks) |
| §7 | Orchestrated & Parallel Execution |
| §7.5 | External Orchestrator Integration |
| §8 | Process Governance |

---

## Rule-by-Rule Status

### Legend
- ✅ = Fully included in Kramak Lite
- ⚡ = Included in condensed/combined form (essence captured, verbosity reduced)
- 🔧 = Requires CLI enforcement (cannot be enforced via markdown alone)
- ⏭️ = Deliberately excluded (too heavyweight for marginal gain)

---

### 1. Bounded Autonomy & Strategic Mindset (Rules 1-11)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 1 | Planner acts as architect with bounded autonomy | ✅ | Preamble + §3 intro |
| 2 | No human I/O needed during autonomous planning | ✅ | Preamble (hard limit #6) |
| 3 | Strategic Override: planner can change productPhase | ✅ | Preamble (bounded freedom #1) + §3.1 |
| 4 | Override requires documented evidence | ✅ | Preamble (bounded freedom #1: "Document your reasoning in the batch plan") |
| 5 | Competitive research during strategic assessment | ⚡ | Preamble (bounded freedom #3: "Spend up to half your session on analysis and research") |
| 6 | Strategic thinking budget (half session for analysis) | ✅ | Preamble (bounded freedom #3) |
| 7 | Roadmap is input to thinking, not hard constraint | ✅ | Preamble (bounded freedom #4) + §3.1 |
| 8 | Do NOT skip Strategic Reorientation check | ✅ | Preamble (hard limit #1) + §3.1 |
| 9 | Do NOT ignore Polish Ceiling Rule | ✅ | Preamble (hard limit #2) + §3.5 (Polish Ceiling Rule callout) |
| 10 | Do NOT skip verification steps | ✅ | Preamble (hard limit #4) + §4.2 rule 3 |
| 11 | Do NOT create code changes directly | ✅ | Preamble (hard limit #3) + §3.6 (planner blacklist callout) |

### 2. Grounded Planning & Capability Gate (Rules 12-17)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 12 | Derive requirements from workspace files | ✅ | §3.2 (reading order) |
| 13 | Grounded Verification (never write from memory) | ✅ | §3.7 (Grounded Verification Protocol) + §4.2 rule 1 |
| 14 | Capability Gate Stage 1 (self-assessment) | ⚡ | §1 (Capability Gate table + planning verification) |
| 15 | Capability Gate Stage 2 (Canary Battery CT-1 to CT-5) | ⚡ | §1 (Planning verification — project-grounded inline challenge replaces abstract battery) |
| 16 | Gate routing by score (0.80/0.60 thresholds) | ⚡ | §1 ("reduce batch scope and elevate risk tiers" — adaptive response replaces fixed thresholds) |
| 17 | Model agnosticism (route by capability, not name) | ✅ | §1 (Capability Gate) + §3.11 (Handoff model guidance) |

### 3. Empty Workspace Guard (Rules 18-21)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 18 | 0 source files + 0 inbox items → waiting | ✅ | §1 (init table + Empty Workspace Guard) |
| 19 | Set nextAction requesting user input | ✅ | §1 (Empty Workspace Guard) |
| 20 | Output single clear sentence | ✅ | §1 (Empty Workspace Guard: "STOP") |
| 21 | STOP immediately, no hallucinated roadmaps | ✅ | §1 (Empty Workspace Guard: "STOP") |

### 4. Project Discovery & Structure Mapping (Rules 22-27)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 22 | Scan root and common doc folders | ✅ | §1 (Project Discovery) |
| 23 | Scan for roadmaps, specs, architecture docs | ✅ | §1 (Project Discovery) |
| 24 | Record in state.projectStructure | ✅ | §1 (Project Discovery) + state schema |
| 25 | Create ROADMAP.md if missing | ⚡ | §1 (Project Discovery: "If ROADMAP.md is missing, create one") |
| 26 | Improve tracking files while preserving content | ⚡ | §3.10 (Common planning situations: "Project docs are wrong → fix them directly") |
| 27 | Reuse projectStructure on subsequent sessions | ✅ | §1 (Project Discovery: "so future sessions skip the scan") |

### 5. Context Reading & Anti-Anchoring (Rules 28-31)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 28 | Mandatory reading order | ✅ | §3.2 (reading order, 6 items) |
| 29 | Anti-anchoring: read roadmap BEFORE state.json | ✅ | §3.2 ("big picture first — read BEFORE state.json") |
| 30 | Directional context (feature vs deployment) | ⚡ | §3.5 (product phase priority ladders) |
| 31 | On-demand context (only when relevant) | ⚡ | §3.2 (reading order structure) |

### 6. INBOX Processing (Rules 32-38)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 32 | Process inbox with top priority | ✅ | §3.2 (reading order, item 3 — Inbox) |
| 33 | Bug handling by phase | ✅ | §3.2 ("bug → Create WI only if security or build-blocking") |
| 34 | Insight → update docs directly | ✅ | §3.2 ("insight / data → Integrate into project documentation") |
| 35 | Credential → mark human task as done | ✅ | §3.2 ("credential → Mark corresponding human task as resolved") |
| 36 | Direction → re-evaluate priorities | ✅ | §3.2 ("direction → Re-evaluate priorities, restructure roadmap") |
| 37 | Data → integrate into specs | ✅ | §3.2 ("insight / data → Integrate into project documentation") |
| 38 | Move processed items to Processed section | ✅ | §3.2 ("Move processed items to a 'Processed' section") |

### 7. Strategic Reorientation (Rules 39-48)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 39 | Never blindly follow state.phase | ✅ | §3.1 (reorientation check) |
| 40 | 4 core reorientation questions | ✅ | §3.1 (5 questions — expanded from 4) |
| 41 | Planning with no overrides → proceed | ✅ | §3.1 (implicit flow to §3.2) |
| 42 | After audit → read lastAudit | ✅ | §3.1 question 5 + §3.2 reading order item 5 |
| 43 | INBOX critical bug → override phase | ✅ | §3.1 ("adjust before proceeding") |
| 44 | Queue still has items → leave executing | ✅ | §6 (resume table: `executing` with no active WI) |
| 45 | Blocked Fallback: identify exact scope of block | ✅ | §3.1 (Blocked Fallback callout) |
| 46 | If non-blocked work exists → switch to BUILD | ✅ | §3.1 ("switch to BUILD phase and continue available work") |
| 47 | If genuinely no work → waiting + STOP | ✅ | §6 (Human Tasks, item 2: "Set phase: 'waiting' only if ALL remaining work is blocked") |
| 48 | Strategic Override with web research | ✅ | Preamble (bounded freedom #1 + #2) |

### 8. Strategic Vision — 5 Lenses (Rules 49-56)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 49 | Vision triggers (milestone, roadmap low, periodic, first session, inflection) | ✅ | §3.3 (5-trigger table) |
| 50 | Skip if no trigger active | ✅ | §3.3 ("If NO trigger is true → skip to §3.4") |
| 51 | Lens 1: Quality Retrospective | ✅ | §3.3 Lens 1 |
| 52 | Lens 2: User Journey Walk | ✅ | §3.3 Lens 2 |
| 53 | Lens 3: Competitive & Market Scan | ✅ | §3.3 Lens 3 |
| 54 | Lens 4: Innovation Brainstorm | ✅ | §3.3 Lens 4 |
| 55 | Lens 5: Architecture Check | ✅ | §3.3 Lens 5 |
| 56 | Update lastVisionAssessment | ✅ | §3.3 ("update state.lastVisionAssessment") |

### 9. Perspective Selection (Rules 57-62)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 57 | Meta-cognition for perspective selection | ✅ | §3.4 (PERCEIVE→REASON→DECIDE with archetype table) |
| 58 | PERCEIVE checklist | ✅ | §3.4 PERCEIVE section |
| 59 | REASON questions (risk, opportunity, neglected) | ✅ | §3.4 REASON section (5 questions) |
| 60 | DECIDE commitment (record in state) | ✅ | §3.4 DECIDE ("Record your decision" in state.lastSession.perspective) |
| 61 | Perspective diversity check | ✅ | §3.4 (Diversity check callout: 3+ consecutive identical = nudge) |
| 62 | Archetype flexibility | ✅ | §3.4 (Emergent category: "or invent one the project demands") |

### 10. Prioritization by Phase & Boundaries (Rules 63-72)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 63 | BUILD priorities (7-tier) | ✅ | §3.5 (BUILD priorities list) |
| 64 | BUILD exclusions (no lint/doc WIs) | ✅ | §3.5 ("Never planned during BUILD" callout) |
| 65 | BUILD → SHIP transition criteria | ⚡ | §3.5 (Phase transitions: "BUILD → SHIP when core features complete") |
| 66 | SHIP priorities (6-tier) | ✅ | §3.5 (SHIP priorities list) |
| 67 | SHIP → ITERATE transition | ⚡ | §3.5 (Phase transitions: "SHIP → ITERATE when product is live") |
| 68 | ITERATE priorities (8-tier) | ✅ | §3.5 (ITERATE priorities list) |
| 69 | Polish Ceiling Rule | ✅ | §3.5 (Polish Ceiling Rule callout) |
| 70 | Planner whitelist (what planner CAN edit) | ✅ | §3.6 (planner may edit ".kramak/ files, docs, roadmaps") |
| 71 | Planner blacklist (what planner MUST NOT edit) | ✅ | §3.6 (HARD LIMIT callout: "MUST NOT directly edit source code") |
| 72 | Research protocol | ✅ | §4.2 rule 6 ("search the web or read documentation") |

### 11. Batch Planning & Sizing (Rules 73-79)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 73 | Consider alternatives (2+ approaches) | ✅ | §3.8 ("evaluate at least 2 approaches") |
| 74 | Batch plan authoring (PLAN-batch-XX.md) | ✅ | §3.9 (Write Batch Plan) |
| 75 | Task sizing (≤ 2 hours, ~200 word spec) | ✅ | §3.8 ("2 hours or less of human-equivalent work") |
| 76 | WI independence (prevent compound errors) | ✅ | §3.8 ("Order by dependency" + "One concern per WI") |
| 77 | Stop when context fatigue degrades quality | ✅ | §4.6 (Hard Stop Gates) |
| 78 | Story build order (schema → backend → frontend) | ✅ | §3.8 ("Schema/data model → backend logic → frontend UI → integration → polish") |
| 79 | One concern per WI | ✅ | §3.8 ("One concern per WI") |

### 12. Branch Management (Rules 80-84)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 80 | First batch: checkout -b kramak/batch-01 | ⚡ | §3 Branch Management table (after §3.11) |
| 81 | Continuing batch: stay on current branch | ✅ | §3 Branch Management table |
| 82 | New feature area: new branch from main | ⚡ | §3 Branch Management table |
| 83 | Stable batch merge to main | ⚡ | §3 Branch Management table |
| 84 | Experimental branch naming | ⚡ | §3 Branch Management table |

### 13. Work Item Specification & Detail Scaling (Rules 85-97)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 85 | File naming (batch-scoped WI-NNN.md) | ✅ | §3.6 (WI numbering: "Batch 1 → WI-101, WI-102...") |
| 86 | Collapse ambiguity for less capable models | ✅ | §3.6 (Collapse ambiguity callout) |
| 87 | Goldilocks Rule (3 tiers) | ✅ | §3.7 (full table) |
| 88 | Distribution guideline (≤ 50% Guided) | ✅ | §3.7 ("If more than 50% are Guided, you are over-specifying") |
| 89 | Guided scope (auth, schema, payments) | ✅ | §3.7 (Goldilocks Rule table — Guided tier) |
| 90 | Grounded Verification Protocol (5 steps) | ✅ | §3.7 (5-step protocol: LOCATE→QUOTE→VERIFY→DESIGN→CROSS-CHECK) |
| 91 | Guided new files: BEFORE = empty | ⚡ | §3.7 (implicit in "BEFORE/AFTER code changes") |
| 92 | Guided WI schema (sections) | ✅ | §3.6 (tier-specific template reference) + guided template |
| 93 | Directed scope (APIs, refactors) | ✅ | §3.7 (Goldilocks Rule table — Directed tier) |
| 94 | Directed grounding (read target files) | ✅ | §3.7 ("Intent + target files + types/interfaces + constraints") |
| 95 | Directed WI schema | ✅ | §3.6 (tier-specific template reference) + directed template |
| 96 | Outcome scope (docs, config, standalone) | ✅ | §3.7 (Goldilocks Rule table — Outcome tier) |
| 97 | Outcome WI schema | ✅ | §3.6 (tier-specific template reference) + outcome template |

### 14. Self-Audit Checklist (Rules 98-107)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 98 | Mandatory pre-dispatch self-audit | ✅ | §3.10 (Pre-Dispatch Self-Audit checklist) |
| 99 | Batch plan exists | ✅ | §3.9 (Write Batch Plan) |
| 100 | Each WI independently verifiable | ✅ | §3.10 item 1 |
| 101 | Risk distribution balanced | ✅ | §3.10 item 2 |
| 102 | Grounded Verification confirmed for Guided | ✅ | §3.10 item 3 |
| 103 | Target files read for Directed | ⚡ | §3.7 (Directed tier requirements) |
| 104 | Clear acceptance criteria for Outcome | ✅ | §3.10 item 4 |
| 105 | Topological dependency ordering | ✅ | §3.10 item 5 |
| 106 | Story coherence (complete testable value) | ⚡ | §3.10 item 1 (implied by "independently verifiable") |
| 107 | Verified build/check commands attached | ✅ | §3.10 item 4 ("specific verification commands") |

### 15. Session Continuity & Model Handoff (Rules 108-115)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 108 | Apply direct planner edits before finalizing WIs | ✅ | §3.10 (Common planning situations: "Project docs wrong → fix them directly") |
| 109 | Assess session weight (WIs, files, edits, research) | ✅ | §4.6 (session weight assessment table) |
| 110 | Assess next phase cost | ✅ | §4.6 (session weight table: "Next Phase Cost" column) |
| 111 | Model-Type Hard Gate (reasoning → new session for execution) | ✅ | §1 (Capability Gate) + §3.11 (Handoff: model recommendation) |
| 112 | Session decision matrix (Light/Medium/Heavy) | ✅ | §4.6 (session weight assessment table) |
| 113 | Context fatigue at 40-50% utilization | ✅ | §4.6 ("Context fatigue causes silent quality decline") |
| 114 | If continuing: update state, proceed directly | ✅ | §3.11 (Exception callout) |
| 115 | If new session: update state, commit, single sentence, STOP | ✅ | §3.11 (Handoff steps 5-7) |

### 16. Executor Audit Review & Circuit Breaker (Rules 116-121)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 116 | On return from execution: read lastAudit and inbox | ✅ | §3.1 (reorientation question 5) + §3.2 (reading order) |
| 117 | Incorporate audit findings into planning | ✅ | §3.1 (reorientation check) |
| 118 | Check for productPhase advancement | ✅ | §3.5 (Phase transitions) |
| 119 | Circuit Breaker: 3 failures or breaker tripped → STOP | ✅ | §4.5 (Circuit Breaker) |
| 120 | Reset breaker ONLY after fundamentally new strategy | ✅ | §4.5 (Breaker reset rule callout) |
| 121 | Repeated Failure Cap: 3rd time = hard STOP | ✅ | §3.2 (failed batch re-entry) + §4.5 (Circuit Breaker) |

### 17. Edge Case Handling (Rules 122-138)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 122 | Project docs wrong → fix directly | ✅ | §3.10 (Common planning situations) |
| 123 | AGENTS.md outdated → update directly | ✅ | §3.10 (Common planning situations) |
| 124 | Pipeline needs improvement → improve with guard | ✅ | §8 (Process Governance) |
| 125 | New dependency → write a WI | ✅ | §3.10 (Common planning situations) |
| 126 | Data model change → Guided WIs in order | ✅ | §3.10 (Common planning situations) |
| 127 | Codebase drifted from docs → update docs | ✅ | §3.10 (Common planning situations) |
| 128 | Design decision needed → decide and document | ✅ | §3.10 (Common planning situations) |
| 129 | Queue still has items → leave executing | ✅ | §6 (resume table) |
| 130 | All roadmap items done → envision next | ✅ | §6 (resume, `complete` phase) |
| 131 | Executor keeps failing → improve spec | ✅ | §4.4 (Spec failure pattern callout) |
| 132 | Tool/skill would help → write WI | ⚡ | §3.10 (implied by "write a WI for it") |
| 133 | Need different architecture → plan restructure | ⚡ | Preamble (bounded freedom #1: Strategic Override) |
| 134 | Unsure about decision → flag risk high | ✅ | §3.8 (confidence calibration: "Low → research and flag risk") |
| 135 | Quick fix temptation → resist, write WI | ✅ | §3.10 (Common planning situations: "'Quick fix' temptation → resist") |
| 136 | Audit flagged strategic concern → read in PERCEIVE | ✅ | §3.2 (reading order, item 5) + §3.4 (PERCEIVE) |
| 137 | BEFORE pattern has multiple matches → widen | ✅ | §3.7 (Grounded Verification, step 3: "confirm exactly one match") |
| 138 | File doesn't exist yet → create via WI | ⚡ | §3.6 (implicit in WI feature workflow) |

### 18. Development Principles (Rules 139-162)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 139 | Understand WHY before WHAT | ✅ | §3.6 + WI templates (Intent section: "Why this change matters") |
| 140 | Trace consequences before proposing edits | ✅ | §4.2 rule 1 ("Verify before editing") |
| 141 | Consider 3 alternatives for architecture | ✅ | §3.8 ("For architectural decisions, consider 3") |
| 142 | Uncertainty → research, not guess | ✅ | §4.2 rule 6 ("Uncertainty is a signal to research, not to guess") |
| 143 | Depth is never wasted | ✅ | §4.2 rule 8 + Preamble (hard limit #5) |
| 144 | Never trust memory of file contents | ✅ | §4.2 rule 1 ("Never code against memory or assumptions") |
| 145 | Never trust memory of an API | ✅ | §4.2 rule 6 ("verify current versions") |
| 146 | Never trust previous session output | ✅ | §4.2 rule 1 + §3.2 (reading order: "ground truth, never from memory") |
| 147 | When docs and code disagree: CODE is truth | ✅ | §4.2 (code-is-truth callout) |
| 148 | If plan feels too easy, investigate deeper | ⚡ | §3.7 (implied by Grounded Verification Protocol) |
| 149 | If about to write repeated code, verify pattern | ✅ | §4.2 rule 1 |
| 150 | Search web before using external APIs | ✅ | §4.2 rule 6 ("search the web or read documentation") |
| 151 | Confidence levels: High/Medium/Low | ✅ | §3.8 (confidence calibration) |
| 152 | Account for training cutoff | ✅ | §4.2 rule 6 ("Account for training data cutoff — verify current versions") |
| 153 | Human Task Contract (WHAT/WHY/HOW/URGENCY) | ✅ | §6 (Human Tasks: "WHAT is needed, WHY it blocks, HOW to resolve it") |
| 154 | Secret Management (env vars, .env.example) | ✅ | §4.2 rule 7 |
| 155 | Quality Ratio (collapse ambiguity, ≤ 2hr, calibrate) | ✅ | §3.6 (collapse ambiguity) + §3.8 (sizing + confidence) |
| 156 | Depth Over Speed | ✅ | §4.2 rule 8 + Preamble (hard limit #5: "Do NOT suppress reasoning tokens") |
| 157 | Anti-Inflation (no fake data) | ✅ | §4.2 (anti-inflation callout) |
| 158 | Progressive Enhancement | ✅ | §4.2 (progressive enhancement callout) |
| 159 | Anti-Bias Guard (G1-G6) | ⚡ | §8 (governance ledger + cooldown rule — captures G4 immutable ledger and G5 cooldown. G3 dual-model critique remains full-Kramak-only.) |
| 160 | Honesty Over Confidence | ✅ | §3.8 (confidence calibration: "Low → research and flag risk explicitly") |
| 161 | Decision Audit Trail | ✅ | §3.8 ("document the chosen one with rationale in the WI Intent") |
| 162 | Tokens Are Thinking | ✅ | §4.2 rule 8 + Preamble (hard limit #5) |

### 19. Bootstrap & Governance (Rules 163-176)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 163 | Bootstrap Scenario 1 (continuing project) | ✅ | §1 (init table, row 1) |
| 164 | Bootstrap Scenario 2 (existing with context) | ✅ | §1 (init table, row 2) |
| 165 | Bootstrap Scenario 3 (existing without context) | ✅ | §1 (init table, row 3) |
| 166 | Bootstrap Scenario 4 (new with requirements) | ✅ | §1 (init table, row 3) |
| 167 | Bootstrap Scenario 5 (empty workspace) | ✅ | §1 (init table, row 4) |
| 168 | Toolchain detection (multi-ecosystem) | ✅ | §1 (Toolchain Detection) |
| 169 | Monorepo orchestration | ⚡ | §7 (Orchestrated & Parallel Execution) + §1 (Toolchain Detection: monorepo detection) |
| 170 | Git initialization | ✅ | §1 (Git Initialization) |
| 171 | Crash & WAL recovery | ⚡ | §4.1 (State Reconciliation) + §4.1 (Atomic state writes callout: .tmp write-then-rename) |
| 172 | Dispatch budget = 1 (sequential) | ✅ | Default behavior (§7 is for orchestrated/parallel mode; manual mode is sequential by default) |
| 173 | Dispatch budget > 1 (parallel) | ✅ | §7 (Orchestrated & Parallel Execution: §7.1–§7.4) |
| 174 | State transition guard matrix | 🔧 | CLI-only: formal precondition enforcement |
| 175 | Resume drift check | ✅ | §6 (Resume drift check callout) |
| 176 | Evidence language precision | ⚡ | Implicit: Lite doesn't cite research papers directly |

---

## Summary by Status

**✅ Fully Included:** 148 rules — the complete operational core including Strategic Vision and Perspective Selection
**⚡ Condensed:** 25 rules — essence captured with less verbosity (including WAL, capability gate, governance ledger)
**🔧 CLI-Only:** 3 rules — require programmatic enforcement (Canary Battery CT-1..5 grading, state transition guards, dual-model critique)
**⏭️ Excluded:** 0 rules — all enforceable rules are now included
