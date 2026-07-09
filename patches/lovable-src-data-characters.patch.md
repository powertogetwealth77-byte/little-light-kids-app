# Patch — Align `src/data/characters.ts` to canonical Supabase env

Apply this in the Lovable public app project `truth-seedlings`.

## Problem

The file currently hardcodes:

```ts
const BASE = "https://zeynbogdijlylhftqbvz.supabase.co/storage/v1/object/public/character-bible";
```

But the project env and `supabase/config.toml` point to:

```text
pohlehtgqlsrvmnlsrkv
```

## Replace the hardcoded BASE line with this

```ts
const SUPABASE_URL = import.meta.env.VITE_SUPABASE_URL as string | undefined;

if (!SUPABASE_URL) {
  throw new Error("Missing VITE_SUPABASE_URL for Little Light Kids character assets");
}

const BASE = `${SUPABASE_URL.replace(/\/$/, "")}/storage/v1/object/public/character-bible`;
```

## Preserve everything else

Do not change:

- `CHARACTER_IMAGE_URLS`
- `Character` type
- `CHARACTERS` array
- character names
- copy
- pricing
- routes
- Supabase functions

## Verify before deploying

Confirm the canonical Supabase storage bucket contains every referenced asset:

- `character-bible/Zeke Strong.png`
- `character-bible/Kai Cross.png`
- `character-bible/Luma Grace.png`
- `character-bible/Jude Brave.png`
- `character-bible/Sunny Joy.png`
- `character-bible/Toby Truth.png`
- `character-bible/Nia Kind.png`
- `character-bible/Max Watch.png`
- `character-bible/King Light Aka Jesus.jpeg`
- `character-bible/The Whisper Aka The Accuser.png`

Then run:

```bash
npm run build
npm run test
```
