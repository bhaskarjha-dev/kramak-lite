# Contributing to Kramak Lite

Thank you for considering contributing to Kramak Lite! This document explains how to contribute effectively.

## How to Contribute

### Reporting Issues

- **Bug Reports:** Open an issue with a clear description, steps to reproduce, and your environment (IDE, model, OS).
- **Feature Requests:** Describe the problem you're solving, not just the solution you want. Include context on which execution mode (manual/orchestrated/parallel/external) is relevant.

### Proposing Changes

1. **Small fixes** (typos, broken links, minor doc improvements): Open a PR directly.
2. **Spec changes** (anything in `.kramak/KRAMAK-LITE.md`): Open an issue first to discuss. Spec changes affect every user.
3. **Architectural changes** (new execution modes, schema changes, new file conventions): Write an ADR in `docs/decisions/` following the existing format. See [ADR index](docs/decisions/README.md).

### Pull Request Checklist

Before submitting a PR, verify:

- [ ] All cross-references are accurate (section numbers, file paths, line counts)
- [ ] Schema changes are reflected in both `schemas/` and `templates/`
- [ ] Coverage claims in `docs/FULL-KRAMAK-MAPPING.md` are updated if rules changed
- [ ] The CHANGELOG.md has an entry describing the change
- [ ] No secrets, API keys, or personal paths are included

### Code of Conduct

Be respectful, constructive, and specific. Kramak Lite is a specification project — precision and clarity matter more than speed.

## Project Structure

```
.kramak/
├── KRAMAK-LITE.md        ← Core specification (the product)
├── schemas/              ← JSON Schema for state and work items
├── templates/            ← Templates for all runtime artifacts
└── inbox/                ← Communication channel
adapters/                 ← IDE integration adapters
docs/                     ← Architecture, comparison, roadmap, ADRs
```

## Key Principles

1. **Zero runtime dependencies.** Never add a requirement for Python, Node, or any other runtime.
2. **Single-file core.** The spec lives in one file. Resist the urge to split it unless there's demonstrated accuracy degradation.
3. **Schema-template alignment.** Every schema field should have a corresponding template value. Every template should validate against its schema.
4. **Cross-reference integrity.** If you change a section number, adapter line count, rule count, or file path — grep the entire repo for references and update them all.

## Testing Your Changes

Since Kramak Lite is a specification (not code), testing means:

1. **Internal consistency:** Do all cross-references, counts, and claims match?
2. **Schema validation:** Does `state.template.json` validate against `state.schema.json`?
3. **Real-world testing:** Can an AI agent follow your changed instructions accurately?

## License

By contributing, you agree that your contributions will be licensed under the [MIT License](LICENSE).
