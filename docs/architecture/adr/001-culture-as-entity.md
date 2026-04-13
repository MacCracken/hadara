# ADR-001: Culture as First-Class Entity

**Status**: Accepted
**Date**: 2026-04-12

## Context

AGNOS needs cultural data for multiple consumers (bhava, joshua, natya, jnana, avatara, itihas). Cultures could be modeled as tags on other entities, as attributes of civilizations, or as standalone entities.

## Decision

Culture is a first-class entity with its own identity, lifecycle (Active/Dormant/Revived/Historical/Extinct), practices, values, art forms, figures, texts, artifacts, and relationships to other cultures.

## Rationale

- Cultures outlive political entities (Egyptian culture survived Roman conquest)
- One civilization hosts multiple cultures (Roman Empire: Roman, Greek, Egyptian, Jewish)
- One culture spans multiple civilizations (Jewish culture across many empires)
- Cultural identity is independent of political boundaries
- Consumer needs differ from historical/political data (itihas handles civilizations)

## Consequences

- hadara and itihas are separate projects with a bridge layer
- The bridge module maps cultures ↔ civilizations via string names (many-to-many)
- Culture records carry cultural data (values, practices, art) that civilizations don't need
- Civilization records carry political data (boundaries, rulers, campaigns) that cultures don't need
