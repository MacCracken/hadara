# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/).

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
