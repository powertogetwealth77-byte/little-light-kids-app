# Little Light Kids™

Official source-of-truth repository for the Little Light Kids™ public children’s story platform.

## Current cleanup status

This repo was previously empty. It is now being seeded with brand rules, project alignment notes, character data, and approved story data so Little Light Kids has its own GitHub home instead of being mixed with Seer AI, RFMG, DOMOS, Christian Surfers, or internal Book Factory tooling.

## Canonical project identity

- Brand: Little Light Kids™
- Public app / Lovable slug found: `truth-seedlings`
- Lovable display name found: `Little Light Kids`
- Public URL found in Lovable: `https://truth-seedlings.lovable.app`
- Separate internal tooling: `Little Light Forge` / Book Factory
- GitHub repo target: `powertogetwealth77-byte/little-light-kids-app`

## Brand mission

Little Light Kids™ is a Jesus-centered children’s story world that helps kids choose truth, courage, kindness, forgiveness, and faith through safe, emotionally strong, story-driven content.

Core chant / phrase:

> Jesus is the Light.

Core decision language:

> Choose the Light.

## Hard separation rules

This repo must not contain code, copy, database schema, or product positioning from:

- Seer AI
- Revival Fire Ministries Global / RFMG
- DOMOS
- Christian Surfers
- Little Light Forge internal-only Book Factory screens, except for documented data contracts or approved export formats

## Repo purpose

This repo should become the clean GitHub source for:

- Public Little Light Kids app code
- Supabase migrations and functions for the public app only
- Seed data for books, characters, prayers, and library content
- Brand guardrails
- Safe Claude/Codex/browser-agent instructions
- Deployment and verification docs

## Immediate rule

Do not run Supabase migrations, delete tables, deploy Edge Functions, or change production env variables until Lovable, GitHub, and Supabase all point to the same confirmed project ref.
