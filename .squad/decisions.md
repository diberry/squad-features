# Decisions

> Team decisions that all agents must respect. Managed by Scribe.

---

## TypeScript strict mode — non-negotiable
**By:** Lead
**Date:** 2026-04-01
**What:** `strict: true`, `noUncheckedIndexedAccess: true`, no `@ts-ignore`.
**Why:** Types are contracts. If it compiles, it works.

---

## ESM-only, Node.js 20+
**By:** Lead
**Date:** 2026-04-01
**What:** All code is ESM. No CommonJS. Target Node.js 20+.
**Why:** Modern Node.js features enable cleaner async patterns.

---

## API-first design for all endpoints
**By:** Architect
**Date:** 2026-04-05
**What:** Define OpenAPI spec before writing implementation code.
**Why:** Spec-first prevents drift between docs and code.

---

## Tests required before merge
**By:** QA Lead
**Date:** 2026-04-08
**What:** Every PR must include tests. No exceptions for "small changes."
**Why:** Small untested changes compound into large untested systems.

---

## Use conventional commits
**By:** Lead
**Date:** 2026-04-10
**What:** All commits follow conventional commit format (`feat:`, `fix:`, `docs:`, etc.).
**Why:** Enables automated changelog generation and semantic versioning.

---

## No secrets in code — use environment variables
**By:** Security Lead
**Date:** 2026-04-12
**What:** All secrets, tokens, and credentials must come from environment variables. Never hardcoded.
**Why:** Leaked secrets in Git history are permanent. Environment variables are ephemeral.

---

## Prefer composition over inheritance
**By:** Architect
**Date:** 2026-04-15
**What:** Use composition patterns (dependency injection, mixins) instead of deep class hierarchies.
**Why:** Reduces coupling and makes code easier to test.

---

## Proposal-first for breaking changes
**By:** Lead
**Date:** 2026-04-18
**What:** Any breaking API change requires a proposal in `docs/proposals/` before implementation.
**Why:** Proposals create alignment before code is written.
