# Kramak-Lite — Strategic Roadmap: Candidate Explorations & Future Horizons

> **Current Version:** 0.1.0-dev  
> **Last Updated:** September 2026  
> **Status:** Pre-Release Development — Heading toward v0.1.0 public release  
> **Core Principle:** Host-Agnostic, Zero-Dependency Standard. All items below represent exploratory candidate directions under evaluation. Kramak-Lite will not be locked into or bound by any single proprietary vendor or ecosystem.

---

## 1. Executive Summary & Competitive Scoreboard

In an exhaustive independent competitive benchmark across 21 process-control tools (evaluated across 6 standardized dimensions: Coding-Agent Fit, Workflow Rigor, Portability, Gate Enforcement, Host/Model Reach, Adoption), **Kramak-Lite currently scores 25/30 (Ranked #3, Tier 1):**

| Dimension | Kramak-Lite Now | Category Leader(s) | Gap | Strategic Driver | Target (Candidate) |
|---|:-:|:-:|:-:|---|:-:|
| **Coding-Agent Fit** | **5/5** | 5/5 | — | Zero wasted surface area on non-coding tasks. Keep as-is. | **5/5** |
| **Workflow Rigor** | **5/5** | 5/5 (Spec Kit, GSD) | — | Orchestration-aware handoffs and governance protocol brought this to parity. | **5/5** |
| **Portability** | **5/5** | 5/5 (Tied) | — | Unmatched zero-runtime-dependency, single-file spec (~56KB). Core asset. | **5/5** |
| **Gate Enforcement** | **4/5** | 5/5 (Spec Kitty) | 1 pt | Quantitative gates exist; evaluate optional external git/CI backstops. | **5/5** |
| **Host/Model Reach** | **5/5** | 5/5 (Spec Kit) | — | Universal AGENTS.md + external mode + orchestrator-aware adapters. | **5/5** |
| **Adoption & Maturity** | **1/5** | 5/5 (Superpowers) | 4 pts | Zero public distribution / marketplace packaging. Pure visibility gap. | **2-3/5** |
| **TOTAL** | **25/30** | **26/30** (Spec Kit) | **-1** | **Close 1 technical point (Gate Enforcement) to tie #1 on merit (26/30).** | **27/30** |

> **The Strategic Takeaway:** The technical gap to #1 is now **1 point** (Gate Enforcement). The remaining gap is **almost entirely a visibility and adoption problem**, solvable through open distribution standards and community testing.

---

## 2. Architectural Framework: Candidate Escalation & Distribution Vectors

Early research notes hypothesized a conceptual "6-rung progressive enforcement ladder". In practice, Kramak-Lite's canonical design is **strictly host-agnostic and zero-dependency**. Rather than adopting a rigid vendor-specific ladder (e.g. locking into Claude-specific mechanisms or proprietary SDKs), Kramak-Lite treats any external mechanization as **provisional candidate vectors to explore**:

```
 Tier 4   Standardized Protocol Interfaces (Optional MCP state server / open agent RPCs)
   ▲
 Tier 3   Portable Mechanical Backstops (Universal Git pre-commit + CI PR verification)
   │
 Tier 2   Universal Open Agent Packaging (Universal Agent Plugin standards, cross-agent skills)
   │
 Tier 1   Canonical Core (Implemented: Single-file, zero-dependency, constitutional framing, orchestration-aware)
```

**Sovereignty Invariant:** Keep the core `.kramak/KRAMAK-LITE.md` completely zero-dependency and model-agnostic. Higher tiers are evaluated purely as **optional, opt-in satellite layers** (e.g., portable scripts or open packaging formats). If any candidate direction compromises independence or introduces bloat, it will not be adopted.

---

## 3. Phased Implementation Candidates (Under Evaluation)

### Phase 0: Zero-Cost Self-Serve Distribution (Priority: Immediate Evaluation)
*Goal: Remove friction from installation and eliminate visibility blind spots without vendor lock-in.*

- [ ] **P0-1: Explore Universal Agent Plugin & Ecosystem Packaging (Candidate)**
  - Investigate packaging formats for zero-friction distribution:
    - Evaluate emerging **universal Agent Plugin standards** to support multiple open agents seamlessly.
    - Investigate host-specific packaging (such as `.claude-plugin/` or Cursor extensions) purely as optional wrappers.
    - Enable one-command installation without manual file copying.
- [ ] **P0-2: Publish to Universal Registries (e.g., `skills.sh`)**
  - Validate against the Vercel Labs `skills.sh` schema to support 38+ AI coding agents (Claude Code, Cursor, Codex, Windsurf, Cline, Roo Code, OpenCode, Goose, etc.) via:
    ```bash
    npx skills add bhaskarjha-dev/kramak-lite
    ```
- [ ] **P0-3: Provide Standalone `docs/COMPARISON.md`**
  - Publish the 20-tool objective benchmark matrix comparing Kramak-Lite to Spec Kit, Superpowers, BMAD-METHOD, GSD Core, and OpenSpec.
- [ ] **P0-4: Awesome-Lists Submissions**
  - Submit PR to `Engineering4AI/awesome-spec-driven-development` and general agentic workflow curated lists.

---

### Phase 1: Workflow Rigor & Audit Independence (Priority: High Evaluation)
*Goal: Evaluate closing the 1-point Workflow Rigor gap (+1 pt).*

- [ ] **P1-1: Adversarial Audit Framing in §5 (Candidate)**
  - Update §5 (AUDITING) in `KRAMAK-LITE.md` from passive "review with fresh eyes" to an explicit mandate:
    > *"Audit with an adversarial mindset: actively attempt to discover edge-case regressions, unhandled errors, and scope creep. Assume the implementation has flaws until live tests prove otherwise."*
  - On platforms supporting subagents (e.g. Antigravity subagents, Claude Code Task tool, OpenCode subtasks), provide instructions to dispatch a fresh subagent with zero conversational history.
- [ ] **P1-2: Explicit Spec-Drift Reconciliation Format (Candidate)**
  - Formalize the "Drift Note" in the batch plan template (`.kramak/templates/batch-plan.md`) to explicitly surface when codebase realities force an intentional departure from original specs (addressing the #1 critique of spec-driven development).

---

### Phase 2: Mechanical Scope & State Backstops (Priority: High Evaluation)
*Goal: Evaluate closing the 1-point Gate Enforcement gap (+1 pt) via portable, optional backstops.*

- [ ] **P2-1: Universal Git Pre-Commit Hook Fallback (Candidate)**
  - Provide a portable git pre-commit hook script (`scripts/kramak-pre-commit.sh`) usable across any IDE, editor, or terminal:
    - Runs `git diff --name-only` against `files_targeted`.
    - Validates that `.kramak/state.json` matches `state.schema.json`.
    - Aborts commit if scope is violated.
- [ ] **P2-2: CI Scope Backstop (GitHub Actions) (Candidate)**
  - Create `.github/workflows/verify-scope.yml`:
    - Validates PR commits against active Work Item `files_targeted`.
    - Guarantees that even if an agent uses `--no-verify` or bypasses client-side hooks, out-of-scope code cannot be merged.
- [ ] **P2-3: Evaluate Client-Side Tool Interception Hooks (Candidate)**
  - Explore whether optional shell/node hooks (e.g. for Claude Code PreToolUse or OpenCode plugin hooks) provide significant marginal value over git pre-commit hooks, while ensuring zero core dependencies.

---

### Phase 3: Empirical Validation & Benchmark Proof (Priority: Medium Evaluation)
*Goal: Replace assertions with verifiable empirical data.*

- [ ] **P3-1: Empirical Scope-Violation Benchmark (OverEager-Gen / SNARE)**
  - Run a 15–20 task empirical benchmark measuring scope-violation rates (unauthorized file edits, config rewrites, extraneous deletions) with and without Kramak-Lite active on identical models (Claude 3.7 Sonnet, GPT-4o, Gemini 2.5 Flash).
  - Publish raw transcripts and metrics in `docs/benchmarks/`.
- [ ] **P3-2: Disclosed Opt-In Telemetry (Candidate)**
  - Provide an optional, fully-disclosed version ping to measure real-world installations (if deemed appropriate and user-respecting).

---

### Phase 4: Long-Term Horizons & Architectural Exploration (Priority: Low / Post-v3)

- [ ] **P4-1: Open Agent Protocol Interfaces (Candidate)**
  - Explore whether exposing FSM state queries and gate validation over open protocols (like MCP — Model Context Protocol) adds tangible workflow value across diverse agent hosts.
- [ ] **P4-2: Universal Agent SDK / Open Harness Compatibility (Candidate)**
  - Evaluate integration with open-source agent SDKs and emerging harness standards, ensuring Kramak's process model remains host-independent.

---

## 4. Open Decisions & Backlog

1. **License Harmonization:** ✅ Resolved
   - *Decision:* Both `kramak` and `kramak-lite` now use MIT. Harmonized based on ecosystem research: all direct competitors (Spec Kit, BMAD, Superpowers, GSD Core) use MIT, skills.sh ecosystem favors MIT, and MIT maximizes adoption for future MCP servers and agent plugins.
2. **Phase Separation vs. Single File:**
   - *Current:* Single ~56KB file (`KRAMAK-LITE.md`).
   - *Decision:* Maintain the single-file core. With 250K–1M token context windows now standard, the single-file architecture case rests on reliability and simplicity, not token budget. Only split if models demonstrably lose instruction-following accuracy in later sections.
3. **External Mode Framework-Specific Detection:**
   - *Current:* `external` mode detection relies on "were you spawned with a pre-assigned task?" heuristic.
   - *Decision:* As more external orchestrators emerge beyond Antigravity Teamwork, evaluate whether framework-specific detection heuristics or adapter annotations are needed.
4. **Teamwork Blueprint Module:**
   - *Candidate:* If/when Teamwork supports custom governance hooks, Kramak Lite could be loaded as a standard Teamwork blueprint module rather than just an AGENTS.md adapter.
   - *Prerequisite:* Teamwork blueprint API must be stable and documented.
5. **§7.5 ALWAYS/HEURISTIC/SKIP Refinement:**
   - *Current:* The governance library interface in §7.5 classifies rules into ALWAYS apply, USE AS HEURISTICS, and SKIP categories.
   - *Decision:* Refine these classifications based on real-world usage data from `external` mode deployments. Some "heuristic" rules may prove universally valuable (promote to ALWAYS) or create friction (demote to SKIP).
6. **Competitive Benchmark Refresh:**
   - *Resolved (September 2026):* Benchmark scores updated to 25/30 reflecting governance protocol evolution (+1 Workflow Rigor, +1 Host/Model Reach). See ADR-001 for the analysis.
   - *Maintenance:* Re-evaluate periodically as tools evolve.
7. **Architecture Decision Records:**
   - *Added:* `docs/decisions/` directory for ADRs capturing strategic reasoning behind architectural changes.
   - *Maintenance:* Write an ADR for any future decision involving tradeoffs between alternatives. See [ADR index](decisions/README.md).
