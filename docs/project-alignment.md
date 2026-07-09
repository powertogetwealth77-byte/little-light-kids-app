# Project Alignment Notes

## Known current state

The empty GitHub repo has been confirmed as:

- `powertogetwealth77-byte/little-light-kids-app`
- Default branch: `main`
- Prior size: `0`

Lovable search found the real public app candidate:

- Lovable project id: `a74f0a65-d227-4ecd-9502-3134391d5329`
- Lovable name/slug: `truth-seedlings`
- Lovable display name: `Little Light Kids`
- Published URL: `https://truth-seedlings.lovable.app`
- Tech stack: Vite + React + shadcn + TypeScript
- Database: Supabase enabled

Lovable also found a separate internal project:

- Display name: `Little Light Forge`
- Purpose: internal Book Factory / production tooling
- It should not be treated as the public kids app.

## Critical Supabase rule

Do not run migrations, delete tables, deploy Edge Functions, or change production settings until these three points match:

1. Lovable `VITE_SUPABASE_URL`
2. GitHub repo `supabase/config.toml` or env docs
3. Supabase dashboard Project Ref

Known expected/canonical project ref from prior repo context:

- `pohlehtgqlsrvmnlsrkv`

Known wrong/mismatched dashboard ref from prior audit:

- `zeynbogdijlylhftqbvz`

Decision rule:

- If Lovable, GitHub, and Supabase all point to `pohlehtgqlsrvmnlsrkv`, proceed with migration verification.
- If any system points to `zeynbogdijlylhftqbvz`, pause and align before touching production data.

## Public app files found in Lovable

The Lovable project contains public-app files such as:

- `src/pages/Index.tsx`
- `src/pages/Auth.tsx`
- `src/pages/Characters.tsx`
- `src/pages/CharacterProfile.tsx`
- `src/pages/member/Dashboard.tsx`
- `src/pages/member/Library.tsx`
- `src/pages/member/Reader.tsx`
- `src/components/member/RequireAuth.tsx`
- `src/components/member/RequireSubscription.tsx`
- `src/integrations/supabase/client.ts`
- `supabase/functions/create-checkout/index.ts`
- `supabase/functions/payments-webhook/index.ts`
- `supabase/migrations/*`

## Potential cleanup issue

The Lovable file list also showed unrelated-looking assets:

- `src/assets/case-book-mockup.webp`
- `src/assets/case-david.webp`
- `src/assets/case-hero-jennifer.webp`
- `src/assets/case-jennifer.webp`
- `src/assets/case-linda.webp`

These may be old case-study or funnel assets. Claude Browser should inspect and remove them if unused or off-brand.

## Safe sync strategy

1. Export the real Lovable `truth-seedlings` project code.
2. Verify it is the public Little Light Kids app, not Little Light Forge.
3. Verify the Supabase project ref before copying migrations.
4. Push public-app code into this GitHub repo.
5. Keep Book Factory/internal admin production code separate.
