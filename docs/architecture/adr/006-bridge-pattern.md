# ADR-006: String-Based Bridge Pattern

**Status**: Accepted
**Date**: 2026-04-12

## Context

hadara needs to cross-reference with avatara (archetype traditions) and itihas (historical civilizations). All three are Cyrius projects but compile independently — no shared binary types.

## Decision

Use string-based mapping functions in `bridge.cyr`. Each function maps a hadara culture ID to string names that match the target project's naming convention:

- `hadara_traditions(id, buf, max)` → avatara tradition names ("Norse", "Hindu", etc.)
- `hadara_civilizations(id, buf, max)` → itihas civilization names ("Roman Empire", etc.)
- Reverse lookups: `hadara_culture_for_tradition()`, `hadara_culture_for_civilization()`

## Rationale

- No binary dependency on avatara or itihas
- String matching is the simplest interop — callers pass the returned names to the target project's lookup functions
- Many-to-many: Vedic-Hindu → 4 avatara traditions; Persian → 3 itihas civilizations
- Bridge functions are 7-8ns (constant-time switch on culture ID)

## Consequences

- Names must stay in sync manually with avatara/itihas naming conventions
- Adding a new avatara tradition or itihas civilization requires updating the bridge
- 19/50 cultures have avatara mappings, 16/50 have itihas mappings (some cultures have no mythological tradition or no single civilization match)
