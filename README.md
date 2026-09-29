<div align="center">

<img src="docs/assets/logo.png" alt="Kramak Lite" width="140" />

# Kramak Lite

**Turn vibe coding into verified engineering.**

An autonomous development engine for AI coding agents.
Zero dependencies. Any IDE. Any model.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Spec Version](https://img.shields.io/badge/Spec-v0.1.0--dev-7C3AED.svg)](.kramak/KRAMAK-LITE.md)
[![Dependencies: Zero Runtime](https://img.shields.io/badge/Runtime_Dependencies-Zero-brightgreen.svg)](.kramak/KRAMAK-LITE.md)
[![Full Kramak](https://img.shields.io/badge/Full_Kramak-Available-lightgrey.svg)](https://github.com/bhaskarjha-dev/kramak)

</div>

---

## The Problem

AI coding agents are powerful but unreliable. Without guardrails, they:

| Failure | What Happens | How Kramak Prevents It |
|---|---|---|
| **Scope drift** | Agent touches 30 files when the task needed 3 | `files_targeted` boundary per Work Item + pre-edit intercept |
| **Hallucinated code** | Agent writes code based on APIs that don't exist | 5-step Grounded Verification: LOCATE → QUOTE → VERIFY → DESIGN → CROSS-CHECK |
| **Silent degradation** | Quality drops after Work Item #5 but the agent can't tell | Hard stop gates: ≥6 WIs, ≥20 files, ≥4 errors = mandatory fresh session |
| **Infinite retry loops** | Agent retries the same broken fix 20 times | Circuit breaker: 3 consecutive failures or oscillation = stop and escalate |
| **Untested output** | "Looks right" but was never actually run | Mandatory verification: `checkCommands` run after every change |

**But guardrails alone aren't enough.** An agent that follows rules mechanically is just a task executor. Kramak Lite gives the agent **strategic intelligence** — the ability to think like a CTO, assess the project from multiple perspectives, plan dynamically, and adapt.

Kramak Lite does all this. In one Markdown file (~56KB). With zero runtime dependencies.

---

## Quick Start (2 Minutes)

### 1. Copy `.kramak/` into your project

```bash
git clone https://github.com/bhaskarjha-dev/kramak-lite.git
cp -r kramak-lite/.kramak/ your-project/.kramak/
```

> **Why `.kramak` and not `.kramak-lite`?** The `.kramak` directory is the ecosystem namespace — like `.git` or `.vscode`. The file inside (`KRAMAK-LITE.md`) identifies which version you're running. Upgrading to full Kramak later is seamless: just replace the directory contents. [More in FAQ →](#faq)

### 2. Add the adapter

Copy the universal adapter to your project root:

```bash
cp kramak-lite/adapters/AGENTS.md ./AGENTS.md
```

That's it. `AGENTS.md` is the [universal standard](https://agents.md) — it works natively with Claude Code, Cursor, Antigravity, Windsurf, Codex, Cline, Roo Code, Devin, GitHub Copilot, Zed, Amp, Warp, and every other modern AI coding harness.

<details>
<summary><strong>Cursor users (optional enhancement)</strong></summary>

For Cursor-specific metadata (glob targeting, priority over AGENTS.md):

```bash
mkdir -p .cursor/rules/
cp kramak-lite/adapters/cursor/kramak.mdc .cursor/rules/kramak.mdc
```

This gives Kramak higher priority in Cursor's rule hierarchy. The universal `AGENTS.md` also works without this step.

</details>

<details>
<summary><strong>Already have an AGENTS.md?</strong></summary>

Append instead of overwriting:

```bash
echo "" >> ./AGENTS.md
cat kramak-lite/adapters/AGENTS.md >> ./AGENTS.md
```

Kramak's adapter is a small section (~65 lines) that cooperates with your existing rules.

</details>

### 3. Say **"Start"**

Open your AI agent and type: **Start**

That's it. The agent will assess the project strategically, plan Work Items from the right perspective, execute them with scope enforcement, audit the results, and plan the next batch — all autonomously.

---

## How It Works

```
         ┌──────────┐
         │ PLANNING  │ ← Strategic vision, perspective selection, batch plan
         └─────┬─────┘
               │
         ┌─────▼─────┐
         │ EXECUTING  │ ← Implement WIs with scope check + testing
         └─────┬─────┘
               │
         ┌─────▼─────┐
         │ AUDITING   │ ← Review all changes with fresh eyes
         └─────┬─────┘
               │
         ┌─────▼─────┐
    ┌────│ COMPLETE?  │────┐
    │ No └────────────┘ Yes│
    ▼                      ▼
  Back to PLANNING       Done!
```

**State** is tracked in `.kramak/state.json`.
**Batch plans** live in `.kramak/plans/`.
**Work Items** live in `.kramak/work-items/`.
**User goals & feedback** go in `.kramak/inbox/INBOX.md`.
**Cross-session history** is logged in `.kramak/SESSION-LOG.md`.
Everything is plain Markdown and JSON — no runtime, no CLI, no magic.

**Execution modes:** Role transitions happen via manual sessions (default), orchestrator-spawned subagents, parallel agent threads, or external frameworks like Antigravity Teamwork — the spec auto-detects your environment. In external mode, Kramak operates as a governance library (quality rules without lifecycle ownership). See §7 of the spec.

---

## Key Concepts

### Strategic Intelligence (What Makes This an Engine, Not a Checklist)

The planner doesn't just follow a roadmap mechanically. It:

1. **Assesses strategically** — 5-lens vision system (Quality, User Journey, Competitive, Innovation, Architecture) triggers at milestones or periodic intervals
2. **Thinks meta-cognitively** — PERCEIVE → REASON → DECIDE loop: "What's the biggest risk? Biggest opportunity? What's been neglected?"
3. **Selects perspectives** — Reasons into the right viewpoint (Solution Architect, UX Designer, CEO, Security Engineer, etc.) rather than defaulting to "developer"
4. **Prioritizes by product phase** — BUILD/SHIP/ITERATE priority ladders determine what work matters most right now
5. **Sizes dynamically** — Batch size is driven by planning quality, not fixed numbers

### Work Items
The atomic unit of work. Each WI specifies what to change, which files to touch, and how to verify. Created during planning, executed one by one.

### Goldilocks Rule (Detail Scaling)
Not all changes need the same level of specification:

| Tier | When to Use | What the Agent Gets |
|---|---|---|
| **Guided** | High-risk (auth, payments, schemas) | Exact BEFORE/AFTER code blocks + 5-step verification |
| **Directed** | Standard changes (most WIs) | Intent + target files + constraints — agent owns the HOW |
| **Outcome** | Low-risk (docs, config, styling) | Acceptance criteria only — agent owns the design |

### Circuit Breaker
3 consecutive failures or oscillation detected → agent stops and escalates. No more infinite retry loops.

### Hard Stop Gates
Quantitative session limits that prevent context fatigue:
- **≥6 WIs completed** → fresh session
- **≥20 files modified** → fresh session
- **≥4 errors corrected** → fresh session
- **≥1 WI failed** → fresh session

Models cannot self-detect quality degradation — these gates enforce the pause.

### Product Phase (BUILD / SHIP / ITERATE)
Determines what kind of work to prioritize. BUILD focuses on architecture and features. SHIP focuses on deployment and security. ITERATE focuses on production issues and improvements. Each phase has an explicit priority ladder.

---

## What's Inside

```
your-project/
├── .kramak/
│   ├── KRAMAK-LITE.md              ← The spec (single file, ~56KB)
│   ├── state.json                  ← Current state (auto-created at runtime)
│   ├── SESSION-LOG.md              ← Cross-session history (created at runtime)
│   ├── HUMAN-TASKS.md              ← Async human blockers (created at runtime)
│   ├── schemas/
│   │   ├── state.schema.json       ← State validation schema
│   │   └── work-item.schema.json   ← Work Item validation schema
│   ├── plans/                      ← Batch plans & audit reports (created at runtime)
│   ├── work-items/                 ← Work Items (created at runtime by planner)
│   ├── inbox/
│   │   └── INBOX.md                ← User goals and direction (you write here)
│   ├── ledger/                     ← Governance self-modification log
│   └── templates/                  ← Production templates
│       ├── state.template.json     ← Initial state bootstrap template
│       ├── conventions.template.md ← Project conventions template (agent orientation)
│       ├── session-log.md          ← Universal session log template
│       ├── batch-plan.md           ← Batch plan template
│       ├── human-tasks.md          ← Human tasks template
│       ├── audit-report.md         ← Audit report template
│       ├── retrospective.md        ← Batch learning template
│       ├── WORK-ITEM.template.md   ← Master WI template
│       ├── work-item-guided.md     ← 🔴 Guided tier template
│       ├── work-item-directed.md   ← 🟡 Directed tier template
│       └── work-item-outcome.md    ← 🟢 Outcome tier template
└── ...your code...
```

---

## Kramak Lite vs Full Kramak

| Aspect | Kramak Lite | Kramak (Full) |
|---|---|---|
| **Spec size** | ~56KB (1 file) | ~191KB (20 files) |
| **Rule coverage** | 173 of 173 enforceable rules — 100% (176 total minus 3 CLI-only) | 176 rules (includes CLI-only guards) |
| **Strategic intelligence** | 5-lens vision + PERCEIVE→REASON→DECIDE + perspectives | Full 5-lens + multi-cycle perspective tracking |
| **States** | 6 (plan/exec/audit/wait/escalate/complete) | 9 (adds dispatch/merge_queue/bootstrap) |
| **Cross-session log** | Unified SESSION-LOG.md (Plan/Exec/Audit) | PLANNING-LOG + PROGRESS.md + RETRO |
| **Multi-agent** | Supported (optional) | Supported (with worktree isolation) |
| **Product lifecycle** | BUILD/SHIP/ITERATE with priority ladders | Full 5-lens strategic vision + GROWTH phase |
| **Failure recovery** | 6-category taxonomy + circuit breaker + recovery shortcuts | Full decision tree + ODC/MAST crosswalk |
| **Session management** | Hard stop gates + session weight + WAL atomic writes | Behavioral + quantitative + WAL-based recovery |
| **Capability gate** | Project-grounded inline verification | Full 5-challenge Canary battery |
| **IDE compatibility** | Any IDE, any model tier | Best with frontier models |
| **Runtime deps** | Zero | Zero |

**Kramak Lite is the autonomous engine. Full Kramak adds depth.** The full version provides extended on-demand modules, formal ODC/MAST failure crosswalks, deep diagnostic trees, and the 5-challenge Canary Capability Battery for rigorous model qualification.

---

## Documentation

| Document | What You'll Learn |
|---|---|
| **[Getting Started](docs/GETTING-STARTED.md)** | Step-by-step setup for every scenario (new project, existing project, existing AI config) |
| **[Architecture](docs/ARCHITECTURE.md)** | Why single-file, IDE compatibility strategy, token analysis, naming decisions |
| **[Competitive Comparison](docs/COMPARISON.md)** | Objective 21-tool benchmark matrix and head-to-head architectural analysis |
| **[Roadmap](docs/ROADMAP.md)** | Provisional candidate backlog for open distribution standards, backstops, and benchmarks |
| **[Full Kramak Mapping](docs/FULL-KRAMAK-MAPPING.md)** | Rule-by-rule coverage map of all 176 rules |
| **[Changelog](CHANGELOG.md)** | Version history with rationale for every change |

---

## FAQ

<details>
<summary><strong>Why is the directory called <code>.kramak</code> and not <code>.kramak-lite</code>?</strong></summary>

The `.kramak` directory is the **ecosystem namespace** for Kramak — like `.git` is for Git regardless of version, or `.vscode` is for VS Code. The file inside (`KRAMAK-LITE.md` vs `ROUTER.md`) identifies which edition you're running.

This design means:
- **Upgrading to full Kramak** later doesn't require renaming directories or updating adapter paths
- **All adapters** work with both Lite and Full because they reference `.kramak/`

</details>

<details>
<summary><strong>I already have a CLAUDE.md / AGENTS.md / GEMINI.md. Will this overwrite it?</strong></summary>

**No, if you follow the instructions.** The Quick Start includes explicit "append" commands for each IDE. Never `cp` over an existing config file — always `cat >> ` to append.

The Kramak adapter is a small section (~65 lines) that tells your agent how to find and follow `KRAMAK-LITE.md`. It cooperates with your existing rules — it doesn't replace them.

</details>

<details>
<summary><strong>Can I use Kramak Lite with multiple IDEs simultaneously?</strong></summary>

Yes. `AGENTS.md` is the [universal standard](https://agents.md) — every modern harness reads it natively. Just copy `AGENTS.md` to your project root once. For Cursor, you can optionally also install `kramak.mdc` in `.cursor/rules/` for higher priority. All adapters point to the same `.kramak/KRAMAK-LITE.md`.

</details>

<details>
<summary><strong>I'm using full Kramak and want to switch to Lite. How?</strong></summary>

1. Back up your current `.kramak/state.json`
2. Replace your `.kramak/` contents with Kramak Lite's `.kramak/`
3. Copy your `state.json` back (the core fields are compatible)
4. Update your adapter if needed (they should work as-is)

Note: Full Kramak's extra phases (`dispatch`, `merge_queue`, `bootstrap`) and `GROWTH` product phase don't exist in Lite. If your `state.json` references these, update `phase` to the nearest Lite equivalent.

</details>

<details>
<summary><strong>Which AI models work best with Kramak Lite?</strong></summary>

Kramak Lite works with any model, but compliance varies by model class (as of August 2026):

| Model Class | Examples | Planning | Execution | Audit | Overall |
|---|---|---|---|---|---|
| Frontier reasoning | Gemini 2.5 Pro, Claude Opus 4 | Excellent | Excellent | Excellent | **Excellent** |
| Strong mid-tier | Claude Sonnet 4, GPT-4o | Good | Good | Adequate | **Strong** |
| Fast / mini | Gemini Flash, GPT-4o-mini | Adequate | May skip steps | May rubber-stamp | **Basic** |

All models benefit from the framework. Stronger models follow it more completely. Model names and versions change rapidly — test with your current model.

</details>

<details>
<summary><strong>What if my agent ignores the Kramak rules?</strong></summary>

This happens occasionally, especially with smaller models. Try:
1. **Restart the session** — say "Start" in a fresh conversation
2. **Check the adapter** — make sure it's in the right location for your IDE
3. **Be explicit** — say "Follow the Kramak workflow in `.kramak/KRAMAK-LITE.md`"
4. **Use a more capable model** — frontier models comply more consistently

For stronger enforcement, use a more capable model or consider upgrading to [full Kramak](https://github.com/bhaskarjha-dev/kramak).

</details>

---

## Requirements

- **Git** — used for scope tracking, branching, crash recovery, and commit history
- An AI coding agent with file read/write and terminal access
- That's it. No Node.js, no Python, no package manager.

## License

MIT

## Links

- [Kramak (Full)](https://github.com/bhaskarjha-dev/kramak) — The comprehensive 176-rule specification
