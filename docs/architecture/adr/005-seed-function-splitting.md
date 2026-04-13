# ADR-005: Seed Function Splitting

**Status**: Accepted
**Date**: 2026-04-12

## Context

The original `hadara_seed()` function grew to ~2800 lines as cultures expanded to 50. The Cyrius compiler has practical limits on function size (statement count, local variable count). Building failed with "unexpected ';'" errors.

## Decision

Split `hadara_seed()` into 7 phase functions called sequentially:

1. `hadara_seed_cultures()` — culture adds, endonyms, region/language/script, display dimensions
2. `hadara_seed_subentities()` — practices, art forms, figures, texts, artifacts for cultures 0-12
3. `hadara_seed_subentities_1b()` — relations, syncretism, additional figures for cultures 0-12
4. `hadara_seed_subentities_2()` — sub-entities for cultures 29-49
5. `hadara_seed_values()` — values for all 50 cultures
6. `hadara_seed_relations()` — Phase 4c additional relations
7. `hadara_seed_evolution()` — status transitions

`hadara_seed()` itself is a one-line dispatcher calling all 7.

## Rationale

- Each function stays under ~800 lines
- CultureId enum constants (CID_EGYPTIAN, CID_PERSIAN, etc.) replace local variables for cross-function references
- Relation records built fresh in each function (no cross-function memcpy)
- Deterministic add order means IDs are stable constants

## Consequences

- Adding a new culture requires: adding to `hadara_seed_cultures()`, adding a CID_ constant, adding sub-entities in the appropriate phase function
- Relation composites must be built inline (no sharing allocated records across functions)
- `var` declarations must not be redeclared within a function (Cyrius restriction)
