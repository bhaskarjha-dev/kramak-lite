# Kramak Lite - Autonomous Development Process

> **Version:** 1.0.0
> **What this is:** A lightweight, structured workflow for autonomous software development.
> **Activate:** When the user says **"Start"** (or "begin", "continue", "go", "kramak").

## Why This Workflow Exists

This process prevents the 5 most documented autonomous coding failures:

1. **Scope drift** - editing files outside the task boundary
2. **Hallucinated references** - coding against imagined file contents instead of real ones
3. **Context fatigue** - quality degrading silently as sessions grow longer
4. **Infinite fix loops** - retrying the same failing approach endlessly
5. **Under/over-specification** - either too vague (70-95% failure) or too detailed (model degradation)

Following this workflow produces higher-quality, more reliable autonomous code.

---

## 1. Initialize

Read `.kramak/state.json`. Handle each case:

| Situation | Action |
|---|---|
| `state.json` exists | Read it. Route by `phase` (see Section 2). |
| `state.json` missing, code exists | Detect toolchain, create `state.json` with `phase: "planning"`. |
| `state.json` missing, workspace empty | Ask what to build. Create `state.json` with `phase: "waiting"`. STOP. |

### Toolchain Detection
Scan the workspace root to populate `state.toolchain`:
- `package.json` -> Node.js (`npm test`, `npm run build`, `npx tsc --noEmit`)
- `Cargo.toml` -> Rust (`cargo build`, `cargo test`, `cargo clippy`)
- `pyproject.toml` / `requirements.txt` -> Python (`pytest`, `mypy .`, `ruff check .`)
- `go.mod` -> Go (`go build ./...`, `go test ./...`, `go vet ./...`)
- Other ecosystems: detect and populate `checkCommands` accordingly.

Store in `state.json`:
```json
{
  "phase": "planning",
  "toolchain": {
    "checkCommands": ["npm test", "npx tsc --noEmit"],
    "detected": true
  }
}
```

---

## 2. Route by Phase

| Phase | What To Do |
|---|---|
| `planning` | Section 3 - Plan a batch of work items |
| `executing` | Section 4 - Execute work items from the queue |
| `auditing` | Section 5 - Verify completed work |
| `waiting` | Human action needed. Show what is blocking. STOP. |
| `escalated` | 3+ consecutive failures. Show diagnosis. STOP. |
| `complete` | Check `inbox/` for new goals. If empty, confirm completion. STOP. |

---

## 3. Plan (`phase: "planning"`)

### 3.1 Orient - Understand Before Acting

Read in this order to prevent anchoring bias:

1. **Project docs** - README, ROADMAP, architecture docs (big picture first)
2. **Inbox** - `.kramak/inbox/` for user goals, bugs, or direction changes (highest priority input)
3. **Prior state** - `state.lastAudit`, `state.failed` (learn from past failures)
4. **Live code** - Scan actual source files with grep/read (ground truth, never from memory)

> **If returning from a failed batch:** Check if the same problem failed 3+ times. If so, rethink the approach from first principles - do not retry the same strategy.

### 3.2 Formulate Work Items

Write Work Items to `.kramak/work-items/WI-NNN.md` with YAML frontmatter:

```yaml
---
id: WI-101
title: "Add user authentication endpoint"
batch: 1
status: queued
detail_tier: directed  # guided | directed | outcome
files_targeted:
  - "src/auth/tokens.ts"
  - "src/auth/routes.ts"
depends_on: []
acceptance_criteria:
  - "POST /api/login returns JWT on valid credentials"
  - "Invalid credentials return 401"
  - "npm test passes"
---
## Intent
[Why this change matters - what breaks or improves]

## Key Files
[Files the executor must read before starting, with brief context]

## Specification
[What to change - scaled by detail_tier, see Section 3.3]

## Constraints
[What NOT to do - boundaries and prohibitions]

## Verification
[Exact commands to run: build, test, lint]
```

**Numbering:** Batch 1 -> WI-101, WI-102... Batch 2 -> WI-201, WI-202...

### 3.3 Detail Scaling - The Goldilocks Rule

Match specification detail to risk. Over-specifying degrades model performance. Under-specifying causes 70-95% failure rates.

| Tier | When To Use | What To Specify |
|---|---|---|
| **Guided** | Schema changes, auth, payments, security, retried failures, 4+ interacting files | Read actual files first. Provide exact BEFORE/AFTER code changes. Zero ambiguity. |
| **Directed** | Features, APIs, integrations, refactors with clear patterns | Intent + target files + types/interfaces + constraints. Executor owns the HOW. |
| **Outcome** | Docs, config, styling, standalone components, tests | Goal + acceptance criteria only. Executor owns design and implementation. |

**Distribution guide:** Most WIs should be Directed. If more than 50% are Guided, you are over-specifying. Shift to Guided early in a project (architecture) and Outcome late (polish).

> **For Guided WIs only - Grounded Verification Protocol:**
> Before writing BEFORE/AFTER specs, you MUST grep or read the actual target file to verify your quoted code matches reality. Never quote code from memory.

### 3.4 Batch Sizing and Ordering

- **Size each WI** at 2 hours or less of human-equivalent work
- **Batch size:** 3-8 WIs (scale with confidence in the codebase)
- **Order by dependency:** Independent WIs first, dependent WIs after their prerequisites
- **Quality over volume:** 5 excellent WIs beats 15 vague ones

### 3.5 Multi-Agent Dispatch (Optional)

If your environment supports parallel execution (subagents, worktrees, multiple terminals):

1. Group WIs by file-independence - ensure `files_targeted` sets do not overlap
2. Set `state.concurrency.budget` greater than 1
3. Each agent gets an independent slice of the queue
4. Use `git worktree` or isolated branches for true parallel execution

### 3.6 Handoff

1. Update `state.json`:
   - Set `phase: "executing"`, populate `queue` with WI IDs, set `batchNumber`
2. Commit planning artifacts:
   `git add .kramak/` then `git commit -m "plan(batch-NN): [theme]"`
3. **Model-type consideration:** If you are an expensive reasoning model, recommend a fast/precise model for execution. Reasoning tokens are valuable for planning, not for mechanical code editing.

---

## 4. Execute (`phase: "executing"`)

### 4.1 Core Rules

1. **Verify before editing.** Read the actual file. Never code against memory or assumptions.
2. **Stay in scope.** Only modify files listed in the Work Item's `files_targeted`. If you must touch another file, note it for the next planning batch instead.
3. **Run verification after changes.** Execute the project's `toolchain.checkCommands`. Code that "looks right" but has not been tested does not count.
4. **Do not add unplanned features.** If you discover something needed, write a new WI for the next batch.
5. **Resolve from spec, not from the user.** The WI specification contains everything you need. Make decisions from the spec and codebase patterns.

### 4.2 Per Work Item

```
1. Read the WI specification completely
2. Read ALL files in files_targeted (establish ground truth)
3. Verify git working tree is clean
4. Execute by detail tier:
   Guided   -> Follow BEFORE/AFTER verbatim, zero deviation
   Directed -> Follow intent and constraints, you own the HOW
   Outcome  -> Follow acceptance criteria, you own the design
5. Run verification (checkCommands + WI-specific tests)
6. Scope check: git diff --name-only must match files_targeted
   -> If unlisted file touched: revert it with git checkout
7. Commit with conventional prefix: fix(scope) or feat(scope)
8. Update WI status to done, set completed_at timestamp
9. Update state.json: move WI from queue to completed, clear active
10. Pick next WI from queue, or transition to auditing when empty
```

### 4.3 Failure Handling

If a WI fails verification after genuine effort:

1. **Classify** the failure:
   - `code-drift` - target source changed since planning
   - `verification-fail` - build/test errors persist after retries
   - `scope-exceeded` - fix requires touching files outside `files_targeted`
   - `dependency-missing` - needs work from another WI first
   - `ambiguous-spec` - WI specification is unclear or contradictory

2. **Document** the diagnosis in the WI file (what failed, why, what should change)

3. **Revert** uncommitted changes: `git checkout -- .` and `git clean -fd`

4. **Update state:** Mark WI as `failed`, increment `metrics.consecutiveFailures`

5. **Retry budget:** 3 attempts per WI. If errors decrease each retry (12 then 4 then 1), extend to 5. If errors increase or oscillate, fail immediately.

### 4.4 Circuit Breaker

**If `consecutiveFailures >= 3`:**
- Set `phase: "escalated"`, `metrics.circuitBreakerTripped: true`
- Record what is failing and why in `state.escalation`
- **STOP.** Do not retry. The approach needs rethinking.

**Also trigger if:** The same error hash appears on 2 non-adjacent retry attempts (oscillation = wrong approach).

### 4.5 Session Health - Objective Degradation Signals

After completing 5+ WIs in one session, check these behavioral metrics:

| Signal | Healthy | Degraded |
|---|---|---|
| Verification retries per WI | Same or fewer than earlier WIs | More retries needed |
| Files touched vs `files_targeted` | Exact match | Touching unlisted files |
| Error trajectory across WIs | Flat or zero | Increasing per WI |

If degradation signals are present, **update state.json and start a fresh session.** Context fatigue causes silent quality decline that models cannot self-detect.

---

## 5. Audit (`phase: "auditing"`)

Best done in a fresh session for unbiased review:

1. **Run full verification:** All `toolchain.checkCommands` must pass
2. **Review completed WIs:** Read the actual code changes. Does each one match its WI intent?
3. **Scope verification:** `git diff --name-only` against the union of all WIs' `files_targeted`
4. **Fix issues directly:** Commit with `fix(audit): description` prefix
5. **Strategic concerns:** Write to `.kramak/inbox/` for the next planning cycle
6. **Update state:**
   - Set `state.lastAudit` with `batchNumber`, `verdict` (pass / pass-with-fixes), `timestamp`
   - Transition to `planning` (next batch) or `complete` (all goals met)

---

## 6. Resume Protocol

When returning to a project after interruption:

| Current Phase | Resume Action |
|---|---|
| `waiting` | Check if blockers are resolved. If yes, go to `executing` or `planning`. If no, show blockers, STOP. |
| `escalated` | Review `state.escalation`. Rethink approach. Clear breaker (`consecutiveFailures: 0`). Go to `planning`. |
| `complete` | Check `inbox/` for new goals. If found, go to `planning`. If empty, confirm completion, STOP. |
| `executing` (with active WI) | Check git status. If clean, resume WI. If dirty/corrupted, reset and restart WI. |

---

## 7. Process Governance

Before modifying any `.kramak/` governance file, answer these three questions:

1. **What specific failure does this change prevent?** (If you cannot name one, do not change it.)
2. **Does this help ALL types of work?** (Frontend, backend, infra, docs, tests - not just what you are doing now.)
3. **Could this change hurt a different type of work?** (A frontend-specific rule hurts backend batches.)

> This guard prevents recency-biased pipeline drift - the tendency to add rules that help your current task but harm future ones.