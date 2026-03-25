# VERCEL-OPS-CONTRACT.md — [Product Name]
> Machine-readable. CC reads this before ANY deployment action.
> Lives at `.claude/VERCEL-OPS-CONTRACT.md` in each project.
> Keep it short. Update it every time deploy config changes.

---

## IDENTITY

```yaml
app: [app-slug]                    # e.g., esti-app
vercel_project: [exact-project-name]
environment: production
platform: vercel                   # vercel | eas | railway
```

---

## SCOPE — CC OPERATES WITHIN THESE BOUNDS

```yaml
scope:
  apps: ["[app-slug]"]
  environments: ["production", "preview"]
  branches:
    production: main
    preview: "feature/*"
```

---

## PERMISSIONS

```yaml
permissions:
  - "CC cannot DROP tables without explicit approval"
  - "CC cannot push directly to main — PR required unless Brad says 'hotfix'"
  - "CC cannot add new env vars to production without confirming they exist first"
  - "CC cannot install native modules without asking"
  - "CC cannot exceed Vercel spend threshold — pause before any action that triggers new builds in a loop"
```

---

## DEPLOYMENT SAFETY

```yaml
deployment_safety:
  blackout_windows:
    - "Sunday 00:00–06:00 UTC"          # No deploys during low-traffic maintenance window
    - "Friday 15:00–17:00 local"        # Pre-weekend freeze — avoid late Friday deploys
  pre_deploy_checks:
    - "npx tsc --noEmit passes"
    - "npm run build passes locally"
    - "No .env changes committed"
    - "RLS policies present on any new table"
  post_deploy_checks:
    - "Vercel deployment status = READY"
    - "No new Sentry errors in first 10 min"
    - "Primary user flow smoke test passes"
```

---

## ROLLBACK

```yaml
rollback:
  command: "vercel rollback [deployment-url]"
  trigger: "Any SEV 0 or SEV 1 incident"
  owner: "CC executes — no approval needed for rollback"
  note: "Rollback first. Diagnose second. Always."
```

---

## ENV VAR RULES

```yaml
env_vars:
  rule: "Changes apply to NEW deploys only — existing deploy is unaffected"
  add_via: "vercel env add CLI or Vercel MCP — never manual dashboard for secrets"
  never_commit: [".env", ".env.local", ".env.production"]
  rotation_cadence:
    ANTHROPIC_API_KEY: "90 days"
    CLERK_SECRET_KEY: "180 days"
    SUPABASE_SERVICE_ROLE_KEY: "180 days"
    SQUARE_ACCESS_TOKEN: "on compromise only"
  protection_bypass_token:
    sensitivity: HIGH
    purpose: "Allows Playwright/CI to access password-protected preview deployments"
    rotation: "Rotate if leaked — treat same as a secret key"
    location: "Vercel project → Settings → Deployment Protection → Bypass Token"
```

---

## SPEND THRESHOLD

```yaml
spend:
  threshold: $[amount]
  what_happens: "Vercel pauses production deployments automatically"
  how_to_resume: "Vercel dashboard → Settings → Spend Management → Resume"
  cc_action: "Stop all deploy loops. Alert Brad. Do NOT attempt to resume autonomously."
```

---

## ESCALATION

```yaml
escalation:
  availability_drop: "Alert Brad if < 99.5% uptime for > 5 min"
  error_rate_spike: "Alert Brad if Sentry errors > 10x baseline in any 5-min window"
  payment_failure: "Alert Brad immediately — never auto-retry Square/Stripe charges"
  secret_leaked: "Rotate immediately → add new key to Vercel env → redeploy → check git history"
```

---

## FILE OWNERSHIP

> CC must not modify these files without explicit per-session permission.

```yaml
frozen_files:
  - "supabase/migrations/*.sql"           # Schema is append-only
  - ".env*"                               # Never touch env files
  - "package-lock.json"                   # Only change via npm install
  - "[any file Brad listed in Section 11 of BRIEF.md]"
```

---

## RECOVERY TEST LOG

> Monthly: run the SEV 0 runbook in staging. Record result here.

| Date | Runbook tested | Result | Notes |
|------|---------------|--------|-------|
| [YYYY-MM] | SEV 0 bad deploy | PASS / FAIL | [notes] |

---

## VERSION

| Version | Date | What changed |
|---------|------|-------------|
| v1.0 | [Date] | Initial contract |

> **Update protocol:** Any change to deployment config, env vars, or spend threshold must update this file in the same commit.
