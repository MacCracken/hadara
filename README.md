# Hadara حضارة

> Culture as a first-class entity for AGNOS

**Hadara** (Arabic: حضارة — civilization, culture, presence) models cultures as living entities with identity, lifecycle, practices, values, art, and relationships. Not tags. Not attributes. First-class things.

**50 cultures** across every inhabited continent, from Aboriginal Australian (65,000 BCE) to Southern Hip-Hop (1990 CE). All data sourced from academic references.

## Quick Start

```bash
# Build
cyrius deps && cyrius build src/main.cyr build/hadara

# Run
./build/hadara list                    # list all 50 cultures
./build/hadara info 4                  # Japanese culture details
./build/hadara at -1000                # cultures in 1000 BCE
./build/hadara search Maya             # search by name
./build/hadara lineage 12              # Roman ancestors (Greek ← Egyptian)
./build/hadara influence 0             # Egyptian influence chain
./build/hadara context 4               # cultural context for LLM
./build/hadara stats                   # corpus statistics
./build/hadara serve 8391              # HTTP JSON API

# Test
cyrius test tests/hadara.tcyr          # 329 assertions, 11 sections

# Benchmark
cyrius bench tests/hadara.bcyr         # 33 benchmarks
```

## What's In It

| Module | Purpose |
|--------|---------|
| `culture.cyr` | 336-byte Culture record: name, endonym, status, region, language, script, display dimensions, parent/child/subculture, values, diaspora |
| `practice.cyr` | 8 categories (ritual, daily, ceremony, festival, art, martial, dietary, social), frequency, sacred/secular |
| `art.cyr` | 11 media (music, dance, visual, literature, oral tradition, theater, architecture, textile, culinary, martial, calligraphy) |
| `figure.cyr` | Key cultural figures with name, role, era |
| `text.cyr` | Sacred and canonical texts with author, year, sacred flag |
| `artifact.cyr` | Material culture: 9 categories (clothing, architecture, food, tool, instrument, craft, weapon, jewelry, container) |
| `relation.cyr` | 7 relation types: influenced, syncretized, branched_from, conflicted, exchanged, absorbed, revived_from |
| `registry.cyr` | In-memory store, 256 max cultures, ID-based lookup |
| `query.cyr` | 20+ query types: temporal, graph traversal, search, diaspora |
| `consumer.cyr` | bhava (display rules), joshua (NPC behavior), natya (narrative mapping), jnana (knowledge export) |
| `evolution.cyr` | Status transitions over time, point-in-time queries |
| `bridge.cyr` | Cross-references to avatara (19 traditions) and itihas (16 civilizations) |
| `hoosh.cyr` | LLM context builder + ask endpoint via hoosh gateway |
| `seed.cyr` | 50 pre-built cultures with verified academic citations |

## The 50 Cultures

**Ancient/Classical**: Egyptian, Persian, Vedic-Hindu, Ancient Greek, Roman, Mesopotamian, Byzantine
**East Asian**: Japanese, Chinese, Korean, Ainu
**South/Central Asian**: Tibetan, Tamil, Sikh
**Southeast Asian**: Javanese, Khmer, Balinese
**African**: West African Mande, Yoruba, Swahili, Ethiopian, Igbo, Zulu, Somali, Tuareg, Amazigh
**European**: Scottish Gaelic, Norse, Basque, Armenian, Georgian, Romani, Catalan
**Americas**: Maya, Inca-Quechua, Aztec, Hip-Hop, Haudenosaunee, Lakota, Inuit
**Oceanian**: Aboriginal Australian, Polynesian, Maori
**Subcultures**: East Coast Hip-Hop, West Coast Hip-Hop, Southern Hip-Hop

## HTTP API

```
GET /stats                 corpus statistics
GET /list                  all cultures (id, name, status)
GET /culture/{id}          full culture detail (JSON)
GET /at?year=N             cultures coexisting at year N
GET /search?q=...          search by name
GET /lineage/{id}          ancestors via influence (BFS backward)
GET /influence/{id}        downstream influence chain (BFS forward)
GET /context/{id}          cultural context for LLM (text/plain)
GET /evolution/{id}        status transitions over time
```

## Library Usage

```cyrius
include "src/lib.cyr"
include "src/seed.cyr"

alloc_init();
hadara_init();
hadara_seed();

# Query: cultures in 500 BCE
var buf = alloc(64 * 8);
var n = hadara_coexisting_at(0 - 500, buf, 64);

# Consumer: get display rules for Japanese
var rule = hadara_display_rule(CID_JAPANESE);
var formality = display_formality(rule);  # 9/10

# Bridge: avatara traditions for Vedic-Hindu
var tbuf = alloc(8 * 8);
var nt = hadara_traditions(CID_VEDIC, tbuf, 8);  # Hindu, Buddhist, Jain, Vedic

# Hoosh: build LLM context
var ctx = hadara_context(CID_JAPANESE);  # rich text for system prompt
```

## Consumers

| Project | Usage |
|---------|-------|
| bhava | Cultural display rules — emotional expression modifiers by culture |
| avatara | Archetype → culture context mapping (via bridge.cyr) |
| joshua | Culturally authentic NPC behavior, world-building |
| natya | Narrative tradition → culture mapping |
| jnana | Structured cultural knowledge in the unified corpus |
| kshetra | Cultural layer on the spatiotemporal database |
| varna | Language/dialect ↔ culture associations |
| itihas | Cultural context for historical events (via bridge.cyr) |
| hoosh | LLM-grounded cultural queries (via hoosh.cyr) |

## Performance

33 benchmarks on x86_64:

| Operation | Latency |
|-----------|---------|
| Registry lookup | 6ns |
| Temporal query (50 cultures) | ~600ns |
| Practice/art medium search | ~800ns |
| Region search | 2μs |
| Influence chain (BFS) | 3μs |
| Context build (LLM) | 5μs |
| Bridge lookup | 7ns |

## Academic Sources

All cultural data is sourced from peer-reviewed scholarship. See `docs/sources/` for per-module bibliographies covering 40+ references including Stearns (2001), Kottak (2019), Shaw (2000), Brosius (2006), Basham (1967), Chang (2005), and others.

## License

GPL-3.0-only

## Part of AGNOS

[agnosticos.org](https://agnosticos.org) — the AI-native operating system.
