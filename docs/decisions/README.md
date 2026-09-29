# Architecture Decision Records

This directory captures the strategic reasoning behind Kramak Lite's architectural decisions. Each ADR documents the context, alternatives considered, decision made, and consequences — ensuring the "why" survives even when the people and conversations that produced it don't.

## Format

Each ADR follows a consistent structure:
- **Context** — What problem or opportunity triggered the decision
- **Options Considered** — All alternatives evaluated with pros/cons
- **Decision** — What was chosen and why
- **Consequences** — What changed as a result, including risks

## Index

| ADR | Title | Date | Status |
|---|---|---|---|
| [ADR-001](ADR-001-governance-protocol-evolution.md) | Governance Protocol Evolution | September 2026 | Accepted |
| [ADR-002](ADR-002-external-orchestrator-integration.md) | External Orchestrator Integration (Teamwork Compatibility) | September 2026 | Accepted |
| [ADR-003](ADR-003-version-reset.md) | Version Reset to 0.1.0-dev (Pre-Release Strategy) | September 2026 | Accepted |

## When to Write an ADR

Write an ADR when:
- You're choosing between multiple architectural approaches
- You're making a change that would be hard to reverse
- Future contributors will ask "why was it done this way?"
- The decision involves tradeoffs that aren't obvious from the code alone
