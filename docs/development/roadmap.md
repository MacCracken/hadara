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

## Phase 2 — Relationships and Lineage

- [ ] Culture relationship graph traversal
- [ ] Lineage queries: "what influenced this culture?" / "what did this culture produce?"
- [ ] Syncretism modeling (Hermes Trismegistus as Greek-Egyptian syncretism)
- [ ] Temporal relationship queries

## Phase 3 — Consumer Integration

- [ ] bhava: cultural display rule export
- [ ] avatara: archetype → culture mapping
- [ ] joshua: NPC cultural background queries
- [ ] natya: narrative tradition → culture mapping
- [ ] jnana: cultural knowledge in unified corpus

## Phase 4 — Deep Content

- [ ] 50+ cultures with detailed practices, art forms, figures, texts
- [ ] Subculture modeling
- [ ] Material culture with structured attributes
- [ ] Diaspora transformation modeling
- [ ] Living culture evolution tracking

---

*Last Updated: 2026-04-12*
