# Changelog

## Unreleased

- **The `sv` and `it` ladders** (one aggregated mint — Nabu P77-6 /
  №R-32 and P77-3 use cases): `sv` anchor (parent `non`, the isl
  precedent) with stage `old` (Old Swedish / fornsvenska, band
  [1225, 1526], wikt `gmq-osw`) — first consumer Fornsvenska
  textbanken, whose whole-source `sv:old` facet rule waits on this
  mint; `it` anchor (parent `roa`) with stage `old` (Old Italian,
  band [960, 1400], wikt `roa-oit`) — first consumer UD_Italian-Old
  (the Commedia under UD's one-tag `it`). Codemap: `swe: sv` and
  `ita: it` (the №11 alias suite), `gmq-osw: sv:old`,
  `roa-oit: it:old`.

- **The Ibero-Romance medieval flank** (Nabu P77-r6 / OSTA use case):
  `ast` anchor (Asturleonese, parent `roa`) with stage `old` (Old
  Leonese, band [1150, 1500]); `an` anchor (Aragonese, parent `roa`)
  with stage `old` (Navarro-Aragonese, band [1100, 1500] — one stage
  for the medieval complex, a /nav variety split deferred to a source
  that needs it); codemap row `arg: an` (the №11 alias suite). First
  consumer: OSTA's works-table lengua census (2,204 work rows —
  leonés, aragonés, navarro-aragonés, navarro among castellano/
  gallego/latín), riding as a raw facet until stage rules land.

- **The script-suffix codemap suite** (counts now 94 anchors,
  `codemap.yml` 48 mappings): 27 universal rows for BCP-47-style tags
  whose script subtag describes the content per the standard's own
  semantics (`san-Latn → san~latn`, the ogham family, the Sicilian
  epigraphic pairs, `xtg-Grek`…) — every row byte-verified
  surface-honest in the first consuming collection before earning its
  line; deviant artifact-claiming uses (egy-Egyd, -Ital-x-) stay
  per-collection by the standing rule. Ten new BARE anchors carry the
  targets (xtg/xcg under cel, osc under itc; xpi/xly/scx/xpu/ta/bra/awa
  parentless with honest classification notes — the Aramaic-fan
  discipline). Validator: `CODE_RE` admits Titlecase script subtags
  (keys are codes verbatim as the standards write them), and the P61
  gap is closed — a `~script` target on a missing anchor no longer
  slips the nil-entry branch.

Additions since the initial registry (counts now 41 anchors, 59
stages, 8 varieties, 2 orthographies; `codemap.yml` 20 mappings):

- **The script axis** (a DOCTRINE REVERSAL, pre-1.0 grammar change):
  `lect-id = anchor [":" stage] ["/" variety] ["~" script] ["@" ortho]`.
  The earlier README argued script should stay in BCP 47 subtags —
  measurement in the first consuming collection overturned that: the
  suffix convention in real catalogs carries two different claims with
  no way to say which (`san-Latn` a surface fact about a romanized
  edition; `egy-Egyd` an artifact fact riding Latin-transliteration
  text). The `~` axis is therefore defined to claim exactly one thing:
  **the script of the text as held**, machine-checkable against the
  bytes; the artifact's differing original script stays a
  consumer-side field, never folded into the lect id. Sigil `~`
  chosen over `&` deliberately: shell-safe mid-word and URL-unreserved
  where `&` backgrounds unquoted commands and separates query strings.
  Ships as: a **global `scripts:` table** (20 rows seeded from the
  consuming collection's measured need, surface and artifact both —
  keys are ISO 15924 lowercased, rows carry the canonical spelling;
  deliberately not per-anchor, since digraphia is open-ended and
  attestation is a collection fact); ortho rows gain a machine
  `script:` scope (`bohoric: latn`, `kyu: jpan` — previously prose
  notes); validator rules (grammar, table shape, referential integrity
  of `~` tags and ortho scopes); README/schema/site rewritten,
  including the retired "Why orthography but not script?" argument
  replaced by "Why a script axis?".

- Sumerian: the `sux` anchor with five stages (archaic ED I–II through
  post-Sumerian), and a separate `qpc` proto-cuneiform anchor whose
  note records the language-identity debate (no codemap row — its
  Sumerian identity is a separately ratifiable claim).
- Akkadian: the Assyrian axis (`old`/`oa`/`ma`) beside the Babylonian
  stages, and the `nb` band widened to fold the Late Babylonian
  through Parthian record.
- Egyptian: the `nk` (New Kingdom) stage, band [-1550, -1070],
  deliberately overlapping `mid` and `late` — the honest coarser claim
  for corpora dated at period grain across the Middle→Late transition.
- Grammar: stage/variety tags admit trailing digits (`sux:ur3`).
- **The ISO-parentage wave** (counts now 84 anchors, 60 stages): anchors
  mirroring ISO 639's Historical-type stage chains within the
  collection's focus axes — the Germanic ladders (Gothic; Old/Middle
  High German → German; Old Saxon → Middle Low German → Low German;
  Old/Middle Dutch → Dutch; Old/Western Frisian), all four Celtic
  ladders under a new `cel` family (Primitive Irish → Old → Middle →
  Irish; the Welsh, Breton and Cornish chains), Old Occitan → Occitan
  (the ISO code is literally `pro` — noted, no relation to the `:pro`
  stage convention), Old Spanish → Spanish, Mycenaean and Modern Greek
  beside `grc`, Avestan and the Persian chain (Old → Middle → Persian),
  the Armenian chain, the East Slavic moderns under `orv`, and
  Classical Syriac under `arc`. Modern chain-ends use ISO 639-1 (the
  `en`/`fr` precedent). Every row is an ISO/MARC fact — names,
  reference-date bands where MARC states them, parent edges from
  textbook philology; no new stages, no mode judgments. DELIBERATELY
  unminted, each needing its own ruling: the Aramaic dialect fan
  (jpa/tmr/sam/myz — overlaps the arc stage model), the Anatolian
  family, the Prakrits, Geez (no ISO chain exists). A 639-3 alias
  suite for modern ends (deu/nld/spa → de/nl/es) is deferred.

Initial registry:

- Project site (GitHub Pages from `docs/`): the case, the identifier
  grammar, and an integration guide for external tools.
- `lects.yml` — 39 anchors, 50 stages, 8 varieties, 2 orthographies:
  the Indo-European family spine with its reconstructed proto stages;
  the full Latin stage ladder with the Vulgar and Ecclesiastical
  registers; Greek (Homeric through Byzantine); Chinese (two stages and
  the Literary register); the English, French, Galician-Portuguese, and
  Tibetan descent ladders; Aramaic, Hebrew, Egyptian (with Coptic),
  Akkadian (the dialect × period grid with Standard Babylonian),
  Sanskrit, Church Slavonic (with recensions), Old East Slavic,
  Slovene, Bulgarian, Icelandic, Japanese, and Arabic.
- `codemap.yml` — 20 universal non-identity mappings (the Greek and
  Chinese stage codes, the Latin etymology-code suite, the
  reconstructed `-pro` family).
- `bin/validate` — standard-library Ruby validator: grammar,
  referential integrity, `ord` uniqueness, band sanity, Glottocode
  shape, parent-graph acyclicity; wired as the CI gate.
- Documentation: README (identifier grammar, genealogy model,
  stability policy), `docs/schema.md` (field semantics),
  `docs/prior-art.md` (the problem, the prior art, and why none of it
  suffices).

Pre-1.0: identifiers may change without notice until the first tagged
release.

## Unreleased — 2026-08-09 (the №1-№10 rulings batch, P64-6)

- Minted: ave:old/yng stages (contested-chronology bands noted) · cop/sah +
  cop/boh dialects · chu/cro (Croatian recension) · egy/trad (égyptien de
  tradition — a register, deliberately not a dating stage) · sl stage bands
  (old 950-1550, emod 1550-1850) + sl:mod · the Aramaic fan jpa/tmr/sam/myz
  as bare anchors parent arc (the standing deliberately-unminted note
  retired; sefaria arc:mid/jud rows stand — a different axis).
