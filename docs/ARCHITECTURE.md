# Architecture & Design Decisions

> This document captures the reasoning behind Kramak Lite's architecture.
> Future contributors: read this before making structural changes.

---

## 1. Why Single-File Architecture

### The Decision
Kramak Lite puts all process instructions in a single file (`KRAMAK-LITE.md`, ~21KB, ~5,252 tokens). Data files (schemas, templates, state, work items) are separate.

### The Reasoning

**Pre-research Kramak (before the research-driven overhaul) used 4 spec files:**
- `spec/PLANNER.md` (40.6 KB, 716 lines)
- `spec/EXECUTOR.md` (17.3 KB, 307 lines)
- `spec/PRINCIPLES.md` (12.2 KB, 231 lines)
- `spec/BOOTSTRAP.md` (7.1 KB, 130 lines)

Per-session token loading:
- **Planning session:** ~54 KB (~13,500 tokens) loaded — PRINCIPLES.md + PLANNER.md
- **Executing session:** ~31 KB (~7,750 tokens) loaded — PRINCIPLES.md + EXECUTOR.md
- **Kramak Lite (any session):** ~21 KB (~5,252 tokens) loaded — just KRAMAK-LITE.md

**Post-research Kramak (current full spec) uses 20 files / 191 KB** with progressive loading via ROUTER.md. This is necessary at 191KB to avoid lost-in-middle attention degradation.

**At 21 KB, single-file is strictly superior because:**

1. **Fewer failure points.** Multi-file = 3+ `view_file` calls per session. Each can fail, truncate, or be skipped. Single file = 1 call = everything loaded.
2. **No routing overhead.** Pre-research adapter had a routing table (phase → file). That table itself consumed attention and could be followed incorrectly.
3. **5,252 tokens is in the sweet spot.** "Lost in the middle" kicks in at ~40-50% context utilization. At 5,252 tokens in a 128K context, we're at ~4% — deep in the high-attention primacy zone.
4. **Section headers ARE routing.** When the model reads `## 4. Execute` and knows `state.phase === "executing"`, it naturally follows that section. No explicit routing needed.
5. **The "waste" is negligible.** During execution, the model reads ~8KB of planning instructions it doesn't need. That's ~2,000 extra tokens — 1.5% of a 128K context window.

### The Threshold
If KRAMAK-LITE.md grows past ~40KB (~10,000 tokens), splitting becomes necessary. But at 21KB, we're well below this.

### What's Correctly Separate
- **Schemas** (`state.schema.json`, `work-item.schema.json`) — machine-readable validation, not instruction text
- **Templates** (`WORK-ITEM.template.md`) — format reference, not process instructions
- **State** (`state.json`) — runtime data, read/written separately
- **Work Items** (`work-items/*.md`) — output artifacts created by the model
- **Inbox** (`inbox/`) — input artifacts written by the user

These are **data files**, not **instruction files**. Instructions go in one place. Data is naturally distributed.

---

## 2. IDE System Prompt Compatibility

### The Problem
When Kramak runs inside an IDE (Antigravity, Claude Code, Cursor), the IDE's system prompt has higher authority than Kramak's instructions. This creates instruction shadowing where:

1. **IDE system prompt** (highest priority) says: "You are Antigravity, a coding assistant..."
2. **Kramak adapter** (medium priority, loaded as a skill/rule) says: "Read KRAMAK-LITE.md and follow the workflow"
3. **KRAMAK-LITE.md** (lowest priority, loaded as a user-level document) contains the actual process

When IDE instructions conflict with Kramak (e.g., IDE says "keep responses concise" but Kramak says "do not suppress reasoning"), the IDE wins. This was confirmed in practice with Gemini Flash in Antigravity IDE.

### The Resolution: Constitutional Framing

Instead of fighting the IDE's authority, align with it:

| Approach | Old Framing | New Framing |
|---|---|---|
| Identity | "You are the planner/executor" | (No identity claims — avoids conflicting with IDE's "You are X") |
| Purpose | "Follow this process" | "This workflow helps you produce higher-quality code" |
| Rules | "You MUST do X" | "Doing X prevents failure Y" — model sees the value, not just the constraint |
| Spec name | "Why This Workflow Exists" | "How This Helps You" |

This works because:
- **No identity conflict** — Kramak doesn't try to override the IDE's "You are X" prompt
- **Cooperative framing** — "helps you" positions Kramak as enhancing the agent, not constraining it
- **Failure-linked rules** — each rule names the failure it prevents, so the model has intrinsic motivation to follow it

### Adapter Design Pattern
Each adapter (SKILL.md, CLAUDE.md, .cursorrules, AGENTS.md):
1. Uses constitutional framing ("helps you produce higher-quality code")
2. Lists 5 always-active rules that apply even before "Start" is said
3. Provides a quick-reference phase table
4. Points to KRAMAK-LITE.md as the single source of truth

### Known Limitations
- IDE system prompts are proprietary and change without notice
- Some IDEs may override specific Kramak rules (e.g., "keep responses concise" overrides "do not suppress reasoning")
- The adapter is advisory — there's no programmatic enforcement. That's what kramak-cli is for.

---

## 3. Relationship to Full Kramak

### What Kramak Lite Keeps (~95% of value)
- The complete plan/execute/audit lifecycle
- All 6 phases (planning, executing, auditing, waiting, escalated, complete)
- Goldilocks Rule with 3 detail tiers
- 6-category failure taxonomy with recovery shortcuts
- Circuit breaker with oscillation detection
- Hard stop gates (quantitative session limits)
- Session weight assessment
- Product lifecycle (BUILD/SHIP/ITERATE)
- Strategic reorientation + strategic override
- Pre-dispatch self-audit
- Grounded Verification Protocol (5-step)
- Scope enforcement (pre-execution intercept + post-commit git diff)
- Neighborhood cleanup
- Audit quality gate
- Progressive enhancement
- Constitutional framing for IDE compatibility

### What's Deliberately Excluded

**CLI-Only Features (need programmatic enforcement):**
| Feature | Why CLI-Only |
|---|---|
| Canary Gate (CT-1 to CT-5) | Requires programmatic challenge generation + grading |
| WAL Atomic Writes | Requires filesystem write-then-rename operations |
| Anti-Bias Guard G3-G6 | G3 dual-model critique and G4 ledger require external tooling |
| 3-Tier Scope Check | Tier 2 (glob) and Tier 3 (merge) need programmatic verification |
| Error hash computation | SHA-256 hashing requires programmatic tooling |
| Formal audit ledger | `.kramak/ledger/self-modifications.jsonl` requires append-only writes |

These features are deferred to [kramak-cli](https://github.com/bhaskarjha-dev/kramak-cli).

**Not Needed in Lite (too heavyweight for marginal gain):**
| Feature | Why Excluded |
|---|---|
| 5 Strategic Lenses | ~500 bytes for marginal gain. Replaced by Strategic Reorientation Check (covers 80% of the value) |
| Perspective Rotation | Archetype cycling (Solution Architect, UX Designer, etc.) adds ceremony without proportional value at Lite scale |
| Detailed branch naming | Lite covers basic git. `pipeline/batch-XX` naming is optional convention |
| Domain conventions module | Ecosystem-specific playbooks (React, Python, Go, Rust patterns) — too large, model already knows these |

---

## 4. Token Budget Analysis

### Full Kramak Token Cost Per Session
```
ROUTER.md:                ~500 tokens (always loaded)
planner/CORE.md:         ~8,200 tokens (if planning)
  + edge-cases.md:       ~2,900 tokens (on-demand)
  + output-contract.md:  ~4,200 tokens (on-demand)
  + domain-conventions.md: ~2,400 tokens (on-demand)
  + capability-gate.md:  ~2,650 tokens (on-demand)
executor/CORE.md:        ~5,400 tokens (if executing)
  + error-recovery.md:   ~5,600 tokens (on-demand)
  + tool-playbooks.md:   ~4,100 tokens (on-demand)

Worst case (full planner session): ~18,850 tokens of instructions
Typical execution session:         ~11,500 tokens of instructions
```

### Kramak Lite Token Cost Per Session
```
KRAMAK-LITE.md:          ~5,252 tokens (everything, every session)
```

**Reduction: 55-72% fewer instruction tokens per session.**

### Safe Threshold
- Modern context windows: 128K-1M tokens
- "Lost in the middle" threshold: ~40-50% utilization
- Kramak Lite at 5,252 tokens: 4.1% of 128K, 0.5% of 1M
- **Verdict:** Well within the high-attention zone for any model

---

## 5. Pre-Research Kramak Insights

Before the research-driven overhaul (commit `9c6b205`), Kramak worked as a simpler multi-file system. Key learnings from that era:

1. **Templates were for bootstrapping, not runtime.** The 8 template files (guided/directed/outcome WIs, batch plan, audit report, etc.) existed for `init.sh` to scaffold projects. The model learned WI format from inline examples in PLANNER.md, not from template files.

2. **The model played both roles.** Even with separate PLANNER.md and EXECUTOR.md, the same model session often did both planning and executing. The role separation was conceptual, not enforced.

3. **54KB loading for planning was too much.** At 13,500 tokens of instruction text, planning sessions had attention dilution in the middle of PLANNER.md (716 lines).

4. **productPhase existed from the start.** Even pre-research Kramak had lifecycle awareness — this wasn't a research addition, it was a proven concept.

5. **The core loop was always the same.** Plan → Execute → Audit → Repeat. The research added rigor (Goldilocks Rule, circuit breaker, error taxonomy) but the fundamental loop was proven.

---

## 6. Future Development Priorities

### Phase 2: kramak-cli
A terminal-based enforcement layer that can programmatically enforce the rules Kramak Lite can only advise:
- WAL atomic writes for state.json
- Canary Gate challenge battery
- Anti-Bias Guard with formal ledger
- 3-tier scope check (file-level, glob, merge)
- Error hash computation and oscillation detection

### Adapter Improvements
- Monitor IDE system prompt changes and update adapters accordingly
- Test with more model tiers (Flash, Haiku, GPT-4o-mini) to verify constitutional framing effectiveness
- Consider "always-active rule" elevation for IDEs that support it

### Spec Maintenance
- If the spec grows past 40KB, consider splitting into PLANNER-LITE.md and EXECUTOR-LITE.md
- Keep the single-file architecture as long as it stays under the attention threshold
- Audit spec size quarterly against model context window advances
