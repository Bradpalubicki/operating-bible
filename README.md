# Operating Bible — NuStack Project Framework

## What This Is
The Operating Bible system is the single source of truth for every NuStack product.
Two documents per project. Different purposes. Both mandatory.

---

## The Two Documents

### 1. `BRIEF.md` — CC reads every session
Short. Outcome-first. The minimum Claude Code needs to build without asking.
Template: `templates/BRIEF-template.md`

### 2. `OPERATING_BIBLE.html` — Full product reference
The complete spec. Brand, architecture, personas, features, flows, financials, decisions.
Template: `templates/OPERATING_BIBLE-template-v3.html`

---

## Project Folder Structure (per engine)

```
/project-root/
  .claude/
    BRIEF.md                  ← CC reads at session start (every session)
    OPERATING_BIBLE.html      ← Full reference (section reference, not full read)
    VERCEL-OPS-CONTRACT.md    ← Machine-readable deploy permissions + escalation rules
  ops/
    runbooks/
      bad-deploy.md           ← SEV 0/1 bad deploy response
      high-error-rate.md      ← Sentry spike response
      secret-leaked.md        ← Credential compromise response
      db-down.md              ← Supabase outage response
      payment-failure.md      ← Square/Stripe failure response
```

### Three-tier contract system (v3.2)

| File | When CC reads it | Purpose |
|------|-----------------|---------|
| `BRIEF.md` | Every session start | Bootstrap contract — product, stack, permissions, session goals |
| `VERCEL-OPS-CONTRACT.md` | Before any deploy action | Platform contract — deploy rules, env vars, escalation, rollback |
| `ops/runbooks/*.md` | When incident occurs | Response SOPs — one file per incident type, tested monthly |

---

## What Makes a Strong Operating Bible (v3 standards)

Learned from PocketPals v5 — the gold standard:

1. **Vision + Anti-Vision** — both matter equally. What you won't build is as important as what you will.
2. **Actual dialogue, not descriptions** — every feature shows real copy, real Buddy lines, real UX text. Not "Buddy greets the child warmly." Write the actual words.
3. **Specific personas** — named people with specific fears, not demographic averages.
4. **Decision log with status** — every open architectural decision tracked.
5. **Acceptance criteria per feature** — GIVEN/WHEN/THEN format, not vague descriptions.
6. **Anti-vision list** — explicit list of things that will never be built. Stops scope creep cold.
7. **CC Prompt Panel** — exact prompts CC uses to build each section. No interpretation required.

---

## Files in This Repo

```
templates/
  BRIEF-template.md                  ← CC session brief (with YAML machine-readable block)
  OPERATING_BIBLE-template-v3.html   ← Full HTML Operating Bible (v3.1+)
  VERCEL-OPS-CONTRACT.md             ← Machine-readable deploy contract template
  RUNBOOK-template.md                ← Per-incident runbook template

examples/
  pocketpals-brief.md                ← PocketPals BRIEF.md (derived from v5 bible)

CHANGELOG.md                         ← Version history of the templates
README.md                            ← This file
```

---

## Version History

| Version | Date | What Changed |
|---------|------|-------------|
| v3.2 | 2026-03-24 | VERCEL-OPS-CONTRACT.md + RUNBOOK-template.md + YAML block in BRIEF.md |
| v3.1 | 2026-03-24 | Operations section in HTML (deploy, SLOs, incidents, third-parties, meta-contract) |
| v3.0 | 2026-03-24 | CC Prompt Panels, Decision Log, Acceptance Criteria, Anti-Vision List |
| v2.0 | 2026-03 | Operating Bible HTML template (template-only, no real content) |
| v1.0 | 2026-02 | PocketPals v4 — first full Operating Bible in production |
