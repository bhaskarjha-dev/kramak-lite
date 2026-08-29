---
id: WI-NNN
title: ""
batch: 1
status: queued
detail_tier: guided
files_targeted: []
depends_on: []
acceptance_criteria: []
created_at: ""
completed_at: null
---

## Intent

[Why this change matters. What user value is created. What breaks if done incorrectly.]

## Key Files

[Specific files and line ranges the executor must read before starting.]

## Specification — 🔴 Guided (Zero Autonomy)

Follow the BEFORE/AFTER replacements below VERBATIM. Zero deviation.

### Change 1: [description]

**File:** `path/to/file.ts`

**BEFORE** (grep-verified, unique match):
```
[Exact code that currently exists — verified via grep before writing this WI]
```

**AFTER:**
```
[Exact replacement code — drop-in replacement for the BEFORE block]
```

### Change 2: [description]
...

## Constraints

[What NOT to do. Explicit boundaries, forbidden patterns, scope limits.]

## Verification

```bash
# Exact commands to validate:
npm test
npx tsc --noEmit
```

<!-- The section below is auto-populated by the executor on failure. Do not fill manually. -->
<!--
## Failure Diagnosis

- **Category:** [code-drift | verification-fail | scope-exceeded | dependency-missing | ambiguous-spec | tool-error]
- **What happened:** [root cause explanation]
- **Error Trajectory:**
  - Attempt 1: [N] errors - [description]
  - Attempt 2: [N] errors - [description]
- **Suggested fix:** [recommend tier elevation if spec was ambiguous]
-->
