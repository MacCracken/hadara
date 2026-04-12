# Hadara حضارة

> Culture as a first-class entity — civilizations, practices, values, art forms, lineage, evolution, diaspora, and relationships between cultures.

**Hadara** (Arabic: حضارة — civilization, culture, from the root for "presence") models cultures as living entities in the AGNOS ecosystem. Not tags. Not attributes. First-class things with identity, lifecycle, practices, values, art, figures, texts, and relationships to other cultures.

## Quick Start

```bash
# Build
cat src/lib.cyr | cc3 > build/hadara

# Test
cyrius test tests/hadara.tcyr
```

## What It Does

- **Culture registry** — in-memory store of culture entities with ID-based lookup
- **Status modeling** — Active, Dormant, Revived, Historical, Extinct
- **Temporal queries** — "which cultures coexisted in 500 BCE?"
- **Relationship graph** — influence, syncretism, branching, conflict, exchange between cultures
- **Practice / Art / Figure / Text / Artifact** — structured sub-entities for cultural detail

## Consumers

bhava (cultural display rules), avatara (archetype context), joshua (NPC culture), natya (narrative traditions), jnana (knowledge corpus), kshetra (temporal geography), varna (language associations), itihas (event context).

## License

GPL-3.0-only

## Part of AGNOS

[agnosticos.org](https://agnosticos.org) — the AI-native operating system.
