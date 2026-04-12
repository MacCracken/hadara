# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

## [Unreleased]

### Added
- **seed** — 12 pre-built cultures with verified academic sources: Egyptian, Persian, Vedic-Hindu, Ancient Greek, Japanese, West African Mande, Scottish Gaelic, Norse, Aboriginal Australian, Hip-Hop, Maya, Chinese
- **seed** — Practices (10), art forms (11), figures (5), texts (5), relations (3) across seeded cultures
- **main** — CLI interface: `list`, `info <id>`, `search <query>`, `at <year>`, `stats`, `serve [port]`
- **main** — HTTP JSON API server (port 8391): `/stats`, `/list`, `/culture/{id}`, `/at?year=N`, `/search?q=...`
- **docs/sources** — Per-module citation files following itihas pattern: general, cultures, practices, art-forms, figures, texts, relations
- **sources** — Academic citations in module headers (culture.cyr, practice.cyr, art.cyr, figure.cyr, text.cyr, relation.cyr)
- **tests** — Seed data verification: 12 cultures, temporal queries, status counts, sub-entity attachment

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
