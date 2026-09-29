# ADR-001: Governance Protocol Evolution (v3.0.0)

> **Date:** September 2026  
> **Status:** Accepted and Implemented  
> **Commits:** `b4e939c`, `84aa349`

---

## Context

By mid-2026, 15 of 18 modern AI coding harnesses supported native multi-agent/subagent orchestration (Antigravity 2.0, Claude Code Task tool, Cursor Background Agents, GSD Core, etc.). Kramak Lite v2.x was designed around sequential, human-initiated sessions — the user manually said "Start" in fresh conversations for each role transition (Plan → Execute → Audit).

This created a growing mismatch:

| Kramak Lite v2.x Assumption | 2026 Reality |
|---|---|
| Users will manually start fresh sessions | Harnesses automate session/subagent management |
| One agent at a time (sequential) | Harnesses support parallel agents |
| Role separation = separate human-initiated sessions | Subagent spawning with isolated context achieves the same thing |
| §7 "Multi-Agent Dispatch" = 5 vestigial lines | Multi-agent orchestration is the dominant execution pattern |

## The Precise Tension

> **Manual sessions, not sequential execution, was the real problem.**

Kramak Lite's process model (Plan → Execute → Audit with strict role separation) was sound. The _delivery mechanism_ (relying on humans to start fresh sessions) was becoming obsolete. Subagent spawning with context isolation is the native mechanism for the same role separation that manual sessions provided.

## Options Considered

### Option A: Stay As-Is (Sequential Manual Sessions)
- **Verdict:** Increasing irrelevance as harnesses automate orchestration.
- **Risk:** Gradual marginalization to single-agent IDEs (a shrinking category).

### Option B: Become a Multi-Agent Orchestration Framework
- Ship orchestration code (scripts, SDK integrations, harness-specific runtime logic).
- **Verdict:** REJECTED. This destroys Kramak's #1 competitive moat — zero dependencies, any IDE, any model. Becomes "yet another framework" competing with GSD Core and Superpowers on their home turf.
- **Risk:** Scope creep, fragmentation across N harness-specific adapters with runtime code.

### Option C: Become a Governance Protocol Layer ✅ (Chosen)
- Remain zero-dependency specification. Evolve from "session-level playbook" to "governance protocol that orchestrators consume."
- The spec describes WHAT to do; adapters and harnesses decide HOW.
- **Verdict:** ACCEPTED. Preserves every strength, adds native multi-agent support, zero runtime dependencies added.

### Option D: Dual-Track (Kramak Lite Core + Kramak Agent)
- Kramak Lite stays as spec; a companion "Kramak Agent" project handles orchestration.
- **Verdict:** REJECTED. Two projects to maintain, risk of divergence, the orchestrator competes with existing tools that bundle spec + execution.

## Decision

Kramak Lite evolves to own **Layers 2-3** of the development stack and provides clear interfaces for Layer 1:

```
┌─────────────────────────────────────────┐
│ Layer 4: User Intent (inbox, goals)      │  ← User writes here
├─────────────────────────────────────────┤
│ Layer 3: Strategic Planning              │  ← Kramak Lite owns this
│   (5-lens vision, PERCEIVE→REASON→DECIDE,│
│    perspective selection, WI authoring)   │
├─────────────────────────────────────────┤
│ Layer 2: Process Governance              │  ← Kramak Lite owns this
│   (scope enforcement, circuit breaker,   │
│    failure taxonomy, hard stop gates,    │
│    Goldilocks Rule, cross-session state) │
├─────────────────────────────────────────┤
│ Layer 1: Orchestration                   │  ← Harness owns this
│   (session management, subagent spawn,   │
│    parallel dispatch, context isolation)  │
├─────────────────────────────────────────┤
│ Layer 0: Model + Tools                   │  ← Provider owns this
│   (LLM, file I/O, terminal, git, search) │
└─────────────────────────────────────────┘
```

Four execution modes introduced:
- `manual` — v2.x behavior (default, backward-compatible)
- `orchestrated` — Kramak's Planner spawns Executor/Auditor subagents
- `parallel` — Same as orchestrated via harness's parallel mechanism
- `external` — External framework owns lifecycle; Kramak provides governance rules as a library

## Competitive Impact

| Dimension | v2.3.0 | v3.0.0 | Change |
|---|---|---|---|
| Coding-Agent Fit | 5/5 | 5/5 | — |
| Workflow Rigor | 4/5 | 5/5 | +1 (orchestration-aware handoffs) |
| Portability | 5/5 | 5/5 | — (still zero-dependency) |
| Gate Enforcement | 4/5 | 4/5 | — |
| Host/Model Reach | 4/5 | 5/5 | +1 (works natively in multi-agent harnesses) |
| Adoption | 1/5 | 1/5 | — |
| **TOTAL** | **23/30** | **25/30** | **+2** |

## Risk Analysis

| Risk | Severity | Mitigation |
|---|---|---|
| Spec grows past single-file threshold | Low | Modern 250K-1M context windows make this a non-issue. Split only on demonstrated accuracy degradation. |
| Harness capabilities are a moving target | Medium | Adapters are thin and separately maintained. Core spec is harness-agnostic. |
| Parallel dispatch introduces merge conflicts | High | Safety invariant: parallel ONLY when `files_targeted` sets have zero overlap. Mandatory merge verification. |
| Users on single-agent harnesses feel left behind | Low | `manual` is the default. All existing behavior preserved. |

## What Was Deliberately NOT Done

1. **No runtime code shipped.** No `kramak-orchestrate.js`, no `kramak-dispatch.py`. The moment Kramak ships orchestration scripts, it loses its core differentiator.
2. **No harness-specific orchestration.** Adapters explain the spawning mechanism; they don't implement it.
3. **No mandatory parallelism.** "When in doubt, run sequentially" is the safety invariant. Parallel execution is optimization, not requirement.
4. **No version-breaking changes.** `executionMode: "manual"` is the default. v2.x workflows are completely unchanged.

## Consequences

- The spec grew from ~45KB to ~55KB (v2.3.0 → v3.0.0 with external mode). Still <5% of modern context windows.
- 4 adapters each grew by ~10-25 lines for orchestration hints.
- New §7 section expanded from 5 vestigial lines to a full protocol with safety invariants, dispatch protocol, merge/verify, and subagent role prompts.
- New §7.5 section defines the `external` mode governance library interface.
