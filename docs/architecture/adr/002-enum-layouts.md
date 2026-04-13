# ADR-002: Enum Layouts for Struct Offsets

**Status**: Accepted
**Date**: 2026-04-12

## Context

Cyrius has structs with named fields, but the hadara codebase needs fine-grained control over memory layout for heap-allocated records accessed by multiple modules.

## Decision

Use enum constants to define struct field offsets (e.g., `CULTURE_NAME_PTR = 8`). Access fields via `load64(ptr + OFFSET)` / `store64(ptr + OFFSET, value)`.

## Rationale

- Zero gvar_toks cost — enum values are compile-time constants
- Same pattern used successfully in bsp, cyrius-doom, and other AGNOS projects
- Explicit layout makes the binary format self-documenting
- Enables `memset(ptr, 0, SIZE)` for initialization
- Compatible with Cyrius include-once semantics

## Consequences

- Field access requires knowing the layout enum (not type-checked)
- Adding fields requires bumping SIZE and updating all initializers
- Accessor functions (`culture_name_ptr(c)`) provide a cleaner API over raw offsets
