# RUNBOOK — [Incident Type]
> Lives at `ops/runbooks/[incident-slug].md` in each project.
> One file per incident type. Keep it short. This is executed under pressure.
> Last tested: [YYYY-MM-DD in staging]

---

## METADATA

```yaml
incident_type: [bad-deploy | high-error-rate | db-down | payment-failure | secret-leaked | auth-outage]
severity: [SEV 0 | SEV 1 | SEV 2 | SEV 3]
owner: CC               # Who executes this
escalate_to: Brad       # Who gets called if CC can't resolve
last_tested: [YYYY-MM-DD]
test_environment: staging
```

---

## TRIGGER

> When does this runbook activate?

- **Condition:** [e.g., "Vercel deployment shows ERROR status" / "Sentry error rate > 10x baseline"]
- **Who detects it:** [e.g., "Vercel deploy hook / Sentry alert / Brad reports it"]
- **Severity:** SEV [0/1/2/3]

---

## IMMEDIATE RESPONSE (do this first, ask questions later)

```bash
# Step 1 — Rollback (if deploy-related)
vercel rollback [last-good-deployment-url]

# Step 2 — Check logs
vercel logs --environment production --since 30m --level error

# Step 3 — Check Sentry
# Go to: [Sentry project URL]
# Filter: last 30 minutes, unresolved

# Step 4 — Verify rollback worked
curl -I https://[production-url]
# Expected: 200 OK within 60 seconds of rollback
```

---

## DIAGNOSIS

> Only after immediate response is complete.

**What to look for:**

1. **Build logs:** `vercel logs --environment production --since 1h`
2. **DB health:** Check Supabase dashboard → Database → Health
3. **Auth health:** Check Clerk dashboard → Activity
4. **Payment health:** Check Square/Stripe → Recent transactions
5. **Edge functions:** Check Supabase → Edge Functions → Logs

**Common causes for [incident type]:**

- [ ] [Cause 1 — e.g., "Env var missing from production"]
- [ ] [Cause 2 — e.g., "Schema migration ran but RLS policy not updated"]
- [ ] [Cause 3 — e.g., "Third-party rate limit hit"]

---

## FIX STEPS

> Work through in order. Stop at the first one that resolves the incident.

**Fix A — [Most common cause]:**
```bash
[exact commands to execute]
```

**Fix B — [Second most common cause]:**
```bash
[exact commands to execute]
```

**Fix C — Escalate:**
- CC cannot resolve → Stop. Call Brad.
- Provide: what symptoms were observed, what was tried, what logs show.

---

## VERIFY RESOLVED

```bash
# Smoke test — confirm primary user flow works
curl -X GET https://[production-url]/api/health
# Expected: {"status":"ok","db":"connected","auth":"ok"}

# Optional: Playwright smoke test
npx playwright test tests/smoke.spec.ts --project=chromium
```

---

## POSTMORTEM (one-liner format)

> Add to CHANGELOG.md after every SEV 0 or SEV 1. No 10-page documents.

```
[YYYY-MM-DD] SEV [X] — [what broke] — root cause: [one sentence] — fix: [one sentence] — prevention: [one sentence]
```

**Example:**
```
2026-03-24 SEV 1 — booking form 500 errors — root cause: SQUARE_ACCESS_TOKEN expired in production — fix: rotated token, redeployed — prevention: add token rotation reminder to VERCEL-OPS-CONTRACT.md rotation_cadence
```

---

## RECOVERY TEST PROCEDURE

> Run this monthly in staging to verify the runbook still works.

1. Trigger the incident condition in staging (or simulate it)
2. Execute this runbook from top to bottom without skipping steps
3. Record pass/fail in `VERCEL-OPS-CONTRACT.md` → Recovery Test Log
4. Update "last_tested" field at the top of this file

---

## VERSION

| Version | Date | What changed |
|---------|------|-------------|
| v1.0 | [Date] | Initial runbook |
