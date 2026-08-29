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
