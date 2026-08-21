# Kramak Lite

**Structured autonomous development in a single file.**

Kramak Lite is a lightweight process control framework for AI coding agents. It turns unstructured "vibe coding" into a disciplined planning, executing, auditing lifecycle -- in a single Markdown file, with zero runtime dependencies.

## What It Does

Kramak Lite helps you produce higher-quality autonomous code by preventing the 5 most common failures:

| Failure Mode | How Kramak Prevents It |
|---|---|
| **Scope drift** | `files_targeted` boundary on every Work Item + pre-execution scope intercept |
| **Hallucinated references** | 5-step Grounded Verification: LOCATE, QUOTE, VERIFY, DESIGN, CROSS-CHECK |
| **Context fatigue** | Hard stop gates (6 WIs, 20 files, 4 errors = fresh session) + session weight matrix |
| **Infinite fix loops** | Circuit breaker: 3 consecutive failures or oscillation detection = escalate |
| **Under/over-specification** | Goldilocks Rule: Guided / Directed / Outcome tiers with distribution guidance |

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
2. Bootstrap the project (detect toolchain, init git if needed, create state)
3. Plan a batch of Work Items with product phase awareness (BUILD/SHIP/ITERATE)
4. Execute them with scope enforcement, verification, and neighborhood cleanup
5. Audit the results with execution-grounded review
6. Plan the next batch (or mark the project complete)

## How It Works

```
              +----------+
              | PLANNING  | <- Understand project, write Work Items
              +-----+-----+
                    |
              +-----v-----+
              | EXECUTING  | <- Implement WIs with scope check + testing
              +-----+-----+
                    |
              +-----v-----+
              | AUDITING   | <- Verify all changes, fix issues
              +-----+-----+
                    |
              +-----v-----+
         +----| COMPLETE?  |----+
         | No +------------+ Yes|
         v                      v
    Back to PLANNING         Done!
```

State is tracked in `.kramak/state.json`. Work Items live in `.kramak/work-items/`. User goals go in `.kramak/inbox/`. Everything is plain Markdown and JSON -- no runtime, no CLI required.

## Project Structure

```
.kramak/
+-- KRAMAK-LITE.md              <- The spec (single file, ~21KB)
+-- state.json                  <- Current state (auto-created)
+-- schemas/
|   +-- state.schema.json       <- State validation schema
|   +-- work-item.schema.json   <- Work Item validation schema
+-- work-items/                 <- Work Items (auto-populated by planner)
+-- inbox/                      <- User goals and direction (you write here)
+-- templates/
    +-- WORK-ITEM.template.md   <- WI template reference

docs/
+-- GETTING-STARTED.md          <- Setup guide and quickstart
+-- ARCHITECTURE.md             <- Design decisions, token analysis, IDE compatibility
+-- FULL-KRAMAK-MAPPING.md      <- 176-rule coverage map (Lite vs Full Kramak)

adapters/                        <- IDE-specific adapters
+-- antigravity/SKILL.md
+-- claude-code/CLAUDE.md
+-- cursor/.cursorrules
+-- generic/AGENTS.md

CHANGELOG.md                     <- Version history with rationale
```

## Kramak Lite vs Kramak (Full)

| Aspect | Kramak Lite | Kramak Full |
|---|---|---|
| **Spec size** | ~21KB (1 file) | ~191KB (20 files) |
| **Rule coverage** | ~92% of all rules (~95% of non-CLI rules) | 176 comprehensive rules |
| **States** | 6 (plan/exec/audit/wait/escalate/complete) | 9 (adds dispatch/merge_queue/bootstrap) |
| **Multi-agent** | Supported (optional) | Supported (with worktree isolation) |
| **Product lifecycle** | BUILD/SHIP/ITERATE priorities | Full 5-lens strategic vision |
| **Failure recovery** | 6-category taxonomy + tier elevation + recovery shortcuts | Full decision tree + ODC/MAST crosswalk |
| **Session management** | Hard stop gates + session weight matrix | Behavioral + quantitative signals |
| **Canary Gate** | Dropped (requires CLI enforcement) | Full 5-challenge battery |
| **WAL writes** | Dropped (requires CLI enforcement) | Two-phase atomic write protocol |
| **IDE compatibility** | Any IDE, any model tier | Best with frontier models |
| **Runtime deps** | Zero | Zero (but kramak-cli recommended) |

**Kramak Lite keeps the value, drops the ceremony.** Features that require programmatic enforcement (WAL, Canary Gate, formal ledger) are deferred to [kramak-cli](https://github.com/bhaskarjha-dev/kramak-cli).

## Key Concepts

### Work Items
The atomic unit of work. Each WI specifies what to change, which files to touch, and how to verify. See `.kramak/templates/WORK-ITEM.template.md` for the format.

### Goldilocks Rule (Detail Scaling)
- **Guided** -- high-risk changes get exact BEFORE/AFTER recipes with 5-step verification
- **Directed** -- standard changes get intent + constraints (most WIs should be this)
- **Outcome** -- low-risk changes get acceptance criteria only

### Product Phase (BUILD / SHIP / ITERATE)
Determines what kind of work to prioritize. BUILD focuses on architecture and features. SHIP focuses on deployment and security. ITERATE focuses on production issues and improvements.

### Circuit Breaker
3 consecutive failures or oscillation detection = stop and escalate. Prevents infinite retry loops.

### Hard Stop Gates
Quantitative session limits: 6+ WIs, 20+ files, 4+ errors corrected, or 1+ failed WI triggers a fresh session. Prevents context fatigue.

### Session Health Monitoring
After hitting any hard stop gate, objective signals determine whether to continue or start fresh. Models cannot self-detect quality degradation -- the gates enforce it.

## Documentation

| Document | Purpose |
|---|---|
| [Getting Started](docs/GETTING-STARTED.md) | Setup guide and quickstart |
| [Architecture](docs/ARCHITECTURE.md) | Design decisions, single-file rationale, IDE compatibility strategy, token analysis |
| [Full Kramak Mapping](docs/FULL-KRAMAK-MAPPING.md) | Complete rule-by-rule coverage map (176 rules) |
| [Changelog](CHANGELOG.md) | Version history with rationale for every change |

## Requirements

- An AI coding agent with file read/write and terminal access
- That's it. No Node.js, no Python, no package manager. Git will be initialized automatically if missing.

## License

Apache 2.0

## Links

- [Kramak (Full)](https://github.com/bhaskarjha-dev/kramak) -- The comprehensive specification
- [kramak-cli](https://github.com/bhaskarjha-dev/kramak-cli) -- Programmatic enforcement layer
