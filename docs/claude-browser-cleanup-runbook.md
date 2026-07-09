# Claude Browser Cleanup Runbook

Use this when direct connector access cannot complete the cleanup.

## Mission

Cleanly align Little Light Kids™ across Lovable, GitHub, and Supabase without mixing it with Seer AI, RFMG, DOMOS, Christian Surfers, or Little Light Forge internal tooling.

## Do not do yet

- Do not run migrations.
- Do not delete Supabase tables.
- Do not deploy Edge Functions.
- Do not change production environment variables.
- Do not copy Little Light Forge internal screens into the public app.

## Step 1 — Verify Lovable project

Open Lovable and locate:

- Project slug/name: `truth-seedlings`
- Display name: `Little Light Kids`
- Published URL: `https://truth-seedlings.lovable.app`

Confirm this is the public children’s app.

## Step 2 — Verify Supabase ref

In Lovable project settings / Supabase / environment variables, find:

- `VITE_SUPABASE_URL`
- `VITE_SUPABASE_PUBLISHABLE_KEY` or anon key

Do not reveal or paste secrets. Only compare the project ref inside the URL.

Expected ref from prior repo context:

- `pohlehtgqlsrvmnlsrkv`

Known mismatch from prior dashboard audit:

- `zeynbogdijlylhftqbvz`

If Lovable points to the wrong ref, stop and report.

## Step 3 — Export code

Export or clone the Lovable project code from `truth-seedlings`.

The public app should contain Vite/React files such as:

- `package.json`
- `src/App.tsx`
- `src/pages/Index.tsx`
- `src/pages/Characters.tsx`
- `src/pages/member/Library.tsx`
- `src/pages/member/Reader.tsx`
- `src/integrations/supabase/client.ts`
- `supabase/migrations/*`
- `supabase/functions/*`

## Step 4 — Push to GitHub

Target repo:

- `powertogetwealth77-byte/little-light-kids-app`

Before pushing, confirm the repo does not contain app code already. If it only contains source-of-truth docs/data, then add the public app code on a new branch.

Suggested branch:

- `import/lovable-truth-seedlings-public-app`

## Step 5 — Cleanup scan

Search the imported code for off-brand terms:

- Seer
- Seer AI
- dream
- dream decode
- Watchroom
- RFMG
- Revival Fire
- DOMOS
- Christian Surfers
- Shopify
- case-david
- case-jennifer
- case-linda

Remove or quarantine anything unrelated to the public Little Light Kids app.

## Step 6 — Keep / remove / separate rules

Keep in public app:

- Little Light Kids pages
- Parent dashboard
- Library
- Reader
- Prayers
- Characters
- Checkout/subscription flow if actively used
- Public customer-facing assets

Separate into Little Light Forge only:

- Book Factory internals
- Production operator dashboard
- Admin-only creation workflows
- Character registry admin tooling, unless protected behind admin routes

Remove if unused/off-brand:

- old client case-study assets
- unrelated funnel proof graphics
- unrelated ministry or agency references
- stale project refs

## Step 7 — Verification

Run:

```bash
npm install
npm run build
npm run lint
npm run test
```

Then verify:

- App loads
- Public routes work
- Member routes are protected
- Library and reader work
- Character pages are child-safe
- No unrelated brand names appear
- Supabase ref is correct

## Final rule

Little Light Kids™ must become its own clean loop:

Input: approved stories, characters, prayers, parent-safe content
Trigger: child/parent opens app or story
Action: read, pray, choose, favorite, complete
Result: child gets a first win in faith/character
Data: reads, completions, favorites, parent feedback
Improvement: better stories, better characters, better follow-up
Repeat: stronger library, stronger trust, stronger retention
