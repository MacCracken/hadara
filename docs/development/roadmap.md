# Hadara Development Roadmap

> For the full spec, see [agnosticos/docs/development/applications/hadara.md](https://github.com/MacCracken/agnosticos/blob/main/docs/development/applications/hadara.md)

## Phase 1 — Core Types and Registry ✓

- [x] Culture, CultureStatus, CultureRelation types
- [x] Practice, ArtForm, Figure, Text, Artifact sub-entity types
- [x] In-memory registry with ID-based lookup
- [x] Temporal queries (existed_at, find_by_year, coexisting_at)
- [x] Status queries (count_by_status, count_active)
- [x] Seed data: 21 cultures with verified academic citations
- [x] Region, language, script fields on Culture layout (304 bytes)
- [x] CLI interface (list, info, search, at, stats, lineage, influence, relations)
- [x] HTTP JSON API server (port 8391, 7 endpoints)
- [x] 208 test assertions

## Phase 2 — Relationships and Lineage ✓

- [x] Graph traversal: `hadara_all_relations`, `hadara_influences_on`, `hadara_influenced_by`
- [x] Lineage queries: `hadara_lineage` (BFS backward), `hadara_influence_chain` (BFS forward)
- [x] Typed relation queries: `hadara_related_by_type`, `hadara_exchanged_with`, `hadara_syncretized_with`
- [x] Temporal relation filtering: `hadara_relations_at`, `hadara_connected_at`, `hadara_exchanges_at`
- [x] Syncretism seed data (Greek↔Egyptian, Vedic↔Chinese, Greek absorbed→Roman)

## Phase 3 — Consumer Integration ✓ (partial)

- [x] bhava: `hadara_display_rule` — formality/expressiveness/individualism/directness
- [x] joshua: `hadara_dominant_practice`, `hadara_sacred_ratio`
- [x] natya: `hadara_narrative_count`, `hadara_narratives`
- [x] jnana: `hadara_fact_count`, `hadara_total_facts`
- [ ] avatara: archetype → culture context (blocked — avatara needs Cyrius port)

## Phase 4 — Deep Content (current)

### 4a: Seed data expansion (actionable now)
- [ ] Practices, art forms, figures, texts, artifacts for 8 new cultures (Arab, Korean, Tibetan, Mesopotamian, Mongol, Jewish, Byzantine, Polynesian)
- [ ] Values/worldview data for all 21 cultures (use existing `values_ptr/count` field)
- [ ] Diaspora data for cultures with significant dispersal (Jewish, African, Polynesian, Chinese)
- [ ] Medium-priority cultures: Aztec/Mexica, Inuit, Inca/Quechua, Ottoman, Khmer, Swahili, Yoruba, Berber/Amazigh

### 4b: Structural improvements (actionable now)
- [ ] Data-driven display rules (move from hardcoded IDs to stored cultural dimensions)
- [ ] Subculture modeling (Hip-Hop regional variants, Ainu within Japanese)
- [ ] Culture↔itihas civilization cross-reference field (for future port)
- [ ] Relation descriptions (use existing `desc_ptr/desc_len` in RelationLayout — never seeded)

### 4c: Additional relations (actionable now)
- [ ] Arab↔Persian exchange (Sassanid→Islamic transition)
- [ ] Vedic→Tibetan influence (Buddhist transmission)
- [ ] Mesopotamian→Egyptian exchange (Bronze Age trade)
- [ ] Mongol→Chinese/Persian/Arab exchange (Pax Mongolica)
- [ ] Jewish↔Arab syncretism (Judeo-Arabic tradition)
- [ ] Byzantine→Norse exchange (Varangian trade)
- [ ] Polynesian internal lineage (Lapita→Tongan→Hawaiian)

### 4d: Query enhancements
- [ ] Full-text search across all string fields (not just culture name)
- [ ] "Cultures with practice category X" query
- [ ] "Cultures with art medium Y" query
- [ ] Region-based lookup

## Phase 5 — Cross-references ✓

- [x] `bridge.cyr` — string-based mapping layer (no binary dep on avatara/itihas)
- [x] `hadara_traditions(id, buf, max)` — culture → avatara tradition names (19 of 21 mapped)
- [x] `hadara_civilizations(id, buf, max)` — culture → itihas civilization names (16 of 21 mapped)
- [x] `hadara_culture_for_tradition(name, buf, max)` — reverse lookup: tradition → cultures
- [x] `hadara_culture_for_civilization(name, buf, max)` — reverse lookup: civ → cultures
- [ ] Shared temporal queries: "what cultures existed during this itihas event?" (needs itihas event API)
- [ ] Validation: hadara dates align with itihas civilization dates

## Phase 6 — Future

- [ ] Living culture evolution tracking (status transitions over time)
- [ ] Consumer: kshetra (spatiotemporal cultural layer)
- [ ] Consumer: varna (language↔culture associations — uses language/script fields)
- [ ] Consumer: avatara (archetype → culture context — post avatara port)
- [ ] 50+ cultures target
- [ ] Medium-priority cultures: Aztec/Mexica, Inuit, Inca/Quechua, Ottoman, Khmer, Swahili, Yoruba, Berber/Amazigh

---

*Last Updated: 2026-04-12*
