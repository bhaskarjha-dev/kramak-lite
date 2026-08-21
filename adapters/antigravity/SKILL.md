---
name: kramak
description: Structured autonomous development workflow. Activates when the user says "Start" to govern planning, execution, and auditing of code changes through batched Work Items with scope enforcement and failure recovery.
---

# Kramak — Autonomous Development Workflow

When the user says **"Start"** (or "begin", "continue", "go", "kramak"), activate the Kramak development workflow:

1. **Read** .kramak/KRAMAK-LITE.md — this is the complete process specification
2. **Read** .kramak/state.json — this is the current project state
3. **Follow** the workflow described in KRAMAK-LITE.md from the appropriate section based on state.phase

## Always-Active Rules (apply even before "Start")

When .kramak/state.json exists in this workspace:

- **Scope:** Only modify files listed in the active Work Item's iles_targeted
- **Verify:** Read actual files before editing. Never code from memory.
- **Test:** Run 	oolchain.checkCommands after making changes.
- **State:** Update .kramak/state.json after Work Item state transitions.

## Quick Reference

| Phase | What Happens |
|---|---|
| planning | Read project → Write Work Items → Transition to executing |
| executing | Pick WI → Implement → Verify → Commit → Next WI or audit |
| uditing | Fresh review of all changes → Fix issues → Plan next batch |
| waiting | Human action needed — show what's blocking |
| escalated | 3+ failures — show diagnosis, stop |
| complete | All goals met — check inbox for new work |
