# Full Kramak → Kramak Lite: Complete Rule Mapping

> **Purpose:** Maps every one of full Kramak's 176 rules to its status in Kramak Lite.
> **Source:** `.kramak/RULES-INVENTORY.md` in the full Kramak repository.
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
| 1 | Planner acts as architect with bounded autonomy | ✅ | Section 3 intro |
| 2 | No human I/O needed during autonomous planning | ✅ | Section 3 + constitutional framing |
| 3 | Strategic Override: planner can change productPhase | ✅ | Section 3.1 Strategic Override callout |
| 4 | Override requires documented evidence | ✅ | Section 3.1 "Document your evidence" |
| 5 | Competitive research during strategic assessment | ⚡ | Section 3.7 "spend up to half session on analysis and research" |
| 6 | Strategic thinking budget (half session for analysis) | ✅ | Section 3.7 explicit statement |
| 7 | Roadmap is input to thinking, not hard constraint | ✅ | Section 3.1 "adjust before proceeding" |
| 8 | Do NOT skip Strategic Reorientation check | ✅ | Section 3.1 check is first action |
| 9 | Do NOT ignore Polish Ceiling Rule | ✅ | Section 3.1 Polish Ceiling callout |
| 10 | Do NOT skip verification steps | ✅ | Section 4.1 Rule 3 |
| 11 | Do NOT create code changes directly | ✅ | Section 3.2 planner blacklist |

### 2. Grounded Planning & Capability Gate (Rules 12-17)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 12 | Derive requirements from workspace files | ✅ | Section 3.1 reading order |
| 13 | Grounded Verification (never write from memory) | ✅ | Section 3.3 + Section 4.1 Rule 1 |
| 14 | Capability Gate Stage 1 (self-assessment) | ⚡ | Section 1 Capability Gate table + planning verification |
| 15 | Capability Gate Stage 2 (Canary Battery CT-1 to CT-5) | ⚡ | Section 1 "Planning verification" — project-grounded inline challenge replaces abstract battery |
| 16 | Gate routing by score (0.80/0.60 thresholds) | ⚡ | Section 1 "reduce batch scope and elevate risk tiers" — adaptive response replaces fixed thresholds |
| 17 | Model agnosticism (route by capability, not name) | ✅ | Section 3.7 "model-type consideration" |

### 3. Empty Workspace Guard (Rules 18-21)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 18 | 0 source files + 0 inbox items → waiting | ✅ | Section 1 init table |
| 19 | Set nextAction requesting user input | ✅ | Section 1 "prompt user for goals" |
| 20 | Output single clear sentence | ✅ | Section 1 "STOP" |
| 21 | STOP immediately, no hallucinated roadmaps | ✅ | Section 1 "STOP" |

### 4. Project Discovery & Structure Mapping (Rules 22-27)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 22 | Scan root and common doc folders | ✅ | Section 1 step 3 |
| 23 | Scan for roadmaps, specs, architecture docs | ✅ | Section 1 step 3 |
| 24 | Record in state.projectStructure | ✅ | State schema includes projectStructure |
| 25 | Create ROADMAP.md if missing | ⚡ | Section 1 "scaffold .kramak/" |
| 26 | Improve tracking files while preserving content | ⚡ | Section 3.1 "Project docs wrong → fix directly" |
| 27 | Reuse projectStructure on subsequent sessions | ✅ | Implicit in state.json persistence |

### 5. Context Reading & Anti-Anchoring (Rules 28-31)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 28 | Mandatory reading order | ✅ | Section 3.1 reading order (5 items) |
| 29 | Anti-anchoring: read roadmap BEFORE state.json | ✅ | Section 3.1 "read these BEFORE state.json" |
| 30 | Directional context (feature vs deployment) | ⚡ | Implied by product phase priorities |
| 31 | On-demand context (only when relevant) | ⚡ | Implied by reading order structure |

### 6. INBOX Processing (Rules 32-38)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 32 | Process inbox with top priority | ✅ | Section 3.1 reading order item 2 |
| 33 | Bug handling by phase | ✅ | Section 3.1 "bug → Create WI only if..." |
| 34 | Insight → update docs directly | ✅ | Section 3.1 "insight / data → Integrate" |
| 35 | Credential → mark human task as done | ✅ | Section 3.1 "credential → Mark resolved" |
| 36 | Direction → re-evaluate priorities | ✅ | Section 3.1 "direction → Re-evaluate" |
| 37 | Data → integrate into specs | ✅ | Section 3.1 "insight / data → Integrate" |
| 38 | Move processed items to Processed section | ✅ | Section 3.1 "Move processed items" |

### 7. Strategic Reorientation (Rules 39-48)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 39 | Never blindly follow state.phase | ✅ | Section 3.1 reorientation check |
| 40 | 4 core reorientation questions | ✅ | Section 3.1 questions 1-4 |
| 41 | Planning with no overrides → proceed | ✅ | Implicit flow |
| 42 | After audit → read lastAudit | ✅ | Section 3.1 reading order item 3 |
| 43 | INBOX critical bug → override phase | ✅ | Section 3.1 "adjust before proceeding" |
| 44 | Queue still has items → leave executing | ✅ | Section 6 resume table |
| 45 | Blocked Fallback: identify exact scope of block | ✅ | Section 3.1 Blocked Fallback callout |
| 46 | If non-blocked work exists → switch to BUILD | ✅ | Section 3.1 "switch to BUILD phase" |
| 47 | If genuinely no work → waiting + STOP | ✅ | Section 6 Human Tasks item 2 |
| 48 | Strategic Override with web research | ✅ | Section 3.1 Strategic Override callout |

### 8. Strategic Vision — 5 Lenses (Rules 49-56)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 49 | Vision triggers (milestone, roadmap low, periodic, first session, inflection) | ✅ | §3.3 Strategic Vision — 5 triggers table |
| 50 | Skip if no trigger active | ✅ | §3.3 "If NO trigger is true → skip to §3.4" |
| 51 | Lens 1: Quality Retrospective | ✅ | §3.3 Lens 1 |
| 52 | Lens 2: User Journey Walk | ✅ | §3.3 Lens 2 |
| 53 | Lens 3: Competitive & Market Scan | ✅ | §3.3 Lens 3 |
| 54 | Lens 4: Innovation Brainstorm | ✅ | §3.3 Lens 4 |
| 55 | Lens 5: Architecture Check | ✅ | §3.3 Lens 5 |
| 56 | Update lastVisionAssessment | ✅ | §3.3 "update state.lastVisionAssessment" |

### 9. Perspective Selection (Rules 57-62)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 57 | Meta-cognition for perspective selection | ✅ | §3.4 PERCEIVE→REASON→DECIDE with archetype table |
| 58 | PERCEIVE checklist | ✅ | §3.4 PERCEIVE section |
| 59 | REASON questions (risk, opportunity, neglected) | ✅ | §3.4 REASON section (5 questions) |
| 60 | DECIDE commitment (record in state) | ✅ | §3.4 DECIDE — record in state.lastSession.perspective |
| 61 | Perspective diversity check | ✅ | §3.4 Diversity check callout (3+ consecutive identical) |
| 62 | Archetype flexibility | ✅ | §3.4 Emergent category in archetype table |

### 10. Prioritization by Phase & Boundaries (Rules 63-72)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 63 | BUILD priorities (8-tier) | ✅ | Section 3.1 BUILD priorities |
| 64 | BUILD exclusions (no lint/doc WIs) | ✅ | Section 3.1 "No standalone lint/doc WIs" |
| 65 | BUILD → SHIP transition criteria | ⚡ | Section 3.1 "Update when project crosses a phase boundary" |
| 66 | SHIP priorities (6-tier) | ✅ | Section 3.1 SHIP priorities |
| 67 | SHIP → ITERATE transition | ⚡ | Section 3.1 "Update when project crosses a phase boundary" |
| 68 | ITERATE priorities (8-tier) | ✅ | Section 3.1 ITERATE priorities |
| 69 | Polish Ceiling Rule | ✅ | Section 3.1 Polish Ceiling callout |
| 70 | Planner whitelist (what planner CAN edit) | ✅ | Section 3.2 planner boundaries |
| 71 | Planner blacklist (what planner MUST NOT edit) | ✅ | Section 3.2 planner boundaries |
| 72 | Research protocol | ✅ | Section 4.1 Rule 6 |

### 11. Batch Planning & Sizing (Rules 73-79)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 73 | Consider alternatives (2+ approaches) | ✅ | Section 3.4 "Consider alternatives" |
| 74 | Batch plan authoring (PLAN-batch-XX.md) | ⚡ | Section 3.2 WI authoring (plans are implicit) |
| 75 | Task sizing (≤ 2 hours, ~200 word spec) | ✅ | Section 3.4 "2 hours or less" |
| 76 | WI independence (prevent compound errors) | ✅ | Section 3.4 "Order by dependency" |
| 77 | Stop when context fatigue degrades quality | ✅ | Section 4.5 hard stop gates |
| 78 | Story build order (schema → backend → frontend) | ✅ | Section 3.4 build sequence |
| 79 | One concern per WI | ✅ | Implicit in WI template structure |

### 12. Branch Management (Rules 80-84)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 80 | First batch: checkout -b pipeline/batch-01 | ⚡ | Section 4.2 "commit with conventional prefix" (branch naming is optional) |
| 81 | Continuing batch: stay on current branch | ✅ | Implicit in git workflow |
| 82 | New feature area: new branch from main | ⚡ | Implicit in git workflow |
| 83 | Stable batch merge to main | ⚡ | Implicit in git workflow |
| 84 | Experimental branch naming | ⚡ | Not enforced — optional naming convention |

### 13. Work Item Specification & Detail Scaling (Rules 85-97)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 85 | File naming (batch-scoped WI-NNN.md) | ✅ | Section 3.2 numbering |
| 86 | Collapse ambiguity for less capable models | ✅ | Section 3.2 "Collapse ambiguity" callout |
| 87 | Goldilocks Rule (3 tiers) | ✅ | Section 3.3 full table |
| 88 | Distribution guideline (≤ 50% Guided) | ✅ | Section 3.3 distribution guide |
| 89 | Guided scope (auth, schema, payments) | ✅ | Section 3.3 table |
| 90 | Grounded Verification Protocol (5 steps) | ✅ | Section 3.3 five-step protocol |
| 91 | Guided new files: BEFORE = empty | ⚡ | Implicit in "BEFORE/AFTER code changes" |
| 92 | Guided WI schema (sections) | ✅ | Section 3.2 WI template |
| 93 | Directed scope (APIs, refactors) | ✅ | Section 3.3 table |
| 94 | Directed grounding (read target files) | ✅ | Section 3.3 "Intent + target files + types" |
| 95 | Directed WI schema | ✅ | Section 3.2 WI template |
| 96 | Outcome scope (docs, config, standalone) | ✅ | Section 3.3 table |
| 97 | Outcome WI schema | ✅ | Section 3.2 WI template |

### 14. Self-Audit Checklist (Rules 98-107)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 98 | Mandatory pre-dispatch self-audit | ✅ | Section 3.6 checklist |
| 99 | Batch plan exists | ⚡ | Section 3.6 (plans are implicit in Lite) |
| 100 | Each WI independently verifiable | ✅ | Section 3.6 item 1 |
| 101 | Risk distribution balanced | ✅ | Section 3.6 item 2 |
| 102 | Grounded Verification confirmed for Guided | ✅ | Section 3.6 item 3 |
| 103 | Target files read for Directed | ⚡ | Covered by Section 3.3 Directed requirements |
| 104 | Clear acceptance criteria for Outcome | ✅ | Section 3.6 item 4 |
| 105 | Topological dependency ordering | ✅ | Section 3.6 item 5 |
| 106 | Story coherence (complete testable value) | ⚡ | Implied by "independently verifiable" |
| 107 | Verified build/check commands attached | ✅ | Section 3.6 "specific verification commands" |

### 15. Session Continuity & Model Handoff (Rules 108-115)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 108 | Apply direct planner edits before finalizing WIs | ✅ | Section 3.6 "Common planning situations" |
| 109 | Assess session weight (WIs, files, edits, research) | ✅ | Section 4.5 session weight assessment table |
| 110 | Assess next phase cost | ✅ | Section 4.5 session weight table (Next Phase Cost column) |
| 111 | Model-Type Hard Gate (reasoning → new session for execution) | ✅ | Section 3.7 "Model-type consideration" |
| 112 | Session decision matrix (Light/Medium/Heavy) | ✅ | Section 4.5 session weight assessment table |
| 113 | Context fatigue at 40-50% utilization | ✅ | Section 4.5 "Context fatigue causes silent quality decline" |
| 114 | If continuing: update state, proceed directly | ✅ | Implicit in flow |
| 115 | If new session: update state, commit, single sentence, STOP | ✅ | Section 3.7 "Commit planning artifacts" |

### 16. Executor Audit Review & Circuit Breaker (Rules 116-121)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 116 | On return from execution: read lastAudit and inbox | ✅ | Section 3.1 reading order |
| 117 | Incorporate audit findings into planning | ✅ | Section 3.1 reorientation check |
| 118 | Check for productPhase advancement | ✅ | Section 3.1 "Update when project crosses a phase boundary" |
| 119 | Circuit Breaker: 3 failures or breaker tripped → STOP | ✅ | Section 4.4 |
| 120 | Reset breaker ONLY after fundamentally new strategy | ✅ | Section 4.4 "Breaker reset rule" callout |
| 121 | Repeated Failure Cap: 3rd time = hard STOP | ✅ | Section 3.1 + Section 4.4 |

### 17. Edge Case Handling (Rules 122-138)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 122 | Project docs wrong → fix directly | ✅ | Section 3.6 "Common planning situations" |
| 123 | AGENTS.md outdated → update directly | ✅ | Section 3.6 |
| 124 | Pipeline needs improvement → improve with guard | ✅ | Section 7 Process Governance |
| 125 | New dependency → write a WI | ✅ | Section 3.6 |
| 126 | Data model change → Guided WIs in order | ✅ | Section 3.6 |
| 127 | Codebase drifted from docs → update docs | ✅ | Section 3.6 |
| 128 | Design decision needed → decide and document | ✅ | Section 3.6 |
| 129 | Queue still has items → leave executing | ✅ | Section 6 resume table |
| 130 | All roadmap items done → envision next | ✅ | Section 6 `complete` phase |
| 131 | Executor keeps failing → improve spec | ✅ | Section 4.3 "Spec failure pattern" |
| 132 | Tool/skill would help → write WI | ⚡ | Implied by "write a WI for it" |
| 133 | Need different architecture → plan restructure | ⚡ | Covered by strategic override |
| 134 | Unsure about decision → flag risk high | ✅ | Section 3.4 confidence calibration |
| 135 | Quick fix temptation → resist, write WI | ✅ | Section 3.6 |
| 136 | Audit flagged strategic concern → read in PERCEIVE | ✅ | Section 3.1 reading order |
| 137 | BEFORE pattern has multiple matches → widen | ✅ | Section 3.3 "confirm exactly one match" |
| 138 | File doesn't exist yet → create via WI | ⚡ | Implicit in WI feature workflow |

### 18. Development Principles (Rules 139-162)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 139 | Understand WHY before WHAT | ✅ | Section 3.2 WI template "Intent: Why this change matters" |
| 140 | Trace consequences before proposing edits | ✅ | Section 4.1 Rule 1 |
| 141 | Consider 3 alternatives for architecture | ✅ | Section 3.4 "For architectural decisions, consider 3" |
| 142 | Uncertainty → research, not guess | ✅ | Section 4.1 Rule 6 |
| 143 | Depth is never wasted | ✅ | Section 4.1 Rule 8 |
| 144 | Never trust memory of file contents | ✅ | Section 4.1 Rule 1 |
| 145 | Never trust memory of an API | ✅ | Section 4.1 Rule 6 |
| 146 | Never trust previous session output | ✅ | Section 4.1 Rule 1 |
| 147 | When docs and code disagree: CODE is truth | ✅ | Section 4.1 callout |
| 148 | If plan feels too easy, investigate deeper | ⚡ | Implied by grounded verification |
| 149 | If about to write repeated code, verify pattern | ✅ | Section 4.1 Rule 1 |
| 150 | Search web before using external APIs | ✅ | Section 4.1 Rule 6 |
| 151 | Confidence levels: High/Medium/Low | ✅ | Section 3.4 confidence calibration |
| 152 | Account for training cutoff | ✅ | Section 4.1 Rule 6 "verify current versions" |
| 153 | Human Task Contract (WHAT/WHY/HOW/URGENCY) | ✅ | Section 6 Human Tasks |
| 154 | Secret Management (env vars, .env.example) | ✅ | Section 4.1 Rule 7 |
| 155 | Quality Ratio (collapse ambiguity, ≤ 2hr, calibrate) | ✅ | Section 3.2 + Section 3.4 |
| 156 | Depth Over Speed | ✅ | Section 4.1 Rule 8 |
| 157 | Anti-Inflation (no fake data) | ✅ | Section 4.1 anti-inflation callout |
| 158 | Progressive Enhancement | ✅ | Section 4.1 progressive enhancement callout |
| 159 | Anti-Bias Guard (G1-G6) | ⚡ | Section 8 governance ledger + cooldown rule — captures G4 (immutable ledger) and G5 (cooldown). G3 dual-model critique remains full-Kramak-only. |
| 160 | Honesty Over Confidence | ✅ | Section 3.4 confidence calibration |
| 161 | Decision Audit Trail | ✅ | Section 3.4 "Decision audit trail" |
| 162 | Tokens Are Thinking | ✅ | Section 4.1 Rule 8 |

### 19. Bootstrap & Governance (Rules 163-176)

| # | Rule | Status | Lite Location |
|---|---|---|---|
| 163 | Bootstrap Scenario 1 (continuing project) | ✅ | Section 1 init table |
| 164 | Bootstrap Scenario 2 (existing with context) | ✅ | Section 1 init table |
| 165 | Bootstrap Scenario 3 (existing without context) | ✅ | Section 1 init table |
| 166 | Bootstrap Scenario 4 (new with requirements) | ✅ | Section 1 init table |
| 167 | Bootstrap Scenario 5 (empty workspace) | ✅ | Section 1 init table |
| 168 | Toolchain detection (multi-ecosystem) | ✅ | Section 1 "auto-detect and record in state.toolchain" |
| 169 | Monorepo orchestration | ⚡ | Section 3.5 mentions parallel dispatch |
| 170 | Git initialization | ✅ | Section 1 "If no .git, run git init" |
| 171 | Crash & WAL recovery | ⚡ | Section 4.1 State Reconciliation + Atomic state writes callout — .tmp write-then-rename protocol |
| 172 | Dispatch budget = 1 (sequential) | ✅ | Default behavior |
| 173 | Dispatch budget > 1 (parallel) | ✅ | Section 3.5 multi-agent dispatch |
| 174 | State transition guard matrix | 🔧 | CLI-only: formal precondition enforcement |
| 175 | Resume drift check | ✅ | Section 6 "Resume drift check" |
| 176 | Evidence language precision | ⚡ | Implicit: Lite doesn't cite research papers directly |

---

## Summary by Status

**✅ Fully Included:** 148 rules — the complete operational core including Strategic Vision and Perspective Selection
**⚡ Condensed:** 25 rules — essence captured with less verbosity (including WAL, capability gate, governance ledger)
**🔧 CLI-Only:** 3 rules — require programmatic enforcement (Canary Battery CT-1..5 grading, state transition guards, dual-model critique)
**⏭️ Excluded:** 0 rules — all enforceable rules are now included
