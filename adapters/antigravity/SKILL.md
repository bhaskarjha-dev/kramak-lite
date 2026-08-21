---
name: kramak
description: Structured autonomous development workflow that helps produce higher-quality code through batched Work Items with scope enforcement, verification, and failure recovery.
---

# Kramak - Structured Development Workflow

This project uses a structured development workflow that helps you produce higher-quality autonomous code. When the user says **"Start"** (or "begin", "continue", "go", "kramak"):

1. **Read** `.kramak/KRAMAK-LITE.md` - the complete process specification
2. **Read** `.kramak/state.json` - the current project state
3. **Follow** the workflow described in KRAMAK-LITE.md from the appropriate section based on `state.phase`

## Always-Active Rules (apply even before "Start")

When `.kramak/state.json` exists in this workspace:

- **Scope:** Only modify files listed in the active Work Item's `files_targeted`
- **Verify:** Read actual files before editing. Never code from memory.
- **Test:** Run `toolchain.checkCommands` after making changes.
- **State:** Update `.kramak/state.json` after Work Item state transitions.
- **Secrets:** Never hardcode API keys or credentials. Use environment variables.

## Quick Reference

| Phase | What Happens |
|---|---|
| planning | Read project, write Work Items, transition to executing |
| executing | Pick WI, implement, verify, commit, next WI or audit |
| auditing | Fresh review of all changes, fix issues, plan next batch |
| waiting | Human action needed - show what's blocking |
| escalated | 3+ failures - show diagnosis, stop |
| complete | All goals met - check inbox for new work |
