# Operating Bible — Template Changelog

## v3.0 — 2026-03-24 (Current)

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
