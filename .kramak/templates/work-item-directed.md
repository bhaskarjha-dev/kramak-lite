---
id: WI-NNN
title: ""
batch: 1
status: queued
detail_tier: directed
files_targeted: []
depends_on: []
acceptance_criteria: []
created_at: ""
completed_at: null
---

## Intent

[Why this change matters. What breaks if done incorrectly. Include your chosen approach and why you chose it over alternatives.]

## Key Files

[Files the executor must read before starting, with brief context on existing patterns:]
- `path/to/file.ts` — [what pattern exists here, what to look for]

## Specification — 🟡 Directed (You Own the HOW)

**Goal:** [What this change accomplishes]

**Interfaces/Types to implement or modify:**
```typescript
// Key interfaces the executor must create or modify
```

**Integration points:**
- [Where this connects to existing code]

**Edge cases to handle:**
- [Specific scenarios the executor must address]

## Constraints

[What NOT to do. Explicit boundaries, forbidden patterns, scope limits.]
- Do NOT change [specific thing]
- Must follow existing [pattern name] pattern
- Keep backward compatibility with [specific interface]

## Verification

```bash
# Exact commands to validate:
npm test
npx tsc --noEmit
```
