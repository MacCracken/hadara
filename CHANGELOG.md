# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [Unreleased]

### Added
- **seed** — 13 pre-built cultures with verified academic sources: Egyptian, Persian, Vedic-Hindu, Ancient Greek, Japanese, West African Mande, Scottish Gaelic, Norse, Aboriginal Australian, Hip-Hop, Maya, Chinese, Roman
- **seed** — Practices (34), art forms (37), figures (19), texts (9), relations (7) across all seeded cultures. Every culture has practices and art forms
- **main** — CLI interface: `list`, `info <id>`, `search <query>`, `at <year>`, `stats`, `serve [port]`
- **main** — HTTP JSON API server (port 8391): `/stats`, `/list`, `/culture/{id}`, `/at?year=N`, `/search?q=...`
- **docs/sources** — Per-module citation files following itihas pattern: general, cultures, practices, art-forms, figures, texts, relations
- **sources** — Academic citations in module headers (culture.cyr, practice.cyr, art.cyr, figure.cyr, text.cyr, relation.cyr)
- **query** — Phase 2 graph traversal: `hadara_influences_on`, `hadara_influenced_by`, `hadara_all_relations`, `hadara_related_by_type`, `hadara_influence_chain` (BFS forward), `hadara_lineage` (BFS backward), `hadara_syncretized_with`, `hadara_exchanged_with`
- **main** — CLI commands: `lineage <id>`, `influence <id>`, `relations <id>`
- **main** — HTTP endpoints: `/lineage/{id}`, `/influence/{id}`
- **seed** — Artifacts for 8 cultures (Egyptian, Japanese, Norse, Roman, Hip-Hop, West African, Chinese, Maya, Aboriginal)
- **seed** — Texts for Greek, Japanese, West African, Maya (completing text coverage)
- **query** — Temporal relation queries: `hadara_relations_at`, `hadara_connected_at`, `hadara_exchanges_at`
- **seed** — Syncretism: Greek↔Egyptian (Hermes Trismegistus, 300 BCE--200 CE), Vedic↔Chinese (Silk Road Buddhism, 100 BCE--800 CE), Greek absorbed→Roman (146--30 BCE)
- **consumer** — Phase 3 consumer integration: bhava display rules (formality/expressiveness/individualism/directness), joshua NPC behavior (`hadara_dominant_practice`, `hadara_sacred_ratio`), natya narrative mapping (`hadara_narrative_count`, `hadara_narratives`), jnana knowledge export (`hadara_fact_count`, `hadara_total_facts`)
- **bridge** — Cross-reference layer to avatara and itihas: `hadara_traditions` (culture → avatara tradition names), `hadara_civilizations` (culture → itihas civ names), reverse lookups `hadara_culture_for_tradition` and `hadara_culture_for_civilization`
- **tests** — 283 assertions across 6 test sections: registry, seed, graph traversal, temporal relations, consumer integration, bridge (avatara + itihas)

## [0.1.0] — 2026-04-12

### Added
- Core types: Culture, CultureStatus (Active/Dormant/Revived/Historical/Extinct), CultureRelation, RelationType
- Sub-entity types: Practice, ArtForm, Figure, Text, Artifact with categorization enums
- In-memory culture registry with add/get/set operations (256 max cultures)
- Temporal queries: culture_existed_at, hadara_find_by_year, hadara_coexisting_at
- Status queries: hadara_count_by_status, hadara_count_active
- Setter functions for practices, art forms, figures, texts, relations, parents, children
- Initial test suite: registry operations, temporal queries, status checks, practice/figure/relation creation
- Project scaffold: CLAUDE.md, README, cyrius.toml, docs structure
