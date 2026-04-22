# Brand Guidelines

---

## Xzibit portfolio context (read before any DB or API changes)

This app is part of the Xzibit Apps portfolio — a set of standalone Next.js / Rails apps sharing one Supabase project (`xzibit-apps`, id `rklzgzyqbajhpjvixlkr`). Architecture is documented centrally. **Read these first before any schema, API, or cross-app change:**

- **Portfolio roadmap:** https://raw.githubusercontent.com/xzibit-apps/standards/main/docs/architecture/portfolio-roadmap.md
- **Shared-DB guide:** https://raw.githubusercontent.com/xzibit-apps/standards/main/docs/architecture/shared-db-guide.md
- **Architectural decisions:** query `public.kb_decisions` in Supabase (50+ accepted ADRs). The ones most relevant to this portfolio baseline:
  - `2c25a2b6-f8f3-47e9-be84-06ca1636f575` — shared-database architecture principle
  - `6ad3b086-3b0f-427e-9e8b-7c3ecabdbbf3` — Launcher owns `public.projects`
  - `f70caa89-3954-4796-99dd-2d836c7f23c9` — Launcher owns `public.staff`
  - `bdd7bca7-c62f-476d-bcfd-1905927dc031` — Launcher is shared-entities admin surface
  - `e4e01133-259d-43db-a5a5-9cfc83c8ce4c` — Whiplash retirement + consolidation sequencing

### This app's data ownership

- **Writes:** No Supabase writes. Static documentation.
- **Reads:** shared tables in `public.*` as needed — `projects`, `staff`, `venues`, `company_closures`, `users`, `roles`. Read-only unless this app is named as the owner in the shared-DB guide.
- **Must never write** to any `public.*` table this app doesn't own. Cross-app writes happen through the owning app's admin UI (usually the Launcher), not direct SQL.

### Non-negotiable rules

1. Every schema change lands as an **additive, reversible** migration file in this repo. No DDL via the Supabase dashboard.
2. Every `/api/*` route that reads or writes must verify a signed JWT (Auth Correctness Sprint in progress).
3. New shared concepts start with a `kb_decisions` ADR, not a new table.
4. Use the Xzibit App Standard CSS only — no bespoke colours or components.

If anything here contradicts what's in `kb_decisions`, **`kb_decisions` wins** — flag it to Joel and pause.
