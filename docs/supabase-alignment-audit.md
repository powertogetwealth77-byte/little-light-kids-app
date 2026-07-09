# Supabase Alignment Audit — Little Light Kids™

## Date

2026-07-09

## Scope

Lovable public app candidate:

- Project id: `a74f0a65-d227-4ecd-9502-3134391d5329`
- Project slug/name: `truth-seedlings`
- Display name: `Little Light Kids`
- Published URL: `https://truth-seedlings.lovable.app`

Internal app to keep separate:

- `Little Light Forge` / Book Factory

## What was inspected

- Lovable database status
- Project environment file refs, without copying secrets
- Supabase config file
- Supabase generated types
- Supabase Edge Functions
- Public character data file
- Public landing/checkout files

## Confirmed Supabase state

The Lovable project has Supabase enabled.

The public app config points to this project ref:

- `pohlehtgqlsrvmnlsrkv`

Evidence inside Lovable project:

- `.env` has `VITE_SUPABASE_PROJECT_ID` set to `pohlehtgqlsrvmnlsrkv`.
- `.env` has `VITE_SUPABASE_URL` set to the same ref.
- `supabase/config.toml` has `project_id = "pohlehtgqlsrvmnlsrkv"`.
- `src/integrations/supabase/client.ts` uses `VITE_SUPABASE_URL` and `VITE_SUPABASE_PUBLISHABLE_KEY`.

## Critical mismatch found

`src/data/characters.ts` hardcodes character asset URLs from a different Supabase project ref:

- `zeynbogdijlylhftqbvz`

This means the app is configured to use one Supabase project for auth/database/functions, while character images are being loaded from another Supabase project's public storage bucket.

## Impact

This creates a split-brain risk:

1. Auth, database, subscriptions, books, child profiles, and Supabase functions use `pohlehtgqlsrvmnlsrkv`.
2. Character public images use `zeynbogdijlylhftqbvz`.
3. If the old storage project is deleted or made private, the public app loses character images.
4. If assets are updated in the canonical project, the app may not show them because it is pulling from the wrong project.
5. Future agents may copy the wrong Supabase ref into GitHub or Lovable.

## Recommended live app patch

Patch only `src/data/characters.ts` in Lovable:

```ts
const SUPABASE_URL = import.meta.env.VITE_SUPABASE_URL as string | undefined;

if (!SUPABASE_URL) {
  throw new Error("Missing VITE_SUPABASE_URL for Little Light Kids character assets");
}

const BASE = `${SUPABASE_URL.replace(/\/$/, "")}/storage/v1/object/public/character-bible`;
```

Then preserve the rest of the file's exports and asset path names.

## Important verification before patch goes live

Before replacing the hardcoded storage ref, confirm the canonical Supabase project contains the public bucket and files:

- Bucket: `character-bible`
- Files such as:
  - `Zeke Strong.png`
  - `Kai Cross.png`
  - `Luma Grace.png`
  - `Jude Brave.png`
  - `King Light Aka Jesus.jpeg`
  - `The Whisper Aka The Accuser.png`

If the canonical bucket does not contain those files, copy the assets from the old storage project into the canonical project first, then apply the code patch.

## Supabase schema quality

The generated Supabase types show a real Little Light Kids public/app schema, including:

- `books`
- `book_assets`
- `book_content`
- `book_characters`
- `characters`
- `children`
- `content_master`
- `daily_light`
- `parent_alerts`
- `prayer_templates`
- `scripture_cards`
- `subscriptions`
- `user_progress`
- `user_roles`

There are also legacy tables prefixed with `_legacy_`. These should not be deleted yet. They should be reviewed and archived only after confirming no active code path depends on them.

## Payment finding

Stripe appears to be the active payment system for the public app:

- `src/lib/stripe.ts`
- `src/pages/Checkout.tsx`
- `supabase/functions/create-checkout/index.ts`
- `supabase/functions/payments-webhook/index.ts`

A Shopify webhook handler also exists:

- `supabase/functions/shopify-webhook-handler/index.ts`

This should be treated as stale or future-only until proven active. Do not delete it yet. Mark it for review because active checkout code is Stripe-based.

## Live-write limitation

Direct Lovable write attempt failed with:

- `403 insufficient_scope: Scope 'projects:write' is required for this operation`

Therefore, the live Lovable app was not modified by this audit. Claude Browser or a Lovable session with write scope must apply the patch.

## Alignment rule going forward

Canonical Supabase ref for the public Little Light Kids app is:

- `pohlehtgqlsrvmnlsrkv`

The `zeynbogdijlylhftqbvz` ref should be treated as a legacy asset source until assets are migrated.

Do not delete `zeynbogdijlylhftqbvz` or make its buckets private until all referenced assets have been copied and the public app build has been verified.
