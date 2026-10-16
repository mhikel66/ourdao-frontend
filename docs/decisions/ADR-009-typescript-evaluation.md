# ADR-009: TypeScript 7 and @types/node Alignment Evaluation

**Date:** 2026-10-16  
**Status:** Accepted  
**Deciders:** Maintainers  
**Issue:** #386 (closes #386)

## Context

The repository is on TypeScript 5.9 while TypeScript 7.0 is available, and `@types/node` was previously targeting `^20`. Issue #386 proposed evaluating TypeScript 7 and `@types/node` alignment to prevent accumulating an overly large jump in compiler versions and runtime type declarations.

## Evaluation & Decision

1. **`@types/node` updated to `^26`:**
   - Node type definitions have been upgraded to `^26`, fully aligning with modern runtime Node.js LTS versions and tooling dependencies without breaking compiler diagnostics.

2. **TypeScript 7 Upgrade Deferred:**
   - Next.js `16.3.6` and `eslint-config-next` officially support and target TypeScript `^5.x`.
   - TypeScript 7 introduces breaking compiler changes, stricter generic inference, and breaking adjustments to config schema and TS build plugins used by Next.js's Turbopack and internal type generators.
   - Upgrading to TypeScript 7 causes upstream compiler and plugin incompatibilities with the current Next.js 16 toolchain.
   - **Decision:** Keep TypeScript pinned to `^5` (TypeScript 5.9.x) with `strict: true` preserved across the codebase.

3. **Blockers & Re-evaluation Trigger:**
   - Upstream support for TypeScript 7 in Next.js core and `@next/eslint-plugin` / `eslint-config-next`.
   - Re-evaluate the TypeScript 7 migration once Next.js releases official support for TypeScript 7 in a future major or minor release.

## Consequences

- `npm run typecheck` (`tsc --noEmit`) passes cleanly with full type safety under TypeScript 5.9.
- `@types/node` provides modern Node.js API typings.
- Next.js development and production Turbopack builds remain stable and fully compatible.
