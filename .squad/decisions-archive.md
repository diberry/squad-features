# Decisions Archive

> Old decisions archived by `squad nap --deep`. For active decisions, see `.squad/decisions.md`.

---

### 2026-03-01: Initial project setup — monorepo with npm workspaces
**By:** Lead
**Date:** 2026-03-01
**What:** Project uses npm workspaces for monorepo management.
**Why:** npm-native workspace resolution avoids pnpm/Yarn lock-in.
**Archived:** 2026-04-20 (stable, no longer actively referenced)

---

### 2026-03-05: Prettier + ESLint config standardized
**By:** Lead
**Date:** 2026-03-05
**What:** Single `.prettierrc` and `eslint.config.mjs` at repo root. No per-package overrides.
**Why:** Consistency across packages reduces cognitive load.
**Archived:** 2026-04-20 (stable, baked into CI)

---

### 2026-03-10: Docker compose for local dev
**By:** DevOps
**Date:** 2026-03-10
**What:** Use `docker compose up` for local development with all services.
**Why:** One command to spin up the full stack. No manual service management.
**Archived:** 2026-04-20 (stable, well-documented in README)
