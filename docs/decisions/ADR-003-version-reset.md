# ADR-003: Version Reset to 0.1.0-dev (Pre-Release Versioning Strategy)

> **Date:** September 2026  
> **Status:** Accepted and Implemented

---

## Context

Kramak Lite had accumulated internal version numbers from v1.0.0 through v3.0.0 across 7+ iteration cycles during development. However, the project has **zero external users, zero public releases, and zero community validation**. The internal version numbers were development milestone markers, not stability guarantees.

The decision needed: what version to stamp on the first public release?

## Options Considered

### v0.0.1
- **Verdict:** REJECTED. Too tentative. The spec is comprehensive (55KB, 173/173 rules, 4 adapters, strategic intelligence engine). Starting at 0.0.1 undersells the work.

### v0.1.0 ✅ (Chosen)
- **Verdict:** ACCEPTED. The right signal: "Feature-complete initial release, expect changes based on real-world feedback. No stability guarantees yet."
- Reserves v0.2.0, v0.3.0 for iterations based on community feedback.
- Reserves v1.0.0 for when external users have validated the spec across multiple IDEs, models, and project types.
- SemVer 0.y.z convention: anything can change between minor versions.

### v1.0.0
- **Verdict:** REJECTED. Despite substantial internal work, SemVer v1.0.0 is a stability contract: "this is the public API, breaking changes require major version bumps." The spec has zero external validation. The Teamwork collision analysis (ADR-002) revealed a major gap hours after the last internal release — what other environments will reveal similar issues?

### v3.0.0 (Keep Internal Numbering)
- **Verdict:** REJECTED. "v3.0.0 that nobody has ever used" confuses potential adopters. Internal iteration history is valuable for contributors but misleading as a public version.

## Decision

### Version Strategy

- **Current:** `0.1.0-dev` (pre-release development version heading toward v0.1.0)
- **On release:** Drop the `-dev` suffix → `0.1.0`
- **Post-release iterations:** `0.2.0`, `0.3.0`, etc.
- **Stability milestone:** `1.0.0` when the spec is validated by external users

### Pre-Release Suffix Convention

The `-dev` suffix (per SemVer §9) indicates "this is a pre-release version, lower precedence than the associated release." New features (MCP server, plugins, etc.) are developed under `0.1.0-dev`. When everything is ready, the suffix is dropped for the public `0.1.0` release.

### Internal Version History

All prior internal versions (1.0.0 through 3.0.0) are preserved in CHANGELOG.md under a "Pre-Release Development History" section, reframed as internal milestone markers rather than published releases. This preserves the development arc for contributors while eliminating confusion for users.

## Consequences

- All 15+ files updated to reflect `0.1.0-dev` or version-neutral language.
- README badge shows `v0.1.0-dev`.
- CHANGELOG restructured: `[0.1.0-dev]` header at top, all prior versions under "Pre-Release Development History" with `### Internal X.Y.Z` formatting.
- ADR references to internal versions remain as-is (they refer to development milestones, not public releases).
- Freedom to make breaking spec changes between `0.x` minor versions without SemVer violations.
- New features (MCP server, plugins, etc.) are added under `0.1.0-dev` until ready for public release.
