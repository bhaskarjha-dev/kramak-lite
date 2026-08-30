# Project Conventions & Architecture Context

> This file captures project-specific conventions, architecture decisions, and developer commands.
> Autonomous agents read this during project discovery and orientation.

## 1. Tech Stack & Toolchain
- **Language / Runtime:** [e.g. TypeScript / Node.js 20+, Python 3.12, Rust 1.80+]
- **Frameworks:** [e.g. Next.js App Router, FastAPI, Actix-web]
- **Package Manager:** [e.g. pnpm, bun, uv, cargo]
- **Build Command:** `[e.g. pnpm build / cargo build]`
- **Check / Lint Command:** `[e.g. pnpm tsc --noEmit && pnpm biome check / ruff check .]`
- **Test Command:** `[e.g. pnpm test / pytest / cargo test]`

## 2. Directory Structure
```
[src/]               -> Core application source code
  [app/ | api/]      -> Routing, endpoints, and handlers
  [components/]      -> Reusable UI/logic components
  [lib/ | core/]     -> Utilities, database clients, helpers
  [types/ | models/] -> Shared schemas, types, domain models
[tests/]             -> Integration and end-to-end test suites
[docs/]              -> Project documentation and specifications
```

## 3. Architecture & Code Patterns
- **Data Access:** [e.g. Prisma / SQLAlchemy / Drizzle / raw SQL]
- **State Management:** [e.g. React server actions / Zustand / Redux]
- **Error Handling:** [e.g. Result types, structured JSON envelopes, custom error classes]
- **API Style:** [e.g. REST JSON, GraphQL, tRPC, gRPC]

## 4. Key Invariants & Rules
- Never commit unverified code or broken builds.
- Reference environment variables via `.env.example` — never hardcode secrets.
- Keep components and functions focused, typed, and testable.
