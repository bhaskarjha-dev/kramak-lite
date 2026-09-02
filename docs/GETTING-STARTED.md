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
│   ├── plans/                ← Batch plans and audit reports
│   └── templates/            ← Template format references
├── src/                      ← Your existing code (untouched)
├── package.json              ← Your existing config (untouched)
└── ...
```

### Step 2: Add Your IDE Adapter

The adapter is a small file (~20 lines) that tells your AI agent where to find the Kramak spec. Pick your IDE:

#### Antigravity IDE
```bash
mkdir -p .agents/skills/kramak/
cp /path/to/kramak-lite/adapters/antigravity/SKILL.md .agents/skills/kramak/SKILL.md
```
> Installs as a skill. No conflicts with existing skills.

#### Claude Code
```bash
# If you DON'T have a CLAUDE.md yet:
cp /path/to/kramak-lite/adapters/claude-code/CLAUDE.md ./CLAUDE.md

# If you ALREADY have a CLAUDE.md (don't overwrite!):
echo "" >> ./CLAUDE.md
cat /path/to/kramak-lite/adapters/claude-code/CLAUDE.md >> ./CLAUDE.md
```
> **Important:** If you have existing rules in CLAUDE.md, always append — never overwrite. Kramak cooperates with your existing rules.

#### Cursor
```bash
mkdir -p .cursor/rules/
cp /path/to/kramak-lite/adapters/cursor/.cursorrules .cursor/rules/kramak.mdc
```
> Cursor loads all `.mdc` files from `.cursor/rules/`. No conflicts.

#### Other IDEs (Windsurf, Cline, Gemini CLI, etc.)
```bash
# If you DON'T have an AGENTS.md / GEMINI.md yet:
cp /path/to/kramak-lite/adapters/generic/AGENTS.md ./AGENTS.md

# If you ALREADY have one (don't overwrite!):
echo "" >> ./AGENTS.md
cat /path/to/kramak-lite/adapters/generic/AGENTS.md >> ./AGENTS.md
```
> Rename to `GEMINI.md`, `.clinerules`, or whatever your IDE reads.

#### Using Multiple IDEs?
Install adapters for all IDEs you use. They're independent files in different locations — all point to the same `.kramak/KRAMAK-LITE.md`.

### Step 3: (Optional) Write a Goal

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

### Step 4: Say **"Start"**

Open your AI agent and type: **Start**

The agent will:
1. Read the Kramak spec and detect your project's toolchain
2. Initialize git if not already present
3. Determine the product phase (BUILD/SHIP/ITERATE) for priority guidance
4. Plan a batch of Work Items based on your goal or codebase analysis
5. Execute them one by one with scope enforcement and verification
6. Audit the results with fresh-eyes review
7. Plan the next batch or mark the project complete

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
