# Operating Bible — Template Changelog

## v3.3 — 2026-03-24 (Current)

### Gap fixes — Operating Handbook + CC Brief YAML

**Gap 1 fixed — `id="ops"` Operating Handbook section added:**
- New section before `#deploy` with eyebrow "Operations"
- `.meta-contract` card at top: full `app_bible_contract` YAML block (app_id, platform, vertical, tier, build_phase, prod_branch, deploy_target, payments, auth, compliance, ai_key_location, permissions block, frozen_files, escalation)
- "How CC uses this document" — 5-step session read order: BRIEF.md → MEMORY.md → build-rules.md → pending-todos.md → Bible (section reference)
- Amber alert: "A stale BRIEF.md is worse than no BRIEF.md"
- Nav link added: `#ops — Operating Handbook` as first item under Operations nav group

**Gap 2 fixed — `#cc-brief` YAML block added:**
- `.meta-contract` card at top of cc-brief section, before all micro-prompts
- Labeled: "Machine-readable contract — CC parses this first"
- Contains same YAML fields as `#ops` (keep in sync note added)
- Positioned above the existing build sequence rule alert

---

## v3.2 — 2026-03-24

### ChatGPT Research Report additions (three-tier ops contract system)

**New template files:**
- `VERCEL-OPS-CONTRACT.md` — Separate machine-readable deploy contract. YAML blocks for scope, permissions, deployment_safety, rollback, env var rules (with rotation cadence), spend threshold, escalation, file ownership, and monthly recovery test log. CC reads before any deploy action.
- `RUNBOOK-template.md` — Per-incident response playbook. One file per incident type in `ops/runbooks/`. Sections: trigger condition, immediate response (exact commands), diagnosis checklist, fix steps A/B/C, verify-resolved smoke test, one-liner postmortem format, monthly test procedure.

**Updated BRIEF-template.md:**
- Added `MACHINE-READABLE CONTRACT` YAML block at the top (before Section 1). Fields: meta (app slug, platform, phase, vertical, owner, agency_client_id), permissions (create_files, modify_schema, push_to_main, install_packages), deployment_safety (blackout_windows, pre_deploy_required), escalation (spend_threshold, sev_01_response).
- Added `VERCEL-OPS-CONTRACT.md` and `ops/runbooks/` to Section 13 memory files list.

**Updated README.md:**
- Added three-tier contract system table (BRIEF.md / VERCEL-OPS-CONTRACT.md / runbooks)
- Added `ops/runbooks/` to project folder structure
- Updated files list with new templates

**What was filtered out from the ChatGPT report (overkill or already covered):**
- `SLO.yaml` as a separate versioned file — already in `OPERATING_BIBLE.html#slos`, sufficient for NuStack scale
- Protection Bypass token documentation added inline to VERCEL-OPS-CONTRACT.md instead of a separate file
- Session-start validation ritual (CC reads BRIEF → validates against SLO before deploy) — already enforced via CLAUDE.md mandatory build sequence

---

## v3.1 — 2026-03-24

### Research-driven additions (from Deep Research Report: Turning the Operating Bible into a Build Blueprint and Operational Runbook)

**New sections added to OPERATING_BIBLE.html:**
- `#meta-contract` — Hidden `_meta.yaml` equivalent. Machine-readable identity block: app slug, deploy platform, payments processor, compliance flags, vertical, owner, agency_client_id. CC reads before any session action.
- `#deploy` — Vercel Deploy Contract. Exact rollback commands, env var rules ("changes apply to new deploys only"), branch protections, spend threshold + recovery steps, secrets rules with rotation cadence. The 4-step bad-deploy runbook.
- `#slos` — SLO table (journey / SLI / target / window / alert name / if broken). Golden signals dashboard (latency/traffic/errors/saturation). Where to look (Vercel logs, Sentry, Supabase, PostHog).
- `#incidents` — SEV 0–3 taxonomy tied to user impact. Standard SEV 0/1 playbook (5 steps). Secret leak response. One-liner postmortem format — no 10-page documents.
- `#third-parties` — Third-party registry table (service / purpose / env vars / credential owner / rate limit / if-down action / data shared). Credential ownership rule (Square = client, not NuStack).

**New CSS components:**
- `.meta-contract` — dark panel for machine-readable fields
- `.slo-table` — SLO definition table with pass/warn states
- `.deploy-block` / `.deploy-row` — dark contract blocks for deploy rules
- `.tp-table` — third-party registry table with criticality colors
- `.sev-badge` / `.sev-row` — severity taxonomy badges (SEV 0–3)

**Updated BRIEF.md template:**
- Added Section 12 — Operations Quick Reference (rollback command, logs command, Sentry link, spend threshold, SEV response, secret rotation)
- Section 13 — Memory files (was 12) with new references to deploy/slos/third-parties sections in the Bible

**What was filtered out from the research report (overkill for NuStack stage):**
- SLSA/SBOM supply chain provenance
- OPA policy-as-code enforcement
- FinOps allocation, forecasting, chargeback
- Warm standby / pilot light DR strategies
- Full OWASP ASVS profiling
- On-call rotation management
- Quarterly game day / incident simulations

## v3.0 — 2026-03-24

### What's new in v3 vs v2

**Added to OPERATING_BIBLE.html:**
- `#decisions` — Decision Log section with OPEN/DONE/BLOCKED status per architectural decision. Every open decision is a build blocker. Resolved before code starts.
- `#acceptance` — Global Acceptance Criteria section with GIVEN/WHEN/THEN format. Applied to the full build, not just individual features.
- `#cc-brief` — Claude Code Build Brief section with micro-prompts pre-written. Max 3 files per prompt. Verification gate built in. CC reads this as the authoritative build plan — no ad-hoc decisions.
- `#anti-vision` — Hard Anti-Vision list. Permanent constraints. CC checks this before adding any feature.
- `feat-layer` badge on every feature — Layer 1 / Layer 2 / Layer 3. Enforces dashboard simplification law at spec level.
- `.cc-prompt` CSS component — dark-themed prompt panels with syntax highlighting for keywords, placeholders, values.
- Multi-audience map block in Personas section — 3 audiences mandatory (primary user / secondary / NuStack agency).
- Financial model with LTV:CAC calculation cards.
- Compliance checklist with done/todo/risk states.
- Active nav scroll highlighting (JS).

**Added to BRIEF.md template:**
- Section 12 is now explicit memory files list (not just a note).
- NuStack agency view added to Section 4 (WHO MATTERS).
- Acceptance criteria format in Section 11 (ACTIVE SESSION).
- "What NOT to touch" in Section 11 — freeze list.

**What v3 fixes that v2 missed:**
1. v2 had no Decision Log → architects made decisions during build → off-track builds
2. v2 had no acceptance criteria format → CC guessed what "done" meant → rework
3. v2 had no CC build prompts → CC improvised micro-prompts → inconsistent scoping
4. v2 had no anti-vision hard list → features crept in that violated the product promise
5. v2 had no layer badges per feature → Layer 3 features ended up on Layer 1 dashboards

---

## v2.0 — 2026-03

Universal template. Sections: Foundation, Market, Product, Brand, Tech, Build, Business, Compliance, CC.
Based on OPERATING_BIBLE_TEMPLATE_v2.html. Generic, no PocketPals-specific content.

---

## v1.0 — 2026-02

PocketPals Operating Bible v4. First production use. Sections: Vision, Personas, Competitive, Features (8), Screens, Flows, Brand, Voice, Marketing, Tech, Financial, Pitch.
