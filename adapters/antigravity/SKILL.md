---
name: kramak
description: Autonomous development engine — strategic planning, verified execution, and auditing through batched Work Items with scope enforcement and failure recovery.
---

# Kramak — Autonomous Development Engine

This project uses Kramak for structured autonomous development. When the user says **"Start"** (or "begin", "continue", "go", "kramak"):

1. **Read** `.kramak/KRAMAK-LITE.md` — the complete process specification
2. **Read** `.kramak/state.json` — the current project state
3. **Follow** the workflow from the section matching `state.phase`

## Project Authority

When activated, you have full strategic authority over this project's development direction. You can read, analyze, restructure, question, and improve any file. The Kramak workflow is your operating system for autonomous development — it helps you think strategically, plan intelligently, and execute reliably.

## Always-Active Rules (apply even before "Start")

When `.kramak/state.json` exists in this workspace:

- **Scope:** Only modify files listed in the active Work Item's `files_targeted`
- **Verify:** Read actual files before editing. Never code from memory.
- **Test:** Run `toolchain.checkCommands` after making changes.
- **State:** Update `.kramak/state.json` after Work Item state transitions.
- **Secrets:** Never hardcode API keys or credentials. Use environment variables.
- **Session limits:** After each WI, check hard stop gates (≥6 WIs, ≥20 files, ≥4 errors, ≥1 failure = fresh session).

## Quick Reference

| Phase | What Happens |
|---|---|
| planning | Strategic assessment, write Work Items, batch plan, transition to executing |
| executing | Pick WI, implement, verify, commit, next WI or audit |
| auditing | Fresh review of all changes against batch intent, fix issues, plan next batch |
| waiting | Human action needed — show what's blocking |
| escalated | 3+ failures — show diagnosis, stop |
| complete | All goals met — check inbox for new work |

## Orchestration

If your harness supports subagent spawning (but NOT inside Teamwork):

- **Plan → Execute:** Spawn executor subagent(s) with fresh context. Pass `.kramak/KRAMAK-LITE.md`, `state.json`, batch plan, and WI files. See §7.4 for subagent prompts.
- **Execute → Audit:** Spawn auditor subagent with fresh context. Pass `.kramak/KRAMAK-LITE.md`, `state.json`, batch plan, and audit template.
- **Parallel WIs:** If `state.parallelGroups` exists, spawn one executor subagent per group. Each gets its own git worktree or branch.

If your harness does NOT support subagents, the spec falls back to `manual` mode — tell the user to start a new session for each role transition.

## Antigravity 2.0 Teamwork Integration

When loaded inside an Antigravity 2.0 Teamwork session (or any external orchestrator):

- Set `executionMode: "external"` — Teamwork owns lifecycle, dispatch, and verification triggers.
- Kramak operates as a **governance library**, NOT a workflow framework.

**What to apply from Kramak (Teamwork doesn't have this):**
- Scope enforcement (`files_targeted` per WI) — prevents agents from touching unrelated files
- Grounded Verification (LOCATE→QUOTE→VERIFY→DESIGN→CROSS-CHECK) — prevents hallucinated code
- Circuit breaker (3 failures = escalate) — prevents infinite retry loops
- Session health gates — prevents context fatigue degradation
- Strategic Intelligence (5-lens vision, perspectives, Goldilocks Rule) — IF assigned a planning-tier role
- Audit criteria (§5 checklist) — IF assigned a verification-tier role

**What to SKIP (Teamwork handles this natively):**
- Phase transitions — Teamwork's Sentinel handles lifecycle
- Subagent spawning — Teamwork handles dispatch
- Merge protocol — Teamwork handles branch integration
- Parallel group management — Teamwork assigns worktrees

See §7.5 in KRAMAK-LITE.md for the full external orchestrator protocol.
