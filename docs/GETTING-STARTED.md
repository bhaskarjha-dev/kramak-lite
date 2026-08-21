# Getting Started with Kramak Lite

## Step 1: Add Kramak Lite to Your Project

Copy the `.kramak/` directory from this repository into your project root:

```bash
cp -r /path/to/kramak-lite/.kramak/ /path/to/your/project/.kramak/
```

Your project should now have:
```
your-project/
├── .kramak/
│   ├── KRAMAK-LITE.md
│   ├── schemas/
│   │   ├── state.schema.json
│   │   └── work-item.schema.json
│   ├── work-items/
│   ├── inbox/
│   └── templates/
│       └── WORK-ITEM.template.md
├── src/
├── package.json
└── ...
```

## Step 2: Install Your IDE Adapter

The adapter tells your AI agent how to find and follow the Kramak workflow.

### Antigravity IDE
```bash
mkdir -p .agents/skills/kramak/
cp /path/to/kramak-lite/adapters/antigravity/SKILL.md .agents/skills/kramak/SKILL.md
```

### Claude Code
```bash
# If you don't already have a CLAUDE.md, copy the adapter:
cp /path/to/kramak-lite/adapters/claude-code/CLAUDE.md ./CLAUDE.md

# If you already have CLAUDE.md, append the Kramak section:
cat /path/to/kramak-lite/adapters/claude-code/CLAUDE.md >> ./CLAUDE.md
```

### Cursor
```bash
mkdir -p .cursor/rules/
cp /path/to/kramak-lite/adapters/cursor/.cursorrules .cursor/rules/kramak.mdc
```

### Any Other IDE
```bash
# Copy the generic adapter to your IDE's rules file:
cp /path/to/kramak-lite/adapters/generic/AGENTS.md ./AGENTS.md
# Or: GEMINI.md, .clinerules, etc. — whatever your IDE reads.
```

## Step 3: (Optional) Add a Goal

Write your project goal to `.kramak/inbox/goal.md`:

```markdown
# Project Goal

Build a REST API for user management with:
- User registration and login (JWT auth)
- Profile CRUD operations
- Role-based access control
- PostgreSQL database with Prisma ORM
```

## Step 4: Say "Start"

Open your AI agent and type: **Start**

The agent will:
1. Read the Kramak spec and detect your project's toolchain
2. Plan a batch of 3-8 Work Items based on your goal
3. Execute them one by one with scope checking and verification
4. Audit the results
5. Plan the next batch (or mark the project complete)

## What to Expect

### First Session
- Agent bootstraps: detects your toolchain, creates `state.json`
- Agent plans Batch 1: writes Work Items to `.kramak/work-items/`
- Agent may execute immediately (if using a capable model) or recommend a separate execution session

### Subsequent Sessions
- Agent reads `state.json` to know where it left off
- Picks up from the correct phase (executing, auditing, or planning next batch)
- No re-explanation needed — just say **"Start"** or **"Continue"**

### Adding New Goals
Drop a `.md` file in `.kramak/inbox/` at any time. The planner will pick it up in the next planning cycle.

### When Things Go Wrong
- **WI fails 3 times:** Circuit breaker trips → agent stops and shows diagnosis
- **Agent is confused:** Check `state.json` — it shows the current phase and next action
- **Need to restart:** Delete `state.json` and say "Start" to re-bootstrap

## Tips

1. **Start small.** Let the agent do 1-2 batches before giving it a huge project.
2. **Trust the process.** The Goldilocks Rule means most WIs are 🟡 Directed — the agent figures out the implementation details.
3. **Write clear goals.** The more specific your `inbox/goal.md`, the better the first batch plan.
4. **Use fresh sessions.** After 5+ WIs, context fatigue is real. Start a new session.
5. **Check the Work Items.** Read `.kramak/work-items/` to see what the agent planned — they're your review checkpoint.
