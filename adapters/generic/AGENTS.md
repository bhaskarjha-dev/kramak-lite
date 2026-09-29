# Kramak — Autonomous Development Engine

This project uses Kramak for structured autonomous development.

When the user says **"Start"** (or "begin", "continue", "go", "kramak"):

1. Read `.kramak/KRAMAK-LITE.md` — the complete process specification
2. Read `.kramak/state.json` — the current project state
3. Follow the workflow from the section matching `state.phase`

## Project Authority

When activated, you have full strategic authority over this project's development direction. You can read, analyze, restructure, question, and improve any file. The Kramak workflow is your operating system for autonomous development — it helps you think strategically, plan intelligently, and execute reliably.

## Always-Active Rules

When `.kramak/state.json` exists:

- Only modify files listed in the active Work Item's `files_targeted`
- Read actual files before editing — never code from memory
- Run `toolchain.checkCommands` after making changes
- Update `state.json` after Work Item state transitions
- Never hardcode API keys or credentials — use environment variables
- After each WI, check hard stop gates (≥6 WIs, ≥20 files, ≥4 errors, ≥1 failure = fresh session)

## Quick Reference

| Phase | What Happens |
|---|---|
| planning | Strategic assessment, write Work Items, batch plan, transition to executing |
| executing | Pick WI, implement, verify, commit, next WI or audit |
| auditing | Fresh review of all changes against batch intent, fix issues, plan next batch |
| waiting | Human action needed — show what's blocking |
| escalated | 3+ failures — show diagnosis, stop |
| complete | All goals met — check inbox for new work |

## Orchestration (v3.0.0)

If your harness supports subagent spawning:

- **Plan → Execute:** Spawn executor subagent(s) with fresh context. Pass `.kramak/KRAMAK-LITE.md`, `state.json`, batch plan, and WI files. See §7.4 for subagent prompts.
- **Execute → Audit:** Spawn auditor subagent with fresh context. Pass `.kramak/KRAMAK-LITE.md`, `state.json`, batch plan, and audit template.
- **Parallel WIs:** If `state.parallelGroups` exists, spawn one executor subagent per group. Each gets its own git worktree or branch.

If your harness does NOT support subagents, the spec falls back to `manual` mode — tell the user to start a new session for each role transition.
