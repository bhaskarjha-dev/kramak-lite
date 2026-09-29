# Getting Started with Kramak Lite

> **Time to install:** ~2 minutes · **Time to first result:** ~5 minutes · **Prerequisites:** Any AI coding agent with file/terminal access

---

## Install

### Step 1: Add Kramak Lite to Your Project

Copy the `.kramak/` directory into your project root:

```bash
# Option A: Clone and copy
git clone https://github.com/bhaskarjha-dev/kramak-lite.git
cp -r kramak-lite/.kramak/ your-project/.kramak/

# Option B: If you already have the repo locally
cp -r /path/to/kramak-lite/.kramak/ /path/to/your-project/.kramak/
```

Your project should now have:
```
your-project/
├── .kramak/
│   ├── KRAMAK-LITE.md        ← The spec (this is the only file the agent needs)
│   ├── schemas/              ← Validation schemas (state & work-item)
│   ├── work-items/           ← Agent writes Work Items here
│   ├── inbox/                ← You write goals & direction here (INBOX.md)
│   ├── ledger/               ← Governance self-modification log
│   ├── plans/                ← Batch plans and audit reports
│   └── templates/            ← Template format references
├── src/                      ← Your existing code (untouched)
├── package.json              ← Your existing config (untouched)
└── ...
```

### Step 2: Add the Adapter

Copy the universal adapter to your project root:

```bash
cp /path/to/kramak-lite/adapters/AGENTS.md ./AGENTS.md
```

`AGENTS.md` is the [universal standard](https://agents.md) — it works natively with Claude Code, Cursor, Antigravity, Windsurf, Codex, Cline, Roo Code, Devin, GitHub Copilot, Zed, Amp, Warp, and every other modern AI coding harness.

> **Already have an AGENTS.md?** Append instead of overwriting:
> ```bash
> echo "" >> ./AGENTS.md
> cat /path/to/kramak-lite/adapters/AGENTS.md >> ./AGENTS.md
> ```
> Kramak's adapter is ~70 lines that cooperate with your existing rules.

#### Cursor Users (Optional Enhancement)

For Cursor-specific metadata (glob targeting, `alwaysApply` priority):

```bash
mkdir -p .cursor/rules/
cp /path/to/kramak-lite/adapters/cursor/kramak.mdc .cursor/rules/kramak.mdc
```

> This gives Kramak higher priority in Cursor's rule hierarchy. The universal `AGENTS.md` also works without this step.

#### Using Multiple IDEs?

Just use `AGENTS.md` — every modern harness reads it natively. For Cursor, you can optionally also install `kramak.mdc` for higher priority. All adapters point to the same `.kramak/KRAMAK-LITE.md`.

### Step 3: Configure `.gitignore`

Add one line to your project's `.gitignore`:

```gitignore
# Kramak WAL recovery file — always ephemeral
.kramak/state.json.tmp
```

**That's the only required entry.** Everything else in `.kramak/` — state, work items, plans, session logs, audit reports — is your development process record. Tracking it means:
- Clone the repo on any machine and resume instantly
- Team members see what was planned, executed, and audited
- Code reviewers get the strategic context behind changes
- Full crash/machine-death recovery via `git clone`

<details>
<summary><strong>Optional: lighter git footprint</strong></summary>

If you prefer a cleaner git history and don't need full process archaeology, you can also ignore the verbose runtime artifacts:

```gitignore
# Kramak — lighter footprint (keeps state + session log, ignores WI/plan details)
.kramak/state.json.tmp
.kramak/work-items/*.md
!.kramak/work-items/.gitkeep
.kramak/plans/*.md
!.kramak/plans/.gitkeep
```

> **Note:** Ignoring work items and plans means you lose the detailed planning/execution record. `SESSION-LOG.md` still provides a narrative summary.

</details>

### Step 4: (Optional) Write a Goal

Tell the agent what to build by adding a goal to `.kramak/inbox/INBOX.md`:

```markdown
## Unprocessed

### direction: Build User Management REST API
Build a REST API for user management with:
- User registration and login (JWT auth)
- Profile CRUD operations
- Role-based access control
- PostgreSQL database with Prisma ORM
```

If you skip this step, the agent will analyze your existing codebase and plan improvements based on what it finds.

### Step 5: Say **"Start"**

Open your AI agent and type: **Start**

The agent will:
1. Read the Kramak spec and detect your project's toolchain
2. Initialize git if not already present
3. Determine the product phase (BUILD/SHIP/ITERATE) for priority guidance
4. Plan a batch of Work Items based on your goal or codebase analysis
5. Execute them one by one with scope enforcement and verification
6. Audit the results with fresh-eyes review
7. Plan the next batch or mark the project complete

### Multi-Agent / Orchestrated Execution

If your IDE supports subagent spawning (Antigravity, Claude Code Task tool, etc.), Kramak Lite auto-detects this and uses it:

| Mode | What Happens | When It's Used |
|---|---|---|
| `manual` | User starts new sessions for each role (Plan → Execute → Audit) | No subagent capability |
| `orchestrated` | Planner auto-spawns executor and auditor subagents | Harness supports subagent spawning |
| `parallel` | Multiple executor subagents run simultaneously on non-overlapping WIs | Harness supports parallel agents |
| `external` | External framework (e.g. Teamwork) owns the lifecycle; Kramak provides governance rules | You're inside an external orchestrator |

**No extra setup needed.** The spec auto-detects your harness capabilities (§1 Execution Mode Detection). The same `.kramak/` directory and adapter works for all modes.

**For external orchestrators (Antigravity Teamwork, Claude Code Agent Teams, Cursor parallel agents, etc.):** The adapter's "External Orchestrator Integration" section tells Kramak to operate as a governance library — providing scope enforcement, verification, and circuit breaker while the framework handles dispatch and lifecycle.

**For manual orchestration:** If you want to use `orchestrated` mode but your harness doesn't auto-detect, you can manually set `"executionMode": "orchestrated"` in `state.json` before saying "Start".

---

## What to Expect

### Your First Session
- **Bootstrapping (~30 seconds):** Agent detects your toolchain (Node, Python, Rust, Go, etc.), creates `state.json`, scans for project documentation
- **Planning (~2-5 minutes):** Agent reads your goal/codebase, determines product phase, writes Work Items to `.kramak/work-items/`
- **Execution:** Agent implements Work Items one by one, running tests after each change
- **Audit:** Agent reviews all changes with fresh perspective, catches issues the executor missed

### Subsequent Sessions
- Agent reads `state.json` and `SESSION-LOG.md` to know exactly where it left off
- Picks up from the correct phase (executing, auditing, or planning next batch)
- No re-explanation needed — just say **"Start"** or **"Continue"**

### Session Limits

Kramak Lite enforces hard stop gates to prevent context fatigue:

| Gate | Threshold | Why |
|---|---|---|
| Work Items completed | ≥6 in one session | Quality degrades silently after sustained output |
| Files modified | ≥20 in one session | High modification count signals over-scoping |
| Errors corrected | ≥4 in one session | Repeated error correction contaminates context |
| Failed WIs | ≥1 in one session | Failure context pollutes subsequent work |

When a gate triggers, the agent commits its state and recommends a fresh session. **This is by design** — models cannot self-detect quality degradation, so the gates enforce the pause.

### Adding New Goals
Add items directly to the `## Unprocessed` section in `.kramak/inbox/INBOX.md` at any time with a type tag (`direction:`, `bug:`, `insight:`, `data:`, `credential:`). The planner picks it up in the next planning cycle.

---

## Common Scenarios

### "I have an existing project with code but no AI setup"
This is the most common scenario. Just follow the normal install above. The agent will:
1. Detect your existing toolchain and test commands
2. Set product phase to `ITERATE` (since code already exists)
3. Scan for your README, architecture docs, roadmap
4. Plan improvements based on what it finds

### "I already have CLAUDE.md / AGENTS.md with my own rules"
**Don't overwrite it.** Append the Kramak adapter section instead (see the install commands above with `cat >> `). Kramak is designed to cooperate with existing rules — it uses "constitutional framing" (cooperative language, not identity overrides) specifically to avoid conflicts.

### "I want to use this with a team"
Add `.kramak/` to version control. All team members share the same spec and state:
```bash
git add .kramak/
git commit -m "chore: add kramak-lite process framework"
```

The `state.json` tracks which Work Items are done, so different sessions can pick up where the last one left off.

### "I want to switch from full Kramak to Lite"
1. Back up your `.kramak/state.json`
2. Replace your `.kramak/` contents with Kramak Lite's `.kramak/`
3. Copy your `state.json` back (core fields are compatible)
4. If your state references phases like `dispatch`, `merge_queue`, or `bootstrap`, update `phase` to the nearest Lite equivalent (`planning` for bootstrap/dispatch, `auditing` for merge_queue)

### "I want to upgrade from Lite to full Kramak later"
Since both use the `.kramak` directory, upgrading is straightforward:
1. Replace `.kramak/` contents with full Kramak's `.kramak/`
2. Your `state.json` carries forward (Lite fields are a subset of Full)
3. Update your adapter to point to full Kramak's `ROUTER.md` instead of `KRAMAK-LITE.md`

---

## When Things Go Wrong

| Problem | Solution |
|---|---|
| **WI fails 3 times** | Circuit breaker trips. Agent stops with diagnosis. Review the error, then start a fresh session with a new strategy. |
| **Spec too vague** | Agent will recommend elevating detail tier (Outcome → Directed → Guided). Provide more specific guidance in the WI. |
| **Agent is confused** | Check `.kramak/state.json` — it shows the current phase and next action. If corrupted, delete `state.json` and say "Start". |
| **Agent ignores Kramak** | Restart the session. Make sure the adapter is in the right location. Say "Follow the Kramak workflow" explicitly. |
| **Need to start over** | Delete `.kramak/state.json` and say "Start" to re-bootstrap from scratch. Your WI history is preserved in `work-items/`. |
| **Agent asks too many questions** | Kramak tells the executor not to ask questions during execution. If this happens, remind the agent: "Follow the Kramak workflow — resolve from the spec, not from me." |

---

## Tips for Success

1. **Start small.** Let the agent do 1-2 batches before giving it a huge project.
2. **Write clear goals.** The more specific your `.kramak/inbox/INBOX.md`, the better the first plan.
3. **Trust the process.** Most WIs are Directed — the agent figures out implementation details.
4. **Respect session limits.** After 5+ WIs, start a new session. Quality degrades silently.
5. **Read the Work Items.** Check `.kramak/work-items/` to see what the agent planned — they're your review checkpoint.
6. **Use product phases.** If priorities seem off, check `state.productPhase`. BUILD = features, SHIP = deployment, ITERATE = improvements.
7. **Don't fight the circuit breaker.** If it trips, the approach is wrong. Rethink, don't retry.

---

## Further Reading

- [Architecture & Design Decisions](ARCHITECTURE.md) — Why single-file, IDE compatibility strategy, token analysis, `.kramak` naming rationale
- [Full Kramak Mapping](FULL-KRAMAK-MAPPING.md) — Rule-by-rule coverage map of all 176 rules
- [Changelog](../CHANGELOG.md) — Version history with rationale for every change
