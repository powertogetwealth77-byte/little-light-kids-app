## What changed

Describe the requested outcome and the implementation in plain English.

## Scope

- [ ] Change is limited to the requested feature/fix
- [ ] Unrelated files were not modified
- [ ] Existing Little Light Kids branding, characters, and approved copy were preserved unless explicitly in scope

## High-risk surfaces

Check any touched area:

- [ ] Authentication / authorization
- [ ] Stripe / checkout / subscriptions
- [ ] Supabase / database / RLS
- [ ] Parent or child data
- [ ] Webhooks / email / external APIs
- [ ] Pricing / plan entitlements
- [ ] None of the above

If a high-risk surface changed, explain the risk and verification performed.

## Verification

- [ ] `npm ci`
- [ ] `npm run lint`
- [ ] `npm run test`
- [ ] `npm run build`
- [ ] Affected UI checked on mobile
- [ ] Affected UI checked on desktop
- [ ] Success path verified where applicable
- [ ] Failure/edge path verified where applicable

List anything that could not be run or verified.

## Regression check

Confirm that pricing, checkout, authentication, subscription access, routing, and existing character/assets remain unchanged unless intentionally modified.

## Merge gate

- [ ] Diff reviewed
- [ ] No secrets or `.env` values committed
- [ ] No known critical regression
- [ ] Product owner approved merge
