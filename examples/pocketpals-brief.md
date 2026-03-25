# BRIEF.md — PocketPals
> Derived from Operating Bible v5. Active as of March 2026.

---

## 1. PRODUCT IN ONE SENTENCE

PocketPals is an AI voice companion for children ages 3–12 — Buddy the Inkfox grows richer with every conversation, gives parents full visibility without surveillance, and sends kids outside on real-world missions. Day-one job: child has their first conversation with Buddy and Buddy visibly "comes to life" as their fur fills in.

---

## 2. THE ONE METRIC THAT PROVES SUCCESS IN 90 DAYS

- **Primary metric:** Child returns for a Session 2 within 72 hours of Session 1
- **How we measure it:** PostHog `session_started` events — child_id has ≥2 events within 72h window
- **What it is NOT:** Not daily active users. Not total sessions. Not parent signups. Retention in the first 72 hours proves the "Buddy Remembers" differentiator actually lands emotionally — everything else is downstream of that.

---

## 3. WHAT'S ALREADY BUILT

- **Repo:** `C:\Users\bradp\dev\kidtalk`
- **Current state:** Phase 4 of 7. Auth works (Supabase Auth). Schema exists. Buddy voice conversation core works. Bedtime Mode shipped. Parent Room partial. Lesson content 40% complete. Rive integration spec written — waiting on buddy.riv from animator.
- **Key files CC should read first:**
  - `POCKETPALS_Operating_Bible_v5.html` — full product spec
  - `SPEC-rive-character-integration-2026-03-24.md` — Rive animation integration (6 micro-prompts)
  - `memory/pocketpals-operating-bible.md` — location + update workflow
- **What is NOT built yet:** Rive character animation (waiting on .riv file), full lesson content library, Educator Portal, kidSAFE certification submission

---

## 4. WHO MATTERS ON DAY ONE

- **Primary user on day one:** The child (ages 3–12) — Buddy must feel real and remembered in Session 1
- **Secondary user:** The parent — Parent Room must show enough to trust the product immediately (session summary, mood signal, time spent)
- **Deferred:** Educators, extended family, the Educator Portal — Layer 3

---

## 5. PAYMENTS

- **Payment processor:** RevenueCat (iOS/Android subscriptions)
- **Credentials owner:** NuStack holds the RevenueCat account
- **What we're collecting in v1:** Free tier (10 sessions/month) + Family plan ($12/mo, 5 children, unlimited)
- **What is explicitly deferred:** Annual billing, gifting, family sharing via App Store family — all post-launch

---

## 6. AUTH SCOPE

- **Auth provider:** Supabase Auth
- **Scope:** Single parent account → multiple child profiles (not Clerk orgs — different children under one parent)
- **Session model:** Parent authenticates. Child profiles are sub-accounts — no separate auth, handed off from Parent Room via single button
- **What's deferred:** Educator accounts, school district licenses — Layer 3

---

## 7. LAYER CONSTRAINTS

| Layer | What's in scope | What's explicitly out |
|-------|-----------------|----------------------|
| Layer 1 (day one) | Buddy conversation, Buddy Remembers (memory), Parent Room (summary + alerts), Bedtime Mode | Everything else |
| Layer 2 (week one) | Buddy Missions, Buddy Grows With You (age bands), Parent voice narration, Buddy Cares (emotional alerts) | Educator Portal, social features |
| Layer 3 (future) | Deep story library, family sharing, kidSAFE submission, Educator Portal, API for schools | Dark patterns (streaks, shame), advertising, surveillance transcripts |

---

## 8. DEPLOY TARGET

- **Platform:** EAS (Expo Application Services) — iOS + Android. PWA planned.
- **Project:** `pocketpals-app` in EAS
- **Env vars already set:** `SUPABASE_URL`, `SUPABASE_ANON_KEY`, `ANTHROPIC_API_KEY`, `EXPO_PUBLIC_SUPABASE_URL`
- **Env vars CC needs to add:** RevenueCat keys when billing goes live
- **Preview URL:** Internal TestFlight + Android internal test

---

## 9. TECH STACK (exact)

```
Framework:      Expo SDK 52 + React Native
Language:       TypeScript — strict mode, no 'any'
Database:       Supabase — Postgres + RLS on every table
Auth:           Supabase Auth (not Clerk — mobile app, pre-Clerk)
State:          Zustand (local) + React Query (server)
Forms:          React Hook Form + Zod
Payments:       RevenueCat
AI:             Claude API via Supabase Edge Function (server-side proxy)
Animations:     Rive (pending buddy.riv) + React Native Reanimated
Error tracking: Sentry
Analytics:      PostHog
```

**Non-negotiable rules:**
- ANTHROPIC_API_KEY never in client bundle — always proxied through Edge Function
- RLS enabled on all child profile tables — COPPA requirement
- No verbatim transcript storage — emotional summaries only
- Age-gated content — every AI prompt includes child's age band in system prompt

---

## 10. AUTONOMOUS OPERATIONS PERMISSIONS

- **Can CC create new files without asking?** Yes within src/
- **Can CC modify the database schema?** Yes with migration file — must update RLS policy in same migration
- **Can CC push to main?** Ask first — app store builds triggered from main
- **Can CC install new packages?** Yes within the existing Expo ecosystem. Ask before adding native modules.

---

## 11. ACTIVE SESSION CONTEXT

> Update at start of each session.

- **Today's goal:** [Replace each session]
- **Acceptance criteria:**
  - GIVEN [state] WHEN [action] THEN [result]
- **Files in play today:** [Replace each session]
- **Blockers:** Buddy.riv file not yet received from Upwork animator — Rive integration blocked
- **What NOT to touch:** Production child profile data. Bedtime Mode — already QA'd and stable.

---

## 12. MEMORY FILES CC READS EVERY SESSION

- `memory/pocketpals-operating-bible.md` — location + update workflow for the Operating Bible
- `memory/buddy-rive-animator-plan.md` — Rive integration status + animator brief
- `POCKETPALS_Operating_Bible_v5.html` — full product spec (section reference, not full read)
- `SPEC-rive-character-integration-2026-03-24.md` — active build spec if working on Rive

---

## COMMIT FORMAT

```bash
git add [files] && git commit -m "feat(buddy): [what was built] — [child-facing outcome]" && git push
```

---

## VERSION

| Version | Date | What changed |
|---------|------|-------------|
| v1.0 | 2026-03-24 | Initial brief derived from Operating Bible v5 |
