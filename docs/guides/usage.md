# Hadara Usage Guide

## As a Library

Include hadara in your Cyrius program:

```cyrius
include "lib/string.cyr"
include "lib/alloc.cyr"
include "lib/str.cyr"
include "lib/vec.cyr"
include "lib/syscalls.cyr"

# Helper functions needed by hoosh.cyr
fn to_cstr(s) { ... }
fn str_builder_add_buf(sb, ptr, len) { ... }

include "src/lib.cyr"
include "src/seed.cyr"

fn main() {
    alloc_init();
    hadara_init();
    hadara_seed();
    # ... your code here ...
    return 0;
}
var exit_code = main();
syscall(60, exit_code);
```

## Querying Cultures

### By ID

Culture IDs are deterministic constants defined in `CultureId` enum:

```cyrius
var c = hadara_get(CID_JAPANESE);   # get culture pointer
var name = culture_name_ptr(c);      # "Japanese"
var status = culture_status(c);      # CULTURE_ACTIVE
var start = culture_time_start(c);   # -300 (300 BCE)
```

### By Time

```cyrius
var buf = alloc(64 * 8);

# Which cultures existed in 500 BCE?
var n = hadara_coexisting_at(0 - 500, buf, 64);
# n cultures, IDs in buf[0..n-1]

# Did Egyptian culture exist in 1000 BCE?
var eg = hadara_get(CID_EGYPTIAN);
var existed = culture_existed_at(eg, 0 - 1000);  # 1 = yes
```

### By Region

```cyrius
var n = hadara_by_region("East Asia", 9, buf, 64);
# Returns: Japanese, Chinese, Korean, Ainu
```

### By Practice Category

```cyrius
var n = hadara_with_practice_category(PRACTICE_MARTIAL, buf, 64);
# Returns cultures with martial practices (Japanese budo, Chinese tai chi, etc.)
```

### Full-Text Search

```cyrius
var n = hadara_search_all("Nihon", 5, buf, 64);
# Searches across: name, endonym, region, language
```

## Graph Traversal

### Influence Chain (Forward)

"What did Egyptian culture influence?"

```cyrius
var n = hadara_influence_chain(CID_EGYPTIAN, buf, 32);
# Returns: Greek (direct), Roman (via Greek) — BFS order
```

### Lineage (Backward)

"Who are Roman culture's ancestors?"

```cyrius
var n = hadara_lineage(CID_ROMAN, buf, 32);
# Returns: Greek, Egyptian — BFS backward through REL_INFLUENCED edges
```

### All Relations

```cyrius
var n = hadara_all_relations(CID_GREEK, buf, 32);
# Returns all relation pointers involving Greek (as source or target)
```

### Temporal Relations

"Who was Egyptian culture interacting with in 400 BCE?"

```cyrius
var n = hadara_connected_at(CID_EGYPTIAN, 0 - 400, buf, 32);
# Returns culture IDs with active relations at that year
```

## Consumer APIs

### bhava — Display Rules

```cyrius
var rule = hadara_display_rule(CID_JAPANESE);
var f = display_formality(rule);       # 9 (very formal)
var e = display_expressiveness(rule);  # 3 (restrained)
var i = display_individualism(rule);   # 2 (collective)
var d = display_directness(rule);      # 3 (indirect)
```

### joshua — NPC Behavior

```cyrius
var cat = hadara_dominant_practice(CID_HIPHOP);  # PRACTICE_ART
var pct = hadara_sacred_ratio(CID_VEDIC);        # 100 (all sacred)
```

### natya — Narrative Traditions

```cyrius
var n = hadara_narrative_count(CID_WESTAFRICAN);  # 1 (Griot Storytelling)
var narr_buf = alloc(8 * 8);
var nc = hadara_narratives(CID_WESTAFRICAN, narr_buf, 8);
# narr_buf contains art form pointers with ART_ORAL_TRADITION or ART_LITERATURE medium
```

### jnana — Knowledge Export

```cyrius
var facts = hadara_fact_count(CID_HIPHOP);  # 19 total queryable facts
var total = hadara_total_facts();             # all facts across all cultures
```

## Cross-References

### avatara Bridge

```cyrius
var tbuf = alloc(8 * 8);
var n = hadara_traditions(CID_VEDIC, tbuf, 8);
# Returns 4: "Hindu", "Buddhist", "Jain", "Vedic"
# Pass these to avatara's by_tradition() function

# Reverse: which cultures use the "Buddhist" tradition?
var cbuf = alloc(16 * 8);
var nc = hadara_culture_for_tradition("Buddhist", cbuf, 16);
# Returns 5: Vedic, Japanese, Chinese, Korean, Tibetan
```

### itihas Bridge

```cyrius
var cbuf = alloc(8 * 8);
var n = hadara_civilizations(CID_PERSIAN, cbuf, 8);
# Returns 3: "Persian Empire", "Parthian Empire", "Sassanid Empire"
# Pass these to itihas civilization lookup functions
```

## Evolution Tracking

### Point-in-Time Status

```cyrius
var status = hadara_status_at(CID_SCOTTISH, 1800);
# Returns CULTURE_DORMANT (after 1746 Culloden, before 1970 revival)
```

### Transition History

```cyrius
var ebuf = alloc(16 * 8);
var n = hadara_evo_for(CID_SCOTTISH, ebuf, 16);
# Returns 3 transitions:
#   843: → ACTIVE
#   1746: ACTIVE → DORMANT
#   1970: DORMANT → REVIVED
```

## Hoosh Integration

### Context Builder (no network)

```cyrius
var ctx = hadara_context(CID_JAPANESE);
# Returns rich text:
# "Cultural context for Japanese:
#  Endonym: Nihon
#  Region: East Asia
#  Language: Japanese
#  Status: Active (living culture)
#  Core values: Wa, On, Mono no aware
#  Communication style: formality=9/10, expressiveness=3/10, ...
#  Key practices: Chado, Budo, Matsuri
#  Art forms: Shodo, Noh, Ukiyo-e, Gagaku
#  ..."
```

### Ask via Hoosh (requires hoosh running)

```cyrius
var response = hadara_ask(CID_JAPANESE, "What is the significance of tea ceremony?", 8088);
# POSTs to hoosh /v1/chat/completions with Japanese cultural context as system prompt
```

## Subcultures

```cyrius
var n = hadara_subculture_count(CID_HIPHOP);  # 3
var ids = hadara_subculture_ids(CID_HIPHOP);
# ids[0] = CID_EASTCOAST, ids[1] = CID_WESTCOAST, ids[2] = CID_SOUTHERN

# Check parent
var ec = hadara_get(CID_EASTCOAST);
var parent_ptr = load64(ec + CULTURE_PARENT_PTR);
var parent_id = load64(parent_ptr);  # CID_HIPHOP
```
