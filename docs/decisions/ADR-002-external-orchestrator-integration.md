# ADR-002: External Orchestrator Integration (Teamwork Compatibility)

> **Date:** September 2026  
> **Status:** Accepted and Implemented  
> **Commit:** `84aa349`  
> **Depends on:** ADR-001

---

## Context

After implementing v3.0.0's governance protocol evolution (ADR-001), analysis of Antigravity 2.0 Teamwork revealed a structural collision: Teamwork is itself a complete autonomous development framework with its own planning, dispatch, verification, and lifecycle management. Kramak Lite's `orchestrated`/`parallel` modes assume Kramak owns the lifecycle — which directly conflicts with Teamwork's architecture.

### How Teamwork Works (Researched September 2026)

Teamwork organizes collaboration into three tiers:

```
TIER 1: ORCHESTRATION — Sentinel decomposes goals into milestones, routes to agents
TIER 2: IMPLEMENTATION — Specialized subagents execute in isolated context windows
TIER 3: VERIFICATION — Independent agents critique & challenge outputs at every milestone
```

### The Four Collision Points Identified

| Collision | What Fights | Kramak's Claim | Teamwork's Claim |
|---|---|---|---|
| **Who Plans?** | Task decomposition | Planner creates Work Items | Sentinel decomposes into milestone graph |
| **Who Orchestrates?** | Dispatch mechanism | Planner spawns Executor subagents | Teamwork auto-spawns specialized agents |
| **Who Verifies?** | Audit trigger | Auditor reviews post-batch | Verification agents critique per-milestone |
| **Who Owns State?** | Source of truth | `state.json` drives transitions | Teamwork manages state internally |

### Mechanism Comparison

| Mechanism | Teamwork | Kramak Lite |
|---|---|---|
| Task decomposition | Auto-decomposes via Sentinel | Planner creates WIs manually |
| Role assignment | Blueprint defines agent roles | Phase-based roles |
| Parallel dispatch | Auto-assigns isolated worktrees | `parallel_group` annotation |
| Verification | Per-milestone verification agents | Post-batch holistic audit |
| State management | Internal to framework | `state.json` — explicit, file-based |
| Scope enforcement | Not built-in (trusts agent) | Explicit `files_targeted` per WI |
| Strategic planning | Scoping phase ("definition of done") | 5-lens Vision + PERCEIVE→REASON→DECIDE |

## Key Insight: Framework vs. Library Duality

The resolution came from recognizing that Kramak Lite can operate in two postures:

| Posture | When | How |
|---|---|---|
| **Framework** | `manual`, `orchestrated`, `parallel` | Kramak owns the lifecycle. Agents follow Plan→Execute→Audit. |
| **Library** | `external` | External framework owns lifecycle. Kramak provides governance rules that agents apply within whatever lifecycle the framework defines. |

## What's Uniquely Kramak (Teamwork Has Nothing Equivalent)

| Capability | Why It's Unique |
|---|---|
| 5-lens Strategic Vision | No orchestrator thinks about competitive positioning, user journey, innovation |
| PERCEIVE→REASON→DECIDE | Meta-cognitive loop prevents mechanical execution |
| Goldilocks Rule | Risk-calibrated detail scaling — no other system does this |
| Perspective selection | "Think as a Security Engineer" vs "Think as a UX Designer" |
| Product Phase awareness | BUILD/SHIP/ITERATE priority ladders |
| `files_targeted` scope enforcement | Hard boundaries per unit of work |
| Circuit breaker | Quantitative failure escalation |
| Cross-session `state.json` | Persists across Teamwork sessions |

## What Kramak Should Surrender to External Frameworks

| Capability | Why the Framework Is Better |
|---|---|
| Task decomposition | Framework has native graph decomposition |
| Role transitions | Framework's tier system is native to the platform |
| Parallel dispatch | Framework handles worktree isolation, agent spawning |
| Merge/verify protocol | Framework's verification is more granular (per-milestone) |

## Decision

Introduce `executionMode: "external"` as a 4th execution mode. In this mode:

**ALWAYS applies:**
- Scope enforcement (`files_targeted`)
- Grounded Verification (5-step protocol)
- Verification after changes (`checkCommands`)
- Circuit breaker (3 failures = escalate)
- Session health gates
- Error taxonomy and retry logic
- State persistence in `state.json`

**USE AS HEURISTICS (when assigned planning role):**
- Strategic Reorientation, Strategic Vision
- PERCEIVE→REASON→DECIDE
- Perspective selection
- Goldilocks Rule
- Product Phase priority ladders

**SKIP (external framework handles):**
- Phase transitions
- Subagent spawning
- Merge protocol
- Parallel dispatch

## Integration Strategies Evaluated

### Strategy A: Kramak Replaces Teamwork ❌
Not viable. Teamwork is a native platform feature with deep integration.

### Strategy B: Kramak as Top-Level Governance ⚠️
High friction. Kramak v3.0.0's `orchestrated` mode tries to own the lifecycle, which fights Teamwork's own planning, dispatch, and verification.

### Strategy C: Kramak as Governance Library ✅ (Chosen)
Position Kramak as a governance library that any orchestrator consumes for quality rules it doesn't have (scope enforcement, strategic intelligence, circuit breaker).

## Antigravity Precedence Hierarchy (Why Kramak Can't Override Teamwork)

In Antigravity's conflict resolution, Kramak's adapter lives at priority 3 (project rules) or 5 (active skill). Teamwork's native orchestration is part of the platform (priority ~1-2). Teamwork wins every conflict. The `external` mode acknowledges this rather than fighting it.

## Consequences

- Kramak Lite now works in 5 environment types: manual sessions, Kramak-orchestrated subagents, parallel agents, Antigravity Teamwork, and any custom external orchestrator.
- The governance rules (scope, verification, circuit breaker) are valuable regardless of who owns the lifecycle.
- Spec grew by ~3.8KB for §7.5 and external mode branches — still well within modern context limits.
- Antigravity adapter gained a dedicated Teamwork section.

## Future Considerations

- As more frameworks emerge (beyond Teamwork), the `external` mode may need framework-specific detection heuristics (currently relies on "were you spawned with a pre-assigned task?").
- Teamwork blueprints may eventually support custom governance hooks — Kramak could be loaded as a standard blueprint module.
- The ALWAYS/HEURISTIC/SKIP classification in §7.5 may need refinement as real-world usage reveals which rules provide value vs. create friction in external mode.
