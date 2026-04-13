# Hadara Architecture

## Module Map

```
src/
  lib.cyr           Public API (includes all modules)
  main.cyr          CLI + HTTP server binary
  ─── Data Layer ───
  culture.cyr       Culture entity (336 bytes), CultureStatus, layout, accessors
  practice.cyr      Practice, PracticeCategory, Frequency
  art.cyr           ArtForm, ArtMedium (11 media)
  figure.cyr        Figure (key cultural figures)
  text.cyr          Text (sacred/canonical texts)
  artifact.cyr      Artifact (material culture, 9 categories)
  relation.cyr      CultureRelation, RelationType (7 types)
  ─── Storage ───
  registry.cyr      In-memory culture registry (256 max, bump-allocated)
  seed.cyr          50 pre-built cultures (split into 7 seed functions)
  ─── Query ───
  query.cyr         20+ query types: temporal, graph, search, diaspora
  ─── Consumer ───
  consumer.cyr      bhava, joshua, natya, jnana integrations
  ─── Integration ───
  bridge.cyr        avatara (tradition mapping), itihas (civilization mapping)
  evolution.cyr     Status transition tracking, point-in-time queries
  hoosh.cyr         LLM context builder + ask endpoint

tests/
  hadara.tcyr       329 assertions across 11 test sections
  hadara.bcyr       33 benchmarks across 8 tiers

docs/
  sources/          7 per-module academic citation files (40+ references)
  architecture/     This file, ADRs
  development/      Roadmap, P(-1) audit
```

## Data Flow

```
                    ┌─────────────┐
                    │  seed.cyr   │ 50 cultures, practices, arts,
                    │  (7 funcs)  │ figures, texts, artifacts, values,
                    └──────┬──────┘ relations, evolution
                           │
                           ▼
                    ┌──────────────┐
                    │ registry.cyr │ hadara_init() + hadara_add()
                    │  256 slots   │ ID-based lookup, set operations
                    └──────┬───────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
       ┌────────────┐ ┌──────────┐ ┌───────────┐
       │ query.cyr  │ │consumer  │ │ bridge.cyr│
       │ temporal,  │ │ bhava,   │ │ avatara,  │
       │ graph,     │ │ joshua,  │ │ itihas    │
       │ search     │ │ natya,   │ │ reverse   │
       └─────┬──────┘ │ jnana   │ │ lookups   │
             │        └────┬─────┘ └─────┬─────┘
             │             │             │
             ▼             ▼             ▼
       ┌───────────────────────────────────────┐
       │              main.cyr                 │
       │  CLI (13 commands) + HTTP (9 routes)  │
       └──────────────────┬────────────────────┘
                          │
                    ┌─────┴──────┐
                    │ hoosh.cyr  │ context builder,
                    │            │ ask endpoint (→ hoosh:8088)
                    └────────────┘
```

## Culture Record Layout (336 bytes)

| Offset | Field | Notes |
|--------|-------|-------|
| 0-7 | id | CultureId (integer index) |
| 8-23 | name ptr+len | Culture name |
| 24-39 | endonym ptr+len | Self-designation (0 if none) |
| 40-47 | status | CultureStatus enum |
| 48-79 | geo_roots, diaspora | Ptr+count pairs |
| 80-95 | time_start, time_end | Emergence/end years (negative = BCE) |
| 96-127 | parent, child | Culture lineage pointers |
| 128-143 | values | Core worldview values |
| 144-175 | practices, art_forms | Ptr+count to sub-entity arrays |
| 176-215 | figures, texts, artifacts | Ptr+count to sub-entity arrays |
| 224-255 | subcultures, relations | Ptr+count |
| 256-303 | region, language, script | Geographic/linguistic identity |
| 304-335 | formality, expressiveness, individualism, directness | Display dimensions (0-10) |

## Key Design Decisions

1. **Enum layouts for struct offsets** — zero gvar_toks cost, field access is `load64(ptr + OFFSET)`. Same pattern as bsp/cyrius-doom.

2. **Culture is not Civilization** — hadara models cultural identity (values, practices, art), not political entities. One civilization may host multiple cultures. One culture may span multiple civilizations. The bridge module handles the mapping.

3. **Data-driven display rules** — cultural dimensions stored on the record itself, not hardcoded by ID. bhava reads directly from culture fields.

4. **String-based cross-references** — bridge.cyr maps culture IDs to avatara tradition names and itihas civilization names via string matching. No binary dependency on either project.

5. **Seed function splitting** — `hadara_seed()` dispatches to 7 sub-functions to stay within Cyrius compiler limits (~500 statements per function).

## Dependencies

- **sakshi** — logging (vendored in `lib/sakshi.cyr`, stderr profile)
- **Cyrius stdlib** — string, alloc, str, vec, fmt, net, json, etc. (vendored in `lib/`)
- No external runtime dependencies
