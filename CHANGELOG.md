# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [1.0.0] — 2026-04-12

### Added

#### Core Types and Registry
- Culture entity: 336-byte record with name, endonym, status, region, language, script, 4 display dimensions (formality/expressiveness/individualism/directness), parent/child/subculture pointers, values, diaspora
- CultureStatus: Active, Dormant, Revived, Historical, Extinct
- Sub-entity types: Practice (8 categories, frequency, sacred/secular), ArtForm (11 media), Figure (name, role, era), Text (title, author, year, sacred), Artifact (9 categories)
- CultureRelation: 7 relation types (influenced, syncretized, branched_from, conflicted, exchanged, absorbed, revived_from) with time bounds and descriptions
- In-memory registry: 256 max cultures, ID-based lookup, add/get/set operations

#### Seed Data — 50 Cultures
- **Ancient/Classical**: Egyptian, Persian, Vedic-Hindu, Ancient Greek, Roman, Mesopotamian, Byzantine
- **East Asian**: Japanese, Chinese, Korean, Ainu (revived)
- **South/Central Asian**: Tibetan, Tamil, Sikh
- **Southeast Asian**: Javanese, Khmer, Balinese
- **African**: West African Mande, Yoruba, Swahili, Ethiopian, Igbo, Zulu, Somali, Tuareg, Amazigh
- **European**: Scottish Gaelic (revived), Norse, Basque, Armenian, Georgian, Romani, Catalan
- **Americas**: Maya, Inca-Quechua, Aztec, Hip-Hop, Haudenosaunee, Lakota, Inuit
- **Oceanian**: Aboriginal Australian, Polynesian, Maori
- **Subcultures**: East Coast Hip-Hop, West Coast Hip-Hop, Southern Hip-Hop
- All 50 cultures have: practices, art forms, values (3 per culture), display dimensions, region, language/script
- 28 figures, 25+ texts, 25 artifacts, 16 inter-culture relations with descriptions
- 6 cultures with diaspora data (Jewish, Chinese, West African, Polynesian, Hip-Hop, Persian)

#### Queries (15 types)
- Temporal: `culture_existed_at`, `hadara_find_by_year`, `hadara_coexisting_at`
- Status: `hadara_count_by_status`, `hadara_count_active`
- Graph traversal: `hadara_influences_on`, `hadara_influenced_by`, `hadara_all_relations`, `hadara_related_by_type`, `hadara_influence_chain` (BFS forward), `hadara_lineage` (BFS backward)
- Temporal relations: `hadara_relations_at`, `hadara_connected_at`, `hadara_exchanges_at`
- Typed shortcuts: `hadara_syncretized_with`, `hadara_exchanged_with`
- Search: `hadara_with_practice_category`, `hadara_with_art_medium`, `hadara_by_region`, `hadara_search_all` (full-text across name/endonym/region/language), `hadara_diaspora_in`

#### Consumer Integration
- **bhava**: `hadara_display_rule` — data-driven formality/expressiveness/individualism/directness per culture
- **joshua**: `hadara_dominant_practice`, `hadara_sacred_ratio` — NPC behavior patterns
- **natya**: `hadara_narrative_count`, `hadara_narratives` — narrative tradition mapping
- **jnana**: `hadara_fact_count`, `hadara_total_facts` — knowledge graph export metrics

#### Cross-references (bridge.cyr)
- **avatara**: `hadara_traditions` — culture → avatara tradition names (19/50 mapped across 22 traditions)
- **itihas**: `hadara_civilizations` — culture → itihas civilization names (16/50 mapped)
- Reverse lookups: `hadara_culture_for_tradition`, `hadara_culture_for_civilization`

#### Evolution Tracking (evolution.cyr)
- `hadara_evolve` — change culture status and record transition
- `hadara_status_at` — point-in-time status query (what was this culture's status in year X?)
- `hadara_evo_for` — get all transitions for a culture
- 17 historical transitions seeded: Scottish Gaelic 3-phase (Active→Dormant→Revived), Norse, Egyptian, Greek, Byzantine, Ainu 3-phase, Aztec

#### Subculture Modeling
- Parent/child relationships: `hadara_set_subcultures`, `hadara_subculture_count`, `hadara_subculture_ids`
- Subculture tree: Hip-Hop (East Coast, West Coast, Southern), Polynesian→Maori, Japanese→Ainu, Vedic→Sikh

#### Hoosh Integration (hoosh.cyr)
- `hadara_context` — builds rich text cultural context for LLM system prompts (name, endonym, region, language, status, values, display style, practices, art forms, figures)
- `hadara_context_json` — compact JSON cultural context
- `hadara_ask` — POST culturally-grounded question to hoosh gateway, returns LLM response

#### CLI (13 commands)
- `list`, `info <id>`, `search <query>`, `at <year>`, `stats`
- `lineage <id>`, `influence <id>`, `relations <id>`
- `context <id>`, `ask <id> <question> [port]`
- `serve [port]`, `help`

#### HTTP JSON API (11 endpoints, port 8391)
- `/stats`, `/list`, `/culture/{id}`, `/at?year=N`, `/search?q=...`
- `/lineage/{id}`, `/influence/{id}`
- `/context/{id}` (text/plain), `/evolution/{id}`

#### Documentation
- Academic source citations: 7 per-module files in `docs/sources/` (general, cultures, practices, art-forms, figures, texts, relations)
- Source citations in all module headers
- P(-1) audit document with gap analysis
- Development roadmap

#### CI/CD
- GitHub Actions CI: build, format check, security scan, test suite, documentation verification
- GitHub Actions Release: CI gate, version verification, binary build, changelog extraction, source archive, SHA256 checksums, GitHub Release
- `scripts/version-bump.sh`

#### Test Suite
- 330 assertions across 11 test sections
- Coverage: registry operations, seed data integrity, graph traversal, temporal relations, consumer APIs, bridge cross-references, query enhancements, subcultures, evolution tracking, relation descriptions, hoosh context builder
