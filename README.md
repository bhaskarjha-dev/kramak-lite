# Kramak Lite

**Structured autonomous development in a single file.**

Kramak Lite is a lightweight process control framework for AI coding agents. It turns unstructured "vibe coding" into a disciplined planning → executing → auditing lifecycle — in ~7KB of Markdown, with zero runtime dependencies.

## What It Does

Kramak Lite prevents the 5 most common autonomous coding failures:

| Failure Mode | How Kramak Prevents It |
|---|---|
| **Scope drift** | `files_targeted` boundary on every Work Item |
| **Hallucinated references** | Grounded Verification: must read files before editing |
| **Context fatigue** | Objective degradation signals + session handoff protocol |
| **Infinite fix loops** | Circuit breaker: 3 consecutive failures → escalate |
| **Under/over-specification** | Goldilocks Rule: 🔴 Guided / 🟡 Directed / 🟢 Outcome tiers |

## Quick Start (2 Minutes)

### 1. Copy the `.kramak/` directory into your project

```bash
# Clone this repo
git clone https://github.com/bhaskarjha-dev/kramak-lite.git

# Copy .kramak/ into your project
cp -r kramak-lite/.kramak/ /path/to/your/project/.kramak/
```

### 2. Install the adapter for your IDE

| IDE | Copy This File | To This Location |
|---|---|---|
| **Antigravity** | `adapters/antigravity/SKILL.md` | `.agents/skills/kramak/SKILL.md` |
| **Claude Code** | `adapters/claude-code/CLAUDE.md` | `CLAUDE.md` (project root) |
| **Cursor** | `adapters/cursor/.cursorrules` | `.cursor/rules/kramak.mdc` |
| **Generic** | `adapters/generic/AGENTS.md` | `AGENTS.md` or `GEMINI.md` (project root) |

### 3. Say "Start"

Tell your AI agent: **"Start"**

The agent will:
1. Read `KRAMAK-LITE.md` and `state.json`
2. Bootstrap the project (detect toolchain, create state)
3. Plan a batch of Work Items
4. Execute them with scope enforcement and verification
5. Audit the results

## How It Works

```
              ┌──────────┐
              │ PLANNING  │ ← Understand project, write Work Items
              └─────┬─────┘
                    │
              ┌─────▼─────┐
              │ EXECUTING  │ ← Implement WIs with scope check + testing
              └─────┬─────┘
                    │
              ┌─────▼─────┐
              │ AUDITING   │ ← Verify all changes, fix issues
              └─────┬─────┘
                    │
              ┌─────▼─────┐
         ┌────│  COMPLETE? │────┐
         │ No └────────────┘ Yes│
         ▼                      ▼
    Back to PLANNING         Done!
```

State is tracked in `.kramak/state.json`. Work Items live in `.kramak/work-items/`. User goals go in `.kramak/inbox/`. Everything is plain Markdown and JSON — no runtime, no CLI required.

## Project Structure

```
.kramak/
├── KRAMAK-LITE.md              ← The spec (single file, ~7KB)
├── state.json                  ← Current state (auto-created)
├── schemas/
│   ├── state.schema.json       ← State validation schema
│   └── work-item.schema.json   ← Work Item validation schema
├── work-items/                 ← Work Items (auto-populated by planner)
├── inbox/                      ← User goals and direction (you write here)
└── templates/
    └── WORK-ITEM.template.md   ← WI template reference
```

## Kramak Lite vs Kramak (Full)

| Aspect | Kramak Lite | Kramak Full |
|---|---|---|
| **Spec size** | ~7KB (1 file) | ~191KB (20 files) |
| **States** | 6 (plan/exec/audit/wait/escalate/complete) | 9 (adds dispatch/merge_queue/bootstrap) |
| **Rules** | ~30 essential | 176 comprehensive |
| **Multi-agent** | Supported (optional) | Supported (with worktree isolation) |
| **Canary Gate** | Dropped (requires CLI enforcement) | Full 5-challenge battery |
| **WAL writes** | Dropped (requires CLI enforcement) | Two-phase atomic write protocol |
| **Formal ledger** | Dropped (requires CLI enforcement) | Append-only JSONL audit trail |
| **IDE compatibility** | Any IDE, any model tier | Best with frontier models |
| **Runtime deps** | Zero | Zero (but kramak-cli recommended) |

**Kramak Lite keeps the value, drops the ceremony.** Features that require programmatic enforcement (WAL, Canary Gate, formal ledger) are deferred to [kramak-cli](https://github.com/bhaskarjha-dev/kramak-cli).

## Key Concepts

### Work Items
The atomic unit of work. Each WI specifies what to change, which files to touch, and how to verify. See `.kramak/templates/WORK-ITEM.template.md` for the format.

### Goldilocks Rule (Detail Scaling)
- 🔴 **Guided** — high-risk changes get exact BEFORE/AFTER recipes
- 🟡 **Directed** — standard changes get intent + constraints
- 🟢 **Outcome** — low-risk changes get acceptance criteria only

### Circuit Breaker
3 consecutive failures → stop and escalate. Prevents infinite retry loops.

### Session Health Monitoring
After 5+ WIs, objective signals (retry count, scope creep, error trajectory) determine whether to continue or start fresh.

## Requirements

- Git initialized in your project
- An AI coding agent with file read/write and terminal access
- That's it. No Node.js, no Python, no package manager.

## License

Apache 2.0

## Links

- [Kramak (Full)](https://github.com/bhaskarjha-dev/kramak) — The comprehensive specification
- [kramak-cli](https://github.com/bhaskarjha-dev/kramak-cli) — Programmatic enforcement layer
