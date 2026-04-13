# Hadara Development Roadmap

> For the full spec, see [agnosticos/docs/development/applications/hadara.md](https://github.com/MacCracken/agnosticos/blob/main/docs/development/applications/hadara.md)

## v1.0.0 ✓ (2026-04-12)

- [x] Core types: Culture (336 bytes), Practice, ArtForm, Figure, Text, Artifact, CultureRelation
- [x] 50 cultures with verified academic citations, all with practices, art forms, values, display dimensions
- [x] 20+ query types: temporal, status, graph traversal, search, diaspora
- [x] Consumer APIs: bhava, joshua, natya, jnana
- [x] Cross-references: avatara (19 traditions), itihas (16 civilizations), reverse lookups
- [x] Subculture modeling: Hip-Hop (3 variants), Polynesian→Maori, Japanese→Ainu, Vedic→Sikh
- [x] Evolution tracking: 16 historical transitions, point-in-time status queries
- [x] Hoosh integration: context builder, JSON context, ask endpoint
- [x] CLI (13 commands), HTTP API (9 endpoints)
- [x] 329 assertions (11 test sections), 33 benchmarks
- [x] CI/CD: GitHub Actions build + test + release

## v1.1 — Content Depth

- [ ] Figures for cultures that have none (Polynesian, Aboriginal, Amazigh, Inuit, etc.)
- [ ] Texts for cultures that have none (Aztec, Inca, Korean, Swahili, etc.)
- [ ] Artifacts for cultures beyond the original 9
- [ ] Relation descriptions for all 21 relations (14 of 21 done)
- [ ] More inter-culture relations: Mongol→Chinese/Persian/Arab (Pax Mongolica), Byzantine→Norse (Varangian), Polynesian internal lineage

## v1.2 — Cross-reference Expansion

- [ ] Shared temporal queries with itihas: "what cultures existed during this event?"
- [ ] Date validation: hadara dates align with itihas civilization dates
- [ ] avatara tradition mappings for remaining 31 cultures
- [ ] itihas civilization mappings for remaining 34 cultures

## v2.0 — Structural

- [ ] Culture evolution: Dormant→Extinct transitions, revival probability modeling
- [ ] Diaspora transformation modeling (culture changes in diaspora vs homeland)
- [ ] Consumer: kshetra (spatiotemporal cultural layer)
- [ ] Consumer: varna (language↔culture associations using language/script fields)
- [ ] 100+ cultures target
- [ ] Subculture depth: region-specific variants for more cultures

---

*Last Updated: 2026-04-13*
