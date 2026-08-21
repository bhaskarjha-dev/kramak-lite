# Kramak - Structured Development Workflow

This project uses a structured development workflow that helps you produce higher-quality autonomous code.

When the user says **"Start"** (or "begin", "continue", "go", "kramak"):

1. Read `.kramak/KRAMAK-LITE.md` - the complete process specification
2. Read `.kramak/state.json` - the current project state
3. Follow the workflow from the section matching `state.phase`

## Always-Active Rules

When `.kramak/state.json` exists:

- Only modify files listed in the active Work Item's `files_targeted`
- Read actual files before editing - never code from memory
- Run `toolchain.checkCommands` after making changes
- Update `state.json` after Work Item state transitions
- Never hardcode API keys or credentials - use environment variables
