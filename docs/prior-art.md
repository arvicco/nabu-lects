---
title: "Why another language classification? Prior art and the case for lects"
---

# Why another language classification? Prior art and the case for lects

Every text in a digital library carries a language tag. This document explains why the
existing tagging systems — ISO 639, Glottolog, BCP 47, Wiktionary's code space, and the
conventions of working corpora — cannot, alone or together, answer a question that any
library of ancient and medieval texts must answer constantly: **which language or
dialect, at what broad stage of its historical development, is this document written
in?** It reviews each system on its merits, shows where each falls short of that
requirement, and motivates the design this repository implements: a small, scoped
registry of *lects*.

---

## 1. The problem

[Nabu](https://github.com/arvicco/nabu) is a research library holding roughly a million
documents — some 68 million text passages — across more than 120 language codes: from
Sumerian administrative tablets and Ugaritic ritual texts through Greek drama, the Latin
of Cicero, Jerome, and twelfth-century chroniclers, to Classical Chinese, Tibetan
canons, and the medieval lyric of Galicia. Every document carries a standard language
code. And the codes, taken at face value, routinely tell less than the truth:

- **One code, two thousand years.** `lat` covers Plautus, Cicero, the Vulgate, the
  monastic charters of the twelfth century, and Vatican encyclicals — there is no ISO
  code for Old, Late, Medieval, or Neo-Latin. `grc` ("Ancient Greek, to 1453") spans
  Homer, Attic drama, the Septuagint, the New Testament, and the whole Byzantine
  millennium; the 1453 boundary is the fall of Constantinople, a library-cataloguing
  convention rather than a linguistic one.
- **A register coded as if it were a stage.** `lzh` "Literary Chinese" names a *written
  register* — wenyan — used continuously for some two millennia alongside the spoken
  language's actual stages (`och` Old Chinese, `ltc` Late Middle Chinese sit beside it
  in ISO as if they were siblings of the same kind). In a large library this is not a
  corner case: Literary Chinese is over 13 million passages here, the second-largest
  holding.
- **Attested language and reconstruction fused in one code.** The Wiktionary code
  `la-vul` "Vulgar Latin" is used both for *attested* substandard Latin (the Appendix
  Probi's scoldings — "speculum non speclum") and for the *reconstructed* Proto-Romance
  of the comparative method (the DÉRom dictionary's asterisked étymons). These are
  categorically different objects — one is evidence, the other is inference — and any
  machinery that treats reconstructions specially (asterisk display, etymological
  closure) breaks when a single code means both. The mirror image also occurs: the code
  `gmq-pro` "Proto-Norse" is worn by real Elder Futhark inscriptions — attested
  epigraphy filed under a reconstruction label.
- **Lumping that loses real distinctions.** A single `arc` shelf can hold Imperial
  Aramaic documents, Qumran Biblical Aramaic, and the Targums' Jewish Literary Aramaic
  — a millennium of distinct varieties (here ISO is actually *finer* than common
  practice: it splits `oar`, `arc`, `jpa`, `tmr`, `syc`, `myz`). Rabbinic and Medieval
  Hebrew have no code at all beside `hbo`/`heb`. Church Slavonic's `chu` covers both
  canonical Old Church Slavonic and the later Russian and Serbian recensions.
- **Genealogy that forks below the stage.** Old Galician-Portuguese (`roa-opt`) is one
  medieval lect with two modern descendants, Portuguese and Galician — the family tree
  branches *underneath* a historical stage, which no flat code list can express.
- **Orthographic epochs.** The same modern language may be printed in reform-era
  variants — Japanese kyūjitai vs shinjitai, pre-Petrine vs modern Cyrillic — which are
  neither stages nor dialects, but which a philological library must record.

Occasionally the standards get it right by accident: Tibetan has three clean ISO codes
(`otb` Old Tibetan, `xct` Classical Tibetan, `bod` modern Tibetan), and English, French,
German, and Irish each received historical-stage codes. But that coverage is accidental
— it exists where a scholarly community happened to lobby for a code, and nowhere else.

The requirement, stated once: **an identifier that names unambiguously which
language/dialect at what broad historical development stage a document or dictionary
entry belongs to** — with genealogy recoverable, reconstructions distinguished from
attested varieties, registers and orthographies honestly recorded, and every code in
actual use mappable onto it. The sections below measure the existing systems against
that requirement.

---

## 2. Prior art

### 2.1 The ISO 639 family

ISO 639 is the bibliographic standard: part 1 (2-letter codes, ~180), part 2 (3-letter
bibliographic codes, ~480, including collective codes), part 3 (comprehensive individual
languages, ~7,900, maintained by SIL International), and part 5 (language families and
groups: `gem` Germanic, `sla` Slavic, `roa` Romance, `ine` Indo-European…). Since
**ISO 639:2023** these parts are consolidated into a single standard.

ISO 639-3 classes every language as living, extinct, constructed, or **historic**, and
the definition of "historic" is load-bearing: *"A language is listed as historic when it
is considered to be distinct from any modern languages that are descended from it: for
instance, Old English and Middle English… the language have a literature that is treated
distinctly by the scholarly community."* So ISO *does* recognize historical stages as
codable languages — but only where someone filed a successful change request. The result
is accidental coverage:

- **English**: `ang` Old English (ca. 450–1100), `enm` Middle English (1100–1500) —
  plus an IANA variant subtag `en-emodeng` for Early Modern English (no ISO code).
- **French**: `fro` Old French (842–ca. 1400), `frm` Middle French (ca. 1400–1600).
- **German**: `goh` Old High German (ca. 750–1050), `gmh` Middle High German
  (ca. 1050–1500); `gml` and `dum` on the Low German / Dutch side.
- **Irish**: `sga` Old Irish (to 900), `mga` Middle Irish (900–1200).
- **Spanish**: `osp` Old Spanish (to ca. 1500). **Greek**: `grc` vs `ell`, split at
  1453 — the reference names and date bands descend from Library of Congress / MARC
  cataloguing practice, not from historical linguistics.
- **Latin**: nothing. One code from Plautus to the present.
- **Chinese**: `och` Old Chinese, `ltc` Late Middle Chinese, and `lzh` Literary
  Chinese — a register coded as a sibling of two stages, the conflation embodied in
  the standard itself.
- **Tibetan**: `otb`, `xct`, `bod` — the clean case.
- A private-use range `qaa`–`qtz` exists for codes with no ISO assignment.

Who draws the boundaries? For part 2, library cataloguing tradition; for part-3
additions, whoever files a change request that SIL's registrar accepts (the batch of
ancient and historic codes largely came from the LINGUIST List — §2.3). There is no
principled periodization authority: `enm` ends at 1500 because bibliographers said so;
the Helsinki Corpus ends Middle English at 1500 via its own period M4 (1420–1500); and
neither cites the other.

**ISO 639-6 — the hierarchy that died.** There *was* a direct attempt at the whole
problem. ISO 639-6, published 2009-11-17, assigned alpha-4 codes for "comprehensive
coverage of language variants" in a recursive hierarchy, researched by the registration
authority GeoLang — genealogy and variant depth in one code space, exactly the shape a
historical library wants. It was **withdrawn on 2014-11-25**, citing concerns about its
usefulness and maintainability, and the lack of standardization across recursive
hierarchies. Its life and death is the central cautionary tale for this repository: a
*global* hierarchical registry of language variants proved unmaintainable. (The design
lesson drawn here is that a *scoped, single-maintainer* registry — a hundred-odd records
covering one library's actual holdings — is precisely the case where the same idea
works.) ISO 639-4:2010, for completeness, contains guidelines and principles only, no
codes.

### 2.2 Glottolog

Glottolog (glottolog.org) catalogues *languoids* at three levels — family, language,
dialect — each with a stable Glottocode, under expert-curated genealogical
classification. It is the best genealogy in existence, and it handles the
attested-ancestor problem with a characteristic device:

- **Latin** (`lati1261`, level *language*, extinct) sits at the bottom of a chain of
  *pseudo-family* nodes: Indo-European > Classical Indo-European > Italic >
  Latino-Faliscan > Latinic > … > **Imperial Latin** (`impe1234`, level: *family*) >
  Latin. The Romance languages hang under that same Imperial Latin node — that is,
  Glottolog expresses "Latin is the ancestor of Romance" by minting a family node named
  after the ancestor and placing the attested ancestor inside it as a leaf **sister**
  of its own descendants.
- **Old English** (`olde1238`, "Old English (ca. 450–1100)", ISO `ang`) likewise:
  … Anglic > Anglo-Saxon > Old English, with Middle English a separate languoid further
  down the Anglic tree. Note that the timespan lives in the languoid's *name*, not in a
  data field.
- **Proto-languages and reconstructions are excluded by design** — Glottolog documents
  attested languoids only; there is no Proto-Indo-European node, no Proto-Slavic.
- Ancient *regional* dialects fare well (Attic and Doric Greek exist as dialect
  languoids); *diachronic* stages below an ISO-coded language do not: there is no Koine
  node, no Byzantine Greek distinct from `grc`/`ell`, nothing for Medieval Latin.

### 2.3 MultiTree and the LINGUIST List codes

The LINGUIST List defined the supplemental ISO-format codes for ancient and historic
languages that later entered ISO 639-3, and minted local-use codes where ISO declined —
`gkm` for Medieval (Byzantine) Greek is a LINGUIST List code, which Wiktionary adopted
and ISO still lacks. MultiTree aggregated *hypothesis trees* of language relationships,
including proto-language nodes. The infrastructure is aging — LL-MAP is defunct,
MultiTree updates have stalled — though Wikidata still tracks the codes as property
P1232. A quarry for precedent when new codes are needed; not a foundation to build on.

### 2.4 BCP 47 and the IANA Language Subtag Registry

BCP 47 (RFC 5646) defines the tag grammar the web runs on:
`language[-extlang][-script][-region][-variant…][-extension][-x-privateuse]`. Three
findings matter here.

**(i) The registry really does hold historical-stage and orthography variants** —
verified against the current IANA registry:

| Variant | Description | Prefix |
|---|---|---|
| `vaidika` / `laukika` / `itihasa` / `bauddha` | Vedic / Classical / Epic / Buddhist Hybrid Sanskrit | `sa` |
| `emodeng` | Early Modern English (1500–1700) | `en` |
| `1606nict` | Late Middle French (to 1606) | `frm` |
| `1694acad` | Early Modern French | `fr` |
| `1901` / `1996` | German orthography, traditional / 1996 reform | `de` |
| `petr1708` / `luna1918` | Russian Petrine / post-1917 orthography | `ru` |
| `polyton` / `monoton` | Greek polytonic / monotonic | `el` |
| `bohoric` / `dajnko` / `metelko` | Slovene historical alphabets | `sl` |
| `baku1926` / `tarask` / `alalc97` … | Turkic unified Latin, Taraškievica, transliteration schemes | various |

So BCP 47 already models **stage** (`sa-vaidika`, `en-emodeng`) and **orthography**
(`ru-petr1708`) as variant subtags on a base language — two of the exact axes needed
beyond genealogy. But the registered set is anecdotal: Sanskrit received a full stage
suite (one motivated registrant, 2010); Greek received nothing diachronic; Latin
nothing at all.

**(ii) Could private-use subtags (`la-x-vulgar`, `grc-x-koine`) carry the whole need?**
Syntactically yes — `x-` subtags are unrestricted and always well-formed. But they are
*semantically opaque by definition* (RFC 5646 §2.2.7: meaning by private agreement
only), invisible to every external consumer, carry no genealogy and no dates, and
cannot be validated. Registering real variants is possible — a template to
ietf-languages@iana.org, reviewed by the Language Subtag Reviewer, typically a matter
of weeks per subtag — but that publishes one project's periodization decisions to a
global registry one negotiation at a time, and still provides no family walk. The
`extlang` mechanism is a closed set for macrolanguage bridging (`zh-`, `ar-`, `ms-`…),
unusable for stages.

**(iii) What is genuinely worth adopting**: the grammar discipline (ordered axes,
lowercase, registry-validated well-formedness), the registered variant names as
ready-made orthography vocabulary (`petr1708`, `1901`, `bohoric`…), and the
demonstration that language-shaped codes with a stage variant are readable and
sortable by humans.

### 2.5 Wiktionary's code space (and Wikidata lexemes)

Wiktionary maintains the de-facto richest stage vocabulary in existence — the code
space any etymological aggregator ends up joining against. Three tiers:

- **Full languages** — the ISO set plus community additions under nonstandard codes:
  `gkm` (Medieval Greek, promoted from etymology-only to full language), `roa-opt`
  (Old Galician-Portuguese), `zle-ort` (Old Ruthenian), and others.
- **Etymology-only languages** — codes usable in etymologies and labels but not as
  entry headers, each with a declared parent: a full Latin stage suite (`la-vul`
  Vulgar, `la-lat` Late, `la-med` Medieval, `la-ecc` Ecclesiastical, `la-ren`
  Renaissance, `la-new` New, with Old Latin as `itc-ola`), `grc-koi` Koine Greek, and
  dozens more.
- **Reconstructed languages** — `<family>-pro` codes (`ine-pro`, `gem-pro`,
  `sla-pro`…) whose entries live in a dedicated `Reconstruction:` namespace, plus
  family codes reusing ISO 639-5. Parent/ancestor chains are machine-readable in the
  project's module data, so a genealogical walk exists — though as a wiki artifact.

**The `la-vul` lesson comes from Wiktionary's own guidelines** (Wiktionary:About
Vulgar Latin): attested Vulgar Latin words are entered in mainspace *as Latin* with a
"Vulgar Latin" label, while unattested comparative-method forms live under
`Reconstruction:Latin/…` — that is, even Wiktionary internally splits what the single
code `la-vul` externally fuses. Any downstream system that adopts the code inherits
the fusion.

**Governance**: the code tables change by editor consensus; codes are renamed, merged,
promoted (as `gkm` was), and occasionally deleted. Excellent as an *input* to a mapping
table; unacceptable as the identifier layer of a library that promises stable
citations.

**Wikidata lexemes**, for completeness: a lexeme's language may be any Wikidata item,
so "Medieval Latin" or "Koine Greek" can serve as a lexeme language wherever an item
exists, and forms can carry orthography qualifiers. But coverage for ancient lects is
thin, there is no controlled stage taxonomy, and the identifiers are opaque Q-numbers.
An interoperability target someday; not a base.

### 2.6 Corpus and philological practice

What the working corpora actually do is the strongest signal in this survey:

- **The Helsinki Corpus of English Texts**: one language, *period parameters* per
  text — O1–O4 for Old English (to 850, then by century), **M1 1150–1250, M2
  1250–1350, M3 1350–1420, M4 1420–1500**, E1–E3 for Early Modern (1500–1570–1640–
  1710). Stage is a *banded date attribute*, not a language code.
- **PROIEL, TOROT, ISWOC** (the classic historical treebank family): ISO codes
  (`grc`, `lat`, `got`, `chu`, `orv`, `ang`) with stage carried by corpus membership
  and per-text dates — TOROT's `orv` deliberately spans Old East Slavic through
  Middle Russian.
- **Universal Dependencies**: stage lives in the *treebank name* while the code stays
  coarse — UD_Latin-Perseus (classical), UD_Latin-ITTB (Aquinas), UD_Latin-LLCT
  (early-medieval charters), UD_Latin-UDante, all tagged `la`; UD_Ancient_Greek-PROIEL
  mixes Herodotus and the New Testament under one `grc`. UD_Old_French and
  UD_Classical_Chinese exist exactly where ISO happened to grant a code — the
  conflations downstream projects inherit *are* UD's.
- **TEI**: `@xml:lang` is BCP 47 by mandate; the Guidelines point to private-use and
  variant subtags for finer distinctions and to `<langUsage>` prose for the rest —
  TEI outsources the problem to BCP 47 and metadata.
- **Reference-work periodization is per-language and non-aligned**: Latin philology's
  Old/Classical/Late/Medieval/Neo bands; Greek's Homeric/Classical/Koine/Byzantine
  (Koine conventionally ~300 BCE–330 CE); Egyptology's Old/Middle/Late/Demotic/Coptic;
  Assyriology's Old/Middle/Neo-Babylonian and -Assyrian dialect-period grid, tagged
  per text in ORACC. No two fields draw compatible bands — so any registry spanning
  fields must delegate band semantics to per-language decisions.
- **OLAC, CLARIN CMDI, lexvo**: all bind identification to ISO 639-3; nothing to add
  on stages.

*The pattern:* everyone keeps the code coarse and hangs stage off metadata and dates.
Nobody has promoted stage into the identifier itself — because nobody else has needed
one identifier to disambiguate holdings spanning a hundred-plus code systems at once.
A library that does faces the gap directly.

---

## 3. Why none suffices

Eight requirements, from §1's problem statement:

(a) an unambiguous language×stage identifier · (b) genealogy recoverable ·
(c) proto, ancient, medieval, and modern varieties in one system ·
(d) registers and sociolects honestly distinguished from stages ·
(e) every code in actual use mappable onto it · (f) stable, sortable,
human-readable identifiers · (g) date-band anchoring · (h) maintainable
by a small team.

| System | a | b | c | d | e | f | g | h |
|---|---|---|---|---|---|---|---|---|
| ISO 639-1/2/3/5 | ✗ (`lat`, `grc`) | ✗ | ✗ (no proto) | ✗ (`lzh`) | — (it *is* the source) | ✓ | ~ (names only) | ✓ (frozen) |
| ISO 639-6 | ~ | ✓ | ~ | ~ | ✗ | ✗ | ✗ | ✗ **withdrawn** |
| Glottolog | ✗ (no Koine, no Medieval Latin) | **✓** | ✗ (no proto) | ✗ | ~ | ~ (opaque codes) | ~ (in names) | ✓ (consume-only) |
| MultiTree / LINGUIST List | ~ | ~ | ~ | ✗ | ~ | ~ | ✗ | ✗ (moribund) |
| BCP 47, registered variants | ~ (where they exist) | ✗ | ✗ | ✗ | ~ | ✓ | ✗ | ✗ (global process) |
| BCP 47, `x-` composition | ✓ syntactically | ✗ | ~ | ~ | ✓ | ~ (opaque semantics) | ✗ | ✓ |
| Wiktionary codes | ✗ (`la-vul`) | ~ (module chains) | **✓** | ~ (conflated) | **✓** | ✗ (wiki churn) | ✗ | ✗ (not ours to govern) |
| Wikidata lexemes | ~ | ~ | ~ | ~ | ~ | ✗ | ~ | ✗ |
| Corpus metadata pattern | ✓ *per corpus* | ✗ | ✗ | ~ | ✓ | ✗ (no identifiers at all) | **✓** | ✓ |

Stated fairly, per system:

- **ISO 639** is the indispensable anchor vocabulary — stable, universal, frozen — and
  it is not a classification. Its stage coverage is an accident of lobbying history
  (English yes, Latin no), it has no proto layer, and it codes at least one register
  (`lzh`) as if it were a stage. It is where identifiers should be *anchored*, not
  where the distinctions live.
- **ISO 639-6** attempted the right thing at the wrong scale, and was withdrawn as
  unmaintainable — the cautionary tale, not an option.
- **Glottolog** has the best genealogy in existence, and its chained pseudo-family
  device makes even attested-ancestor walks possible (Latin > Romance). But it
  excludes reconstructions by design, stops staging where ISO codes stop (no Koine,
  no Medieval Latin), has no register axis, and its identifiers (`lati1261`) are not
  human-readable. It earns its place as a *crosswalk field*, not as the identifier.
- **BCP 47** contributes syntax discipline and a genuinely useful registered
  orthography vocabulary, but its historical-stage coverage is anecdotal, its
  governance is global (one negotiation per subtag), private-use subtags are
  semantically opaque by definition, and no BCP 47 tag can name a proto-language ISO
  never coded.
- **Wiktionary's code space** has the richest stage coverage anywhere and
  machine-readable ancestor chains — and it embeds the exact `la-vul`
  attested/reconstructed fusion this work needs to kill, under wiki governance where
  codes are renamed and merged by consensus. Map *from* it; do not build *on* it.
- **Corpus practice** (Helsinki's date bands, PROIEL's per-text dates, UD's
  name-borne stages) validates the two-layer architecture — coarse code plus rich
  stage metadata — but supplies no identifiers at all: each corpus's periodization is
  internal to that corpus.

No row passes. The nearest thing to a pass is a *composition*: Wiktionary's coverage
(c, e) + Glottolog's genealogy (b) + BCP 47's syntax and orthography vocabulary (f) +
the corpus world's date-band semantics (g), under a scoped registry that a small team
can actually maintain (a, d, h).

---

## 4. The conclusion: compose, under one roof

That composition is what this repository implements. The unit is the **lect** — the
standard linguistics term for "any variety of a language, without commitment to its
status" — and each lect identifier composes four axes:

```
lect-id  =  anchor [ ":" stage ] [ "/" variety ] [ "@" ortho ]
```

- the **anchor** is an ISO 639 or established Wiktionary code — the most specific
  genealogical node (language or family) the lect hangs from, keeping every
  identifier legible to anyone who knows the standard codes;
- the **stage** names a broad historical development stage from that anchor's
  registered vocabulary, with the registry recording each stage's date band and its
  **mode** — attested or reconstructed — as data, not as a naming convention;
- the optional **variety** carries registers, sociolects, and recensions — the axis
  the standards conflate with stage;
- the optional **orthography** tag carries reform-era spelling systems, reusing IANA
  variant names where they exist.

Worked examples: `lat:med` — Medieval Latin, at last distinct from Cicero's `lat:cla`;
`grc:koi` — Koine Greek, which no standard codes; `zho/lit` — Literary Chinese as what
it is, a register of Chinese rather than a stage; `roa:pro` — Proto-Romance, anchored
to the Romance family with `mode: reconstructed`, cleanly separated from the attested
Vulgar Latin (`lat/vul`) that shares its Wiktionary code. A bare anchor remains legal
and means the anchor's whole span — honest coarseness where nothing finer is known.
Where ISO already codes the stage (`ang`, `fro`, `gmh`, `otb`, `xct`…), the lect *is*
the bare anchor, and the mapping is the identity — the common case costs nothing.

Each registry record carries its Glottocode (making Glottolog's genealogy available as
a crosswalk rather than a maintenance burden), its parent lect, its date band with a
source note (bands are per-language scholarly decisions, recorded, never derived), and
its mode. Existing codes map onto lects per collection, with a per-document escape
hatch for corpora that span centuries under one tag.

The scope is deliberately what ISO 639-6's was not: not the world's languages, but the
languages a real library actually holds — on the order of a hundred registry records,
maintained where the holdings are, growing only when a holding forces a distinction.

The registry itself — the full identifier grammar, the schema, the stage vocabularies,
and the mapping discipline — is specified in this repository's README and schema
documentation.

---

## Sources

- ISO 639-6 publication and withdrawal: en.wikipedia.org/wiki/ISO_639-6;
  iso.org/standard/43380.html
- ISO 639-3 language types: iso639-3.sil.org/about/types
- Glottolog: glottolog.org/glottolog/glottologinformation; resource pages for
  `lati1261`, `impe1234`, `olde1238`
- IANA Language Subtag Registry: iana.org/assignments/language-subtag-registry
  (variant survey via en.wikibooks.org/wiki/Module:Language/data/iana_variants;
  r12a.github.io/app-subtags); RFC 5646, RFC 5645
- Wiktionary: en.wiktionary.org/wiki/Wiktionary:About_Vulgar_Latin;
  Category:Vulgar_Latin; Category:Medieval_Latin;
  Wiktionary:List_of_languages/special
- LINGUIST List / MultiTree:
  language-archives.org/wg/language-codes/linguist-20020219.html;
  github.com/linguistlist/multitree; wikidata.org/wiki/Property:P1232
- Helsinki Corpus periods: helsinkicorpus.arts.gla.ac.uk;
  varieng.helsinki.fi/CoRD/corpora/HelsinkiCorpus/
