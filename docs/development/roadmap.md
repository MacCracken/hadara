# Hadara Development Roadmap

> For the full spec, see [agnosticos/docs/development/applications/hadara.md](https://github.com/MacCracken/agnosticos/blob/main/docs/development/applications/hadara.md)

## Phase 1 — Core Types and Registry (current)

- [x] Culture, CultureStatus, CultureRelation types
- [x] Practice, ArtForm, Figure, Text, Artifact sub-entity types
- [x] In-memory registry with ID-based lookup
- [x] Temporal queries (existed_at, find_by_year, coexisting_at)
- [x] Status queries (count_by_status, count_active)
- [x] Initial test suite
- [x] Seed data: 13 cultures (Egyptian, Persian, Vedic-Hindu, Greek, Japanese, West African Mande, Scottish Gaelic, Norse, Aboriginal Australian, Hip-Hop, Maya, Chinese, Roman)
- [x] Academic source citations (docs/sources/, module headers)
- [x] CLI interface (list, info, search, at, stats)
- [x] HTTP JSON API server (serve command, port 8391)
- [x] Seed data tests
- [x] Tests: 90+ assertions
- [x] All 13 cultures have practices and art forms
- [x] 7 inter-culture relations (exchange, influence)
- [ ] Expand texts for all cultures (Greek, Japanese, Chinese have partial)
- [ ] Artifact seed data for all cultures

## Phase 2 — Relationships and Lineage (current)

- [x] Culture relationship graph traversal (`hadara_all_relations`)
- [x] Lineage queries: `hadara_lineage` (ancestors via influence, BFS backward)
- [x] Influence chain: `hadara_influence_chain` (forward propagation, BFS)
- [x] Direct influencer lookup: `hadara_influences_on`, `hadara_influenced_by`
- [x] Typed relation queries: `hadara_related_by_type`, `hadara_exchanged_with`, `hadara_syncretized_with`
- [x] CLI: `lineage <id>`, `influence <id>`, `relations <id>`
- [x] HTTP: `/lineage/{id}`, `/influence/{id}`
- [x] Syncretism seed data (Greek↔Egyptian Hermes Trismegistus, Vedic↔Chinese Silk Road, Greek absorbed→Roman)
- [x] Temporal relationship queries: `hadara_relations_at`, `hadara_connected_at`, `hadara_exchanges_at`

## Phase 3 — Consumer Integration (current)

- [x] bhava: `hadara_display_rule` — formality, expressiveness, individualism, directness per culture
- [x] joshua: `hadara_dominant_practice`, `hadara_sacred_ratio` — NPC behavior patterns
- [x] natya: `hadara_narrative_count`, `hadara_narratives` — narrative tradition mapping
- [x] jnana: `hadara_fact_count`, `hadara_total_facts` — knowledge graph export metrics
- [ ] avatara: archetype → culture context mapping (needs avatara types)

## Phase 4 — Deep Content

- [ ] 50+ cultures with detailed practices, art forms, figures, texts
- [ ] Subculture modeling
- [ ] Material culture with structured attributes
- [ ] Diaspora transformation modeling
- [ ] Living culture evolution tracking

---

*Last Updated: 2026-04-12*
