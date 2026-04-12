# Hadara — Claude Code Instructions

## Project Identity

**Hadara** (Arabic: حضارة — civilization, culture, presence) — Culture as a first-class entity for AGNOS.

- **Type**: Shared library — cultural foundation for bhava, joshua, natya, jnana, time-machine
- **License**: GPL-3.0-only
- **Language**: Cyrius (native, not ported from Rust)
- **Version**: SemVer, version file at `VERSION`
- **Status**: v0.1.0 — scaffolded, core types defined, initial test suite
- **Genesis repo**: [agnosticos](https://github.com/MacCracken/agnosticos)
- **Standards**: [First-Party Standards](https://github.com/MacCracken/agnosticos/blob/main/docs/development/applications/first-party-standards.md)
- **Shared crates**: [shared-crates.md](https://github.com/MacCracken/agnosticos/blob/main/docs/development/applications/shared-crates.md)

## Consumers

| Project | Usage |
|---------|-------|
| bhava | Cultural display rules — emotional expression modifiers by culture |
| avatara | Archetype → culture context mapping |
| joshua | Culturally authentic NPC behavior, world-building |
| natya | Narrative tradition → culture mapping (rasa = Indian, kishōtenketsu = Japanese) |
| jnana | Structured cultural knowledge in the unified corpus |
| kshetra | Cultural layer on the spatiotemporal database |
| varna | Language/dialect ↔ culture associations |
| itihas | Cultural context for historical events |

## Architecture

```
src/
  lib.cyr         — public API (includes all modules)
  main.cyr        — CLI + HTTP server program
  seed.cyr        — pre-built culture data (12 cultures, cited)
  culture.cyr     — Culture entity, CultureStatus, layout, accessors
  practice.cyr    — Practice, PracticeCategory, Frequency
  art.cyr         — ArtForm, ArtMedium
  figure.cyr      — Figure (key cultural figures)
  text.cyr        — Text (sacred/canonical texts)
  artifact.cyr    — Artifact (material culture)
  relation.cyr    — CultureRelation, RelationType
  registry.cyr    — in-memory culture registry, add/get/set
  query.cyr       — query helpers (status, temporal, graph traversal, lineage)
  consumer.cyr    — consumer integration (bhava, joshua, natya, jnana)
docs/
  sources/        — per-module academic citations (itihas pattern)
```

## Key Design Constraints

- **Culture is a first-class entity**, not an attribute or tag
- **Living and historical** — CultureStatus: Active, Dormant, Revived, Historical, Extinct
- **Relational** — cultures influence, syncretize, branch, conflict, exchange
- **Zero external deps** — only sakshi (logging) as dependency
- **Consumer-driven content** — structure first, depth grows as consumers demand it
- **Enum layouts for struct offsets** — zero gvar_toks cost, same pattern as bsp/cyrius-doom

## Dependencies

- **sakshi** — logging (stdlib integrated)
- No other dependencies. Pure data modeling.

## Quick Start

```bash
# Build program
cat src/main.cyr | cc3 > build/hadara && chmod +x build/hadara

# Run
./build/hadara list              # list all cultures
./build/hadara info 9            # show hip-hop details
./build/hadara at -1000          # cultures in 1000 BCE
./build/hadara search Maya       # search by name
./build/hadara stats             # corpus statistics
./build/hadara serve 8391        # HTTP JSON API

# Run tests
cyrius test tests/hadara.tcyr

# Or manually:
cat tests/hadara.tcyr | cc3 > build/test && ./build/test
```

## Development Process

### P(-1): Scaffold Hardening (before any new features)

0. Read roadmap, CHANGELOG, and open issues — know what was intended before auditing what was built
1. Build check: `cat src/main.cyr | cc3 > build/hadara && chmod +x build/hadara`
2. Test sweep: `cyrius test tests/hadara.tcyr` — all 190 assertions pass
3. Internal deep review — correctness (culture data accuracy vs. cited sources), completeness (all fields populated), relationships (graph consistency), consumer API correctness
4. External research — are dates accurate? newer scholarship? missing cultures that consumers need?
5. Build + test again — must be clean after review
6. Additional tests from findings
7. Documentation audit — CHANGELOG, roadmap, docs/sources/ citations current
8. Repeat if heavy

### Work Loop (continuous)

1. Work phase — implement types, seed data, queries, consumer APIs
2. Build check: `cyrius build` or manual `cc3` pipeline
3. Run tests: `cyrius test tests/hadara.tcyr` — assert "0 failed"
4. Review — correctness (culture data accuracy), completeness (all fields populated), relationships (graph consistency)
5. Documentation — CHANGELOG, roadmap
6. Version check — VERSION, cyrius.toml in sync
7. Return to step 1

### Task Sizing

- **Low/Medium**: Batch freely (add a culture, add a field, add a query)
- **Large**: Small bites (new relationship type, consumer integration, seed data expansion)
- **If unsure**: Treat as large

### Key Principles

- **Never skip tests** — build and test after every change
- **Cite sources** — no invented cultural data, all claims traceable to docs/sources/
- **Consumer-driven** — add depth where consumers demand it, not speculatively
- **One change at a time** — don't bundle unrelated cultural data additions
- **3 failed attempts = defer and document** — don't burn time on blocked work

## DO NOT

- **Do not commit or push** — the user handles all git operations
- **NEVER use `gh` CLI** — use `curl` to GitHub API only
- Do not add unnecessary dependencies
- Do not invent cultural data — use verified sources. When unsure, mark with a comment: `# VERIFY: source needed`
- Do not model cultures the user hasn't reviewed — seed data should be validated
- Do not skip tests before claiming changes work

## Documentation Structure

```
Root files:
  README.md, CHANGELOG.md, CLAUDE.md, CONTRIBUTING.md,
  SECURITY.md, CODE_OF_CONDUCT.md, VERSION

docs/:
  development/roadmap.md  — development plan
```
