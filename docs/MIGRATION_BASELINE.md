# Little Light Kids™ — Lovable Migration Baseline

**Baseline date:** 2026-09-09  
**Migration branch:** `migration/lovable-baseline-2026-09-09`  
**Destination repository:** `powertogetwealth77-byte/little-light-kids-app`  
**Status:** Migration scaffold created; full Lovable source import still pending verification.

## Verified source checkpoint

The latest verified completed Lovable edit at migration setup is:

- Commit: `7e342cb69ade7f28cfca64cb0343c821aa52b7cd`
- Message: `Enforced checkout price guard`
- Completed: 2026-09-09T03:43:05Z

Immediately preceding verified source edits include:

- `8ef470be4a90de0b5bd3acf6297e744bb1eab10c` — Corrected pricing structure
- `f5071496bd893fcbbad430e0d1bc568d3bb6730f` — Updated pricing schema & copy
- `8e8fcce7ad449ee8a6b980fc7d04fc91e043da73` — Refined comparison copy
- `2afaf3188b3b915630e923407cb09b4909b366b0` — Updated landing page to final

## Verified application stack

The Lovable project currently includes a Vite + React 18 + TypeScript application with Tailwind/shadcn/Radix UI, React Router, TanStack Query, Supabase, Stripe, Vitest, and ESLint.

The source project contains application code under `src/`, public assets under `public/`, character assets, checkout/subscription components, member/admin surfaces, and project configuration/lockfiles.

## Migration acceptance gate

The migration is **not complete** until all of the following are true:

- [ ] Complete Lovable source tree is present in this branch
- [ ] Required binary/image assets are present and render correctly
- [ ] No secret-bearing `.env` file is committed
- [ ] `package.json` and lockfile are present
- [ ] `npm ci` succeeds
- [ ] `npm run lint` succeeds or all pre-existing lint failures are documented
- [ ] `npm run test` succeeds or all pre-existing failures are documented
- [ ] `npm run build` succeeds
- [ ] Landing page visually matches the verified Lovable baseline
- [ ] Established character assets render correctly
- [ ] Current pricing is consistent across funnel and checkout
- [ ] Server-side checkout price guard is preserved
- [ ] Authentication/member access is smoke-tested
- [ ] Checkout success/cancel/error paths are smoke-tested
- [ ] Supabase/RLS assumptions are reviewed before any policy change
- [ ] Diff reviewed for accidental deletions or generated junk
- [ ] Product owner explicitly approves merge

## Source-of-truth transition

Until this checklist is completed and the migration branch is merged, the verified Lovable project remains the source baseline.

After merge approval:

1. `main` becomes the engineering source of truth.
2. All feature work happens on `feature/*`, `fix/*`, `refactor/*`, `migration/*`, or `chore/*` branches.
3. Codex/AI agents follow `AGENTS.md`.
4. Changes reach `main` only through reviewed pull requests.
5. A Git tag/release should mark this exact baseline as `lovable-baseline-2026-09-09`.
6. Lovable becomes optional tooling rather than the authoritative codebase.

## Do not do during migration

- Do not overwrite `main` with an unverified export.
- Do not copy secret values from Lovable `.env` files into GitHub.
- Do not rewrite pricing, checkout, auth, subscriptions, character names, or brand copy as part of the migration.
- Do not remove historical branches until the new baseline is proven stable.
