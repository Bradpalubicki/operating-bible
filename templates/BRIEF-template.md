# BRIEF.md — [Product Name]
> Claude Code reads this at the start of every session.
> Keep it short, honest, and outcome-first.
> This is NOT the Operating Bible — that lives at .claude/OPERATING_BIBLE.html
> This IS the minimum CC needs to build confidently without asking.

---

## 1. PRODUCT IN ONE SENTENCE

[What it is, who it's for, what day-one job it does.]

**Good:** "A solo esthetician needs to see today's appointments and collect payment without leaving the app — that's it for day one."

**Bad:** "A booking system with calendar, reminders, and staff management."

---

## 2. THE ONE METRIC THAT PROVES SUCCESS IN 90 DAYS

> Without this, CC invents the wrong KPI and optimizes for the wrong thing.

- **Primary metric:** [e.g., "50 bookings completed end-to-end without support tickets"]
- **How we measure it:** [e.g., PostHog event `booking_completed` + `payment_collected` in same session]
- **What it is NOT:** [e.g., "Not daily active users — we don't care yet. We care that the core loop works."]

---

## 3. WHAT'S ALREADY BUILT

> Is this a new engine or extending an existing one?

- **Repo:** [alias or URL — e.g., `nustack/esti-app` or local path]
- **Current state:** [e.g., "Auth works. Supabase schema exists. Home screen stubbed. Nothing else."]
- **Key files CC should read first:**
  - `[path]` — [what it is]
  - `[path]` — [what it is]
- **What is NOT built yet:** [Be explicit. If CC doesn't know, it will assume it needs to build it.]

---

## 4. WHO MATTERS ON DAY ONE

> Audience map. Never build for one audience.

- **Primary user on day one:** [e.g., "The solo esthetician — not her clients, not the admin, just her."]
- **Secondary user (deferred):** [e.g., "Clients get a booking link — but we're not building client accounts yet."]
- **NuStack agency view:** [What does the agency dashboard need to show for this engine?]

---

## 5. PAYMENTS

> Ambiguity here causes builds that can't go live.

- **Payment processor:** [Square / Stripe / RevenueCat / none yet]
- **Credentials owner:** [e.g., "Client holds the Square account. Credentials in Vercel env as SQUARE_ACCESS_TOKEN."]
- **What we're collecting in v1:** [e.g., "Card on file only — no live charges yet."]
- **What is explicitly deferred:** [e.g., "Refunds, disputes, invoices — Layer 3."]

---

## 6. AUTH SCOPE

> Wrong auth scope = rebuild.

- **Auth provider:** [Clerk / Supabase Auth]
- **Scope:** [Single-tenant / Clerk orgs / public-facing multi-tenant]
- **Session model:** [e.g., "One account per salon. Staff share the owner's session for now."]
- **What's deferred:** [e.g., "Staff permissions, role-based access — Layer 2."]

---

## 7. LAYER CONSTRAINTS

> What is Layer 1 only? What is explicitly deferred?

| Layer | What's in scope | What's explicitly out |
|-------|-----------------|----------------------|
| Layer 1 (today) | [Feature A], [Feature B], [Feature C] | Everything else |
| Layer 2 (next sprint) | [Feature D], [Feature E] | [Feature F, G — document why] |
| Layer 3 (future) | [Deferred features] | [Won't features — anti-vision] |

---

## 8. DEPLOY TARGET

- **Platform:** [Vercel / EAS / Railway]
- **Project name:** [exact name in platform dashboard]
- **Env vars already set:** [list — e.g., `SUPABASE_URL`, `CLERK_SECRET_KEY`]
- **Env vars CC needs to add:** [list with placeholder names]
- **Preview URL:** [e.g., `project.vercel.app` or "not deployed yet"]

---

## 9. TECH STACK (exact)

```
Framework:      [Next.js 16 App Router / Expo SDK 52 + React Native]
Language:       TypeScript — strict mode, no 'any'
Database:       Supabase — Postgres + RLS on every table
Auth:           [Clerk / Supabase Auth]
State:          Zustand (local) + React Query (server)
Forms:          React Hook Form + Zod
Payments:       [Square SDK / RevenueCat / Stripe legacy]
AI:             Claude API via [Server Action / Edge Function / Route Handler]
Animations:     [Rive / Framer Motion / none]
Error tracking: Sentry
Analytics:      [PostHog / none yet]
```

**Non-negotiable rules:**
- API keys NEVER in client bundle — always server-side env vars
- RLS enabled on every Supabase table — no exceptions
- All AI prompts through server-side proxy — no direct client → Anthropic calls
- TypeScript strict mode — no exceptions

---

## 10. AUTONOMOUS OPERATIONS PERMISSIONS

> CC reads this before deciding whether to act or ask.

- **Can CC create new files without asking?** [Yes / Within src/ only]
- **Can CC modify the database schema?** [Yes with migration file / No — ask first]
- **Can CC push to main?** [Never / Yes for hotfixes / Ask first]
- **Can CC install new packages?** [Yes / Ask first]

---

## 11. ACTIVE SESSION CONTEXT

> Updated at the start of each session. Replace this each time.

- **Today's goal:** [One sentence — the outcome, not the feature list]
- **Acceptance criteria for this session:**
  - GIVEN [starting state] WHEN [user action] THEN [specific result]
  - GIVEN [starting state] WHEN [user action] THEN [specific result]
- **Files in play today:**
  - `[path]` — [what we're doing to it]
- **Blockers / known issues:** [What CC should know before starting]
- **What NOT to touch:** [Files, tables, or features that are frozen today]

---

## 12. OPERATIONS QUICK REFERENCE

> If something breaks in production, check here first.

- **Rollback:** `vercel rollback [deployment-url]`
- **Logs:** `vercel logs --environment production --since 1h --level error`
- **Sentry project:** [URL]
- **Spend threshold:** $[amount] — if hit, production deployments pause. Resume: Vercel dashboard → Settings → Spend Management.
- **SEV 0/1 response:** Rollback first. Diagnose second. One-liner postmortem in CHANGELOG.md after.
- **Secret leaked:** Rotate immediately → add new key to Vercel env → redeploy → check git history.

---

## 13. MEMORY FILES CC READS EVERY SESSION

- `~/.claude/projects/.../memory/MEMORY.md` — Active projects + key locations
- `memory/build-rules.md` — Forms, RLS, Server Actions rules
- `memory/pending-todos.md` — What's outstanding before any new build starts
- `.claude/OPERATING_BIBLE.html` — Full spec (reference, not read every session)
- `.claude/OPERATING_BIBLE.html#deploy` — Deploy contract (rollback, env vars, spend threshold)
- `.claude/OPERATING_BIBLE.html#slos` — SLOs and alert definitions
- `.claude/OPERATING_BIBLE.html#third-parties` — Third-party registry and failure modes

---

## COMMIT FORMAT

```bash
git add [files] && git commit -m "feat([phase]): [what was built] — [outcome achieved]" && git push
```

**Examples:**
- `feat(layer1): booking list screen — operator sees today's appointments`
- `fix(auth): session persistence — stays logged in after app restart`
- `refactor(payments): Square webhook handler — idempotent, handles duplicates`

---

## VERSION

| Version | Date | What changed |
|---------|------|-------------|
| v1.0 | [Date] | Initial brief |

> **Update protocol:** When a major decision is made mid-session, update this file and commit it first.
> A stale BRIEF.md is worse than no BRIEF.md.
