# Little Light Kids™ — AI Engineering Operating Rules

This repository is the permanent engineering source of truth for Little Light Kids™ once the Lovable baseline migration is verified and merged.

## Mission and product integrity

Little Light Kids is a Jesus/Bible-centered children's product. Preserve established brand identity, approved characters, pricing, funnel logic, and parent/child safety boundaries. Bible quotations used in product content default to KJV unless the product owner explicitly directs otherwise.

## Non-negotiable operating rules

1. Never make feature work directly on `main`.
2. Inspect the existing implementation before editing it.
3. Make the smallest reliable change that fully solves the requested problem.
4. Do not rewrite approved copy, pricing, character names, artwork references, checkout logic, authentication, subscription logic, or database policies unless the task explicitly requires it.
5. Never invent new Little Light Kids characters or silently replace established characters/assets.
6. Never hard-code secrets, API keys, Stripe secrets, Supabase service-role keys, tokens, passwords, or private customer/child data.
7. Never commit `.env` files containing secrets. Use `.env.example` for variable names only.
8. Treat child data, parent data, authentication, billing, subscriptions, Stripe, Supabase/RLS, admin permissions, and webhooks as high-risk surfaces. For these areas, inspect dependencies and call sites before edits and add/adjust tests.
9. Do not modify unrelated files just to make a diff look cleaner.
10. Do not delete working functionality, assets, migrations, or content unless the product owner explicitly requests removal.
11. Preserve mobile responsiveness and accessibility when changing UI.
12. Prefer existing design-system components and patterns over introducing one-off styling or dependencies.
13. Do not add a package when the existing stack can reasonably solve the problem.
14. Before finishing, run the relevant validation commands and report exactly what passed, failed, or could not be run.
15. Never claim a test, build, deployment, payment, email, webhook, or database change succeeded unless it was actually verified.

## Branching

Use descriptive branches:

- `feature/<short-name>` for product work
- `fix/<short-name>` for bugs
- `refactor/<short-name>` for internal restructuring
- `migration/<short-name>` for migrations
- `chore/<short-name>` for maintenance

`main` must remain production-ready. Changes should reach `main` through a reviewed pull request after validation.

## Required workflow for every meaningful task

### 1. Diagnose
- Read the relevant files and adjacent dependencies.
- Identify the existing behavior and the actual bottleneck/bug.
- Confirm whether the request touches auth, payments, data, subscriptions, routing, SEO, analytics, or child safety.

### 2. Plan
- State the files expected to change.
- State risks and test strategy.
- Avoid scope creep.

### 3. Implement
- Work only on the task branch.
- Preserve established behavior outside the requested scope.
- Reuse existing components/tokens/utilities where appropriate.

### 4. Verify
When available, run:

```bash
npm ci
npm run lint
npm run test
npm run build
```

For UI work, also verify the affected path at mobile and desktop widths. For checkout/auth/subscription work, verify both success and failure paths.

### 5. Report
Summarize:
- what changed
- files changed
- tests/build results
- remaining risks
- any manual verification still needed

Do not merge unless explicitly authorized.

## Current stack baseline

The Lovable source project currently uses Vite, React 18, TypeScript, shadcn/Radix UI, Tailwind CSS, React Router, TanStack Query, Supabase, Stripe, Vitest, and ESLint. Preserve compatibility with the existing stack unless an architectural change is explicitly approved.

## Product-specific guardrails

- Keep pricing consistent across landing pages, pricing pages, checkout, upgrade paths, and server-side price validation.
- Server-side billing validation is authoritative; UI pricing must never be treated as the security boundary.
- Preserve the established Little Light Kids character system and source artwork.
- Never expose parent or child private data in logs, client-side secrets, analytics payloads, or public pages.
- Any database policy/RLS change requires explicit inspection of read/write access for anonymous, authenticated, parent/member, and admin roles.
- Any checkout change requires checking product/price mapping, subscription state, success/cancel return paths, and webhook assumptions.

## Migration baseline

The migration branch `migration/lovable-baseline-2026-09-09` is reserved for importing and validating the final Lovable baseline before `main` becomes authoritative. Do not use it for unrelated feature work.
