# P(-1) Scaffold Hardening Audit — 2026-04-12

## Current State

- **13 cultures**, 190 assertions, 3,760 lines
- Phases 1-3 complete (minus avatara integration — blocked on port)
- HTTP server, CLI, graph traversal, consumer APIs all functional

## Internal Review Findings

### Code Quality
- **Clean**: All modules have source citations, consistent layout patterns
- **Test coverage**: 190 assertions across 5 sections — solid for current scope
- **Missing**: No build verification yet (can't run cc3 in this session — user builds)

### Data Accuracy Issues
1. **"Analerta" typo** in seed.cyr line 752 — should be "Analects" (论语)
2. **Aboriginal endonym missing** — no `hadara_set_endonym` call for culture #8. Complex: "Aboriginal Australian" is an exonym; there's no single endonym for 250+ language groups. Consider leaving blank or noting this explicitly.
3. **Egyptian end date 641 CE** — Shaw (2000) uses 30 BCE (Cleopatra/Roman conquest) as political end. 641 CE is Arab conquest which ended Coptic phase. Our choice is defensible but should be documented as "cultural end" vs "political end."

### Structural Issues
1. **No geographic region field** — itihas has `region` on every civilization. Hadara has `geo_roots_ptr/count` in the layout but never seeds it. Cultures need geographic anchoring.
2. **No language/script field** — itihas tracks scripts and language codes. For a culture library these are essential.
3. **No "values" seeded** — `values_ptr/count` exists in the layout, never populated.
4. **Consumer display rules are hardcoded by ID** — brittle. Should be driven by culture data (e.g., a formality score stored on the culture itself).

## External Research: Missing Cultures

### Critical gaps vs. itihas coverage (53 civilizations)

Hadara models **culture** (living or historical social identity), not **civilization** (political entity). But there are culture-bearing groups that any serious cultural library must include:

#### High Priority (consumers will immediately need these)

| Culture | Why | Source |
|---------|-----|--------|
| **Arab/Islamic** | One of history's most influential cultural spheres. Arts, sciences, calligraphy, literature. itihas has "Arab Caliphates" | Hourani (1991) *A History of the Arab Peoples* |
| **Korean** | Distinct from Chinese/Japanese. Hangul, kimchi, Confucian adaptation. itihas has Goryeo | Eckert et al. (1990) *Korea Old and New* |
| **Tibetan/Buddhist** | Major philosophical tradition, unique aesthetics. Bridges Indian→East Asian | Samuel (1993) *Civilized Shamans* |
| **Mesopotamian/Sumerian** | First urban culture, first writing. itihas covers but hadara doesn't | Kramer (1963) *The Sumerians* |
| **Mongol** | Largest contiguous empire, massive cultural exchange catalyst | Weatherford (2004) *Genghis Khan and the Making of the Modern World* |
| **Jewish/Hebrew** | One of the longest-lived cultural identities. Diaspora model essential | Seltzer (1980) *Jewish People, Jewish Thought* |
| **Byzantine/Orthodox** | Continuation of Roman East, distinct aesthetic and liturgical tradition | Mango (1980) *Byzantium* |
| **Polynesian** | Wayfinding, oral tradition, tattoo, haka. itihas has Tonga/Hawaiian | Howe (2006) *Vaka Moana* |

#### Medium Priority

| Culture | Why | Source |
|---------|-----|--------|
| **Aztec/Mexica** | Distinct from Maya. itihas covers | Townsend (2009) |
| **Inuit/Arctic** | Extreme environment adaptation, oral tradition | Stern (2004) *Inuit of the Arctic* |
| **Inca/Andean** | Quipu, terracing, non-literate empire. itihas covers | D'Altroy (2014) |
| **Ottoman/Turkish** | Bridge culture between East and West | Finkel (2007) *Osman's Dream* |
| **Southeast Asian (Khmer)** | Angkor, Hindu-Buddhist syncretism | Higham (2001) |
| **Swahili** | East African coast, Bantu-Arab synthesis | Nurse & Spear (1985) |
| **Yoruba** | Orisha tradition, Ifá divination, influence on diaspora religions | Bascom (1969) |
| **Berber/Amazigh** | North African indigenous, pre-Arab | Brett & Fentress (1996) |

#### Lower Priority (deeper content phase)

| Culture | Why |
|---------|-----|
| Inca/Quechua | Living Andean culture |
| Maori | Aotearoa, haka, tā moko |
| Sikh | Distinct from Hindu, martial + spiritual |
| Romani | Diaspora culture, oral tradition |
| Basque | Language isolate, pre-Indo-European |
| Armenian | Ancient Christian culture, diaspora |
| Ethiopian/Ge'ez | Aksumite heritage, coffee, unique script |
| Javanese | Gamelan, wayang, Hindu-Buddhist layering |

## Structural Gaps: What a culture library needs that we don't model

### 1. Geographic Region (missing from seed data)
Culture is spatial. We have the layout field but never populate it. Need:
- Primary region(s) as string
- Diaspora regions

### 2. Language and Script
Every culture has a linguistic identity. Need at minimum:
- Primary language name
- Script system
- ISO 639 code (where applicable)

### 3. Values / Worldview
The `values_ptr/count` field exists but is never used. Cultural values drive consumer behavior:
- Communal vs individual
- Sacred vs secular orientation  
- Linear vs cyclical time
- Nature relationship

### 4. Subculture Support
Hip-hop has regional variants (East Coast, West Coast, Southern). Japanese has Ainu subculture. These are Phase 4 but the type system should be ready.

### 5. Diaspora Tracking
Cultures move. African diaspora → Caribbean → Americas → Hip-hop. Jewish diaspora. Chinese diaspora. The layout has `diaspora_ptr/count` but it's never seeded.

### 6. Cross-reference to itihas
When itihas is ported to Cyrius, hadara cultures should be linkable to itihas civilizations. Need a field or convention for: "this culture was the cultural layer of these itihas civilizations."

## Recommended Actions (Priority Order)

1. **Fix typo**: "Analerta" → "Analects"
2. **Add 8 high-priority cultures** (Arab, Korean, Tibetan, Mesopotamian, Mongol, Jewish, Byzantine, Polynesian)
3. **Seed geographic regions** for all cultures (use the existing layout field)
4. **Add language/script field** to culture layout (expand CULTURE_SIZE)
5. **Seed values** for existing cultures
6. **Document the culture vs. civilization distinction** clearly for when itihas ports

## Decision: Culture vs. Civilization

Hadara is NOT itihas. Key distinction:

- **itihas** models political entities (empires, kingdoms, states) — they have borders, rulers, military campaigns
- **hadara** models cultural identities — they have practices, values, art, texts. They can outlive political collapse (Egyptian culture survived Roman conquest; Greek culture survived as Hellenism)

A single itihas civilization may host multiple hadara cultures (Roman Empire hosted Roman, Greek, Egyptian, Jewish, Christian cultures). A single hadara culture may span multiple itihas civilizations (Jewish culture spans Kingdom of Israel, Diaspora communities across many empires).

When avatara ports to Cyrius, it will need to map archetypes to cultures (the Warrior archetype manifests differently in Norse vs Japanese vs Roman culture) and to personages (historical figures live in a specific cultural context).

---

*Audit complete. Ready for action.*
