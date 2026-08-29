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
