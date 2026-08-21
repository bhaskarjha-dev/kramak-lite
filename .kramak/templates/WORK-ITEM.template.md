---
id: WI-NNN
title: ""
batch: 1
status: queued
detail_tier: directed  # guided | directed | outcome
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

## Specification

[What to change, scaled by detail_tier:]
- Guided: Exact BEFORE/AFTER code blocks with grep-verified line references
- Directed: Intent + target files + interfaces + constraints (executor owns HOW)
- Outcome: Acceptance criteria only (executor owns design)

## Constraints

[What NOT to do. Explicit boundaries, forbidden patterns, scope limits.]

## Verification

[Exact commands to validate the change:]
```bash
# Example:
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
