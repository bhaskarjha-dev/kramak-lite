# Kramak-Lite vs. the AI-Agent Process-Control Landscape
### Competitive Analysis & Architectural Comparison

> **Benchmarked Against:** 20 tools across 6 standardized dimensions (August 2026 snapshot).  
> **Methodology:** Author-assessed scoring based on public documentation, repos, and feature audits. Scores reflect one evaluator's judgment — not community consensus or automated measurement. Tool versions may have changed since the snapshot date.  
> **Core Value Proposition:** Single-file, zero-dependency, IDE-agnostic process-control specification (Plan → Execute → Audit state machine) with quantitative hard-stop gates and tiered task detail.

---

## 1. Executive Summary & Scoring Matrix

Each tool was evaluated across six dimensions (1–5 points each, 30 max):
1. **Coding-Agent Fit:** Precision of focus on AI coding agents/IDEs vs general-purpose automation.
2. **Workflow Rigor:** Structure of the Plan → Build → Verify lifecycle and artifact clarity.
3. **Portability:** Dependency footprint; usable across any IDE/terminal without installing runtimes.
4. **Gate Enforcement:** Mechanization of checkpoints (schemas, hard stop numbers, CI/hooks vs advisory prose).
5. **Host/Model Reach:** Number of actual IDEs and models supported out of the box.
6. **Adoption & Maturity:** Public community validation, stars, and real-world testing.

### Full 21-Tool Leaderboard

| Rank | Tool | Coding Fit | Workflow Rigor | Portability | Gate Enforcement | Host Reach | Adoption | **Total /30** | Footprint & Mechanism |
|---|---|:-:|:-:|:-:|:-:|:-:|:-:|:-:|---|
| 1 | **GitHub Spec Kit** | 5 | 5 | 3 | 3 | 5 | 5 | **26** | CLI (`uv`/Python 3.11+), slash-command workflow, 30+ integrations |
| 1 | **Superpowers** | 4 | 5 | 4 | 3 | 5 | 5 | **26** | Auto-triggering skills library, TDD-execute, 280K★ community |
| 3 | **BMAD-METHOD** | 4 | 5 | 3 | 3 | 5 | 5 | **25** | 21 agent personas, agile framework, Node/Python runtime |
| 3 | **GSD Core** | 5 | 5 | 3 | 4 | 5 | 3 | **25** | Context-engineering system, fresh subagent loops, mandatory installer |
| 5 | **Spec Kitty** | 5 | 5 | 2 | 5 | 4 | 3 | **24** | Spec Kit fork, git worktrees, CI drift detector gate |
| 5 | **Gangsta Agents** | 5 | 4 | 5 | 4 | 4 | 2 | **24** | 6-phase heist framework, contract gate, persistent ledger |
| **7** | **Kramak-Lite** | **5** | **4** | **5** | **4** | **4** | **1** | **23** | **Single 45KB markdown spec, 0 runtime deps, quantitative gates** |
| 7 | **OpenSpec** | 5 | 3 | 3 | 2 | 5 | 5 | **23** | Delta-format specs for brownfield repos, explicitly advisory ("nothing locks") |
| 7 | **Tessl** | 5 | 4 | 3 | 3 | 4 | 4 | **23** | Commercial platform ($125M raised), spec-as-source code generation |
| 10 | **MUSUBI** | 5 | 5 | 4 | 5 | 2 | 1 | **22** | 7 agents × 31 skills, 9-article constitution, high rigor, stalled (~57★) |
| 11 | **CursorRIPER♦Σ** | 5 | 4 | 4 | 4 | 2 | 2 | **21** | RIPER-5 fork with CRUD permission matrix and memory bank |
| 12 | **Traycer** | 5 | 4 | 2 | 3 | 2 | 4 | **20** | Commercial VS Code extension (100K+ users), Epic ticket mode |
| 13 | **Kiro** | 5 | 4 | 2 | 3 | 1 | 4 | **19** | AWS-backed agentic IDE, requirements/design/tasks, locked to Kiro IDE |
| 13 | **Kilo Code** | 3 | 3 | 2 | 2 | 4 | 5 | **19** | Roo Code fork, memory bank, 1.5M+ users, not strictly SDD |
| 13 | **Ruflo (Claude-Flow)** | 2 | 3 | 1 | 3 | 5 | 5 | **19** | 100+ agents swarm meta-harness; SPARC is 1 of 35 plugins |
| 16 | **RIPER-5 (original)** | 5 | 3 | 5 | 1 | 2 | 2 | **18** | Viral Cursor prompt, mode declarations, zero schema/state |
| 16 | **Cline** | 3 | 2 | 2 | 2 | 4 | 5 | **18** | Autonomous agent extension, Plan/Act toggle, `.clinerules` |
| 18 | **Zencoder/Zenflow** | 4 | 4 | 1 | 3 | 3 | 2 | **17** | Commercial SDD-as-a-service, cross-agent review |
| 18 | **Ralph Loop** | 3 | 1 | 5 | 1 | 4 | 3 | **17** | Minimalist stateless bash pattern, fresh agent per loop, no gates |
| 20 | **Devin** | 4 | 3 | 1 | 2 | 1 | 4 | **15** | Proprietary cloud engineer sandbox, human PR review |

---

## 2. Where Kramak-Lite Wins Outright

### 1. Zero Runtime Dependencies (Pure Portability: 5/5)
- **The Competition:** GitHub Spec Kit requires `uv` + Python 3.11+; BMAD requires Node 20.12+, Python 3.10+, and `uv`; OpenSpec requires Node ≥20.19; Spec Kitty requires `pip` and git worktree automation.
- **Kramak-Lite:** Literally **one markdown file** in `.kramak/KRAMAK-LITE.md`. Zero packages to install, zero binaries to compile, zero container setups. Works on air-gapped systems, secure corporate environments, and any terminal or IDE immediately.

### 2. Quantitative, Unambiguous Hard Stop Gates
- **The Competition:** Superpowers relies on the agent choosing to invoke mandatory skills; OpenSpec explicitly refuses to gate ("nothing locks"); GSD's verification is qualitative prose.
- **Kramak-Lite:** Sets strict mathematical limits against context degradation:
  - **≥6 Work Items completed** → Hard Stop (Fresh Session required)
  - **≥20 files modified** → Hard Stop (Fresh Session required)
  - **≥4 tool/command errors** → Hard Stop (Fresh Session required)
  - **3 consecutive failures** → Circuit Breaker trips to `escalated`

### 3. Goldilocks Rule: 3-Tier Task Detail Scaling
- Rather than forcing one monolithic spec format on every task:
  - **Guided:** Exact BEFORE/AFTER snippets for high-risk changes (schemas, auth, payments).
  - **Directed:** Strict acceptance criteria and interfaces for standard features.
  - **Outcome:** Concise criteria only for docs, standalone components, and styles.

---

## 3. Detailed Head-to-Head Comparisons

### Kramak-Lite vs. GitHub Spec Kit
- **Spec Kit Strengths:** Huge backing (GitHub/Microsoft), 30+ integrations, rich slash-command CLI workflow (`specify → plan → tasks → implement`).
- **Spec Kit Limitations:** Requires Python/uv installation; rigid 8-step pipeline; heavyweight for rapid iteration.
- **Kramak-Lite Advantage:** 100% portable; no runtime dependency; includes built-in Strategic Vision (5 lenses) and meta-cognitive perspective switching.

### Kramak-Lite vs. Superpowers
- **Superpowers Strengths:** #1 Claude Code skills library (280K★); seamless TDD loop; strong Anthropic community integration.
- **Superpowers Limitations:** Heavily tailored to Claude Code; lacks cross-host schema validation; advisory self-enforcement.
- **Kramak-Lite Advantage:** Works identically in Claude Code, Cursor, Antigravity, and any generic terminal agent; persistent JSON state machine across all sessions.

### Kramak-Lite vs. OpenSpec
- **OpenSpec Strengths:** Delta-format specs (ADDED/MODIFIED/REMOVED); excellent for incremental changes in legacy brownfield repos.
- **OpenSpec Limitations:** Refuses to enforce hard stops or circuit breakers; relies on user discipline.
- **Kramak-Lite Advantage:** True bounded autonomy with failure recovery, write-ahead logging (WAL), and strict scope enforcement (`files_targeted`).

---

## 4. Closing the Remaining Gaps (The Road to 27/30)

Kramak-Lite sits just 3 points behind the category leaders:
1. **Gate Enforcement (4 → 5):** Adding optional pre-tool-use hooks and CI scope-verification checks.
2. **Workflow Rigor (4 → 5):** Adding explicit adversarial audit framing and formal spec-drift notes.
3. **Host Reach & Adoption (1 → 3):** Evaluating universal agent packaging standards (e.g. open Agent Plugin standards, cross-agent skills manifests) for frictionless one-command installation.

See [ROADMAP.md](ROADMAP.md) for the complete exploratory backlog and candidate horizons.
