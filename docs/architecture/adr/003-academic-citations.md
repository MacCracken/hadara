# ADR-003: Academic Source Citations

**Status**: Accepted
**Date**: 2026-04-12

## Context

hadara stores cultural data (dates, practices, values, figures) that must be accurate. Invented data is unacceptable — consumers depend on correctness for simulation, NPC behavior, and knowledge systems.

## Decision

All cultural data must be traceable to named academic sources. Each source module (culture.cyr, practice.cyr, etc.) has a `# Sources:` header comment. Full bibliographies live in `docs/sources/` with per-module files.

## Rationale

- itihas established this pattern successfully (per-module source files with full citations)
- Source traceability enables peer review and correction
- Comments in code headers give immediate context; `docs/sources/` gives full bibliography
- Prevents drift toward invented or stereotyped cultural data

## Consequences

- Adding a new culture requires identifying academic sources first
- Dates and classifications can be verified against named references
- The `# VERIFY: source needed` convention flags unverified claims
- `docs/sources/` currently has 7 files covering 40+ references
