# ADR-004: Data-Driven Display Rules

**Status**: Accepted
**Date**: 2026-04-12

## Context

bhava needs cultural display modifiers (formality, expressiveness, etc.) per culture. Initially these were hardcoded by culture ID in if/elif chains. This broke when culture IDs changed and didn't scale to 50 cultures.

## Decision

Store display dimensions directly on the Culture record (4 fields at offsets 304-335: formality, expressiveness, individualism, directness). The `hadara_display_rule()` function reads from the record instead of branching on IDs.

## Rationale

- Data-driven: adding a culture automatically gets display rules via `hadara_set_display()`
- No code changes needed when culture IDs change
- Defaults (5/5/5/5) set in `hadara_add()` for cultures without explicit values
- Culture layout expanded from 304 to 336 bytes (acceptable — only 50 cultures × 336 = 16.8KB)

## Consequences

- `hadara_display_rule()` is now a simple struct read (35ns) instead of a branching chain
- All 50 cultures have display dimensions set in seed data
- New cultures get moderate defaults automatically
