# Changelog

## v1.4.0 — 2026-08-29: the P88 anchor batch (Geʿez · Prakrit · Newar · Old Mandarin)

Four node-less constituencies of the consuming library, minted in one
aggregated package (the №R-53 ruling batch; the concurrent-mints rule):

- **`gez` (Geʿez)** — bare anchor, the Aramaic-fan discipline (no
  Semitic family node minted). Use case: the Geʿez shelf family was the
  largest node-less language left after the P81-r1 Anatolian mint —
  Beta maṣāḥǝft 3,774 docs + TraCES 15 + the Dillmann dictionary
  (13,727 entries). Band deliberately absent (Aksumite inscriptions to
  19th-century manuscripts; liturgically alive).
- **`pra` (Prakrit)** — collective ISO 639-2 anchor, parent `san`
  (the lineage edge: Middle Indo-Aryan continues from Old Indo-Aryan).
  DELIBERATELY coarse: the consuming corpus (SuttaCentral, 22 docs)
  claims no finer identity; pka/pmh/psu/pgd stay unminted until a
  consumer distinguishes them.
- **`nwc` (Classical Newari) + `new` (Newar, parent: nwc)** — the
  xct/bod two-anchor mold. Use case: the DACON gold-POS corpus
  (P88-A4, 4 docs / 977 passages), whose lect posture pends on exactly
  this node. Band [1100, 1900] from the attested span. No Sino-Tibetan
  family node (the Aramaic-fan discipline).
- **`zho:oman` (Old Mandarin)** — a third stage on the Chinese ladder
  (band [1200, 1455], after `mid`): the Yuan-era spoken standard the
  rhyme books attest. Use case: unblocks the menggu-ziyun shelf (the
  Menggu Ziyun, 1308, 'Phags-pa) and the parked zhongyuan-data
  question (Zhongyuan Yinyun, 1324) — no ISO code exists for Old
  Mandarin, so consumers tag those shelves honest-coarse `zho` and the
  `zho:oman` lect row refines.

Deliberately unminted, recorded: the Anatolian flank (already served,
P81-r1); finer Prakrit member codes; a Semitic or Sino-Tibetan family
node; Hittite stages (unchanged from the P81-r1 note).

## v1.3.0 — 2026-08-28: six scripts for the held-corpus surfaces (Nabu char-desk use case)

- Six rows join the global `scripts:` table — `tibt` (Tibetan), `ethi`
  (Ethiopic/Geʿez), `hang` (Hangul), `avst` (Avestan), `ugar`
  (Ugaritic), `xpeo` (Old Persian cuneiform). Naming rows only, no
  schema change: the registry stays the naming authority; mechanical
  codepoint→script facts live in the consumer's Unicode data (UCD
  Scripts.txt), joined on the lowercased ISO 15924 code.
- First consumers, per row (Nabu's held collections, censused
  2026-08-28): tibt — the Tibetan shelf family (84000, OTDO, SOAS,
  Derge); ethi — Beta maṣāḥǝft + Dillmann; hang — ONCOJ-adjacent
  Korean shelves and the Unihan kHangul stratum; avst — the TITUS
  Avestan corpus; ugar — the Copenhagen Ugaritic Corpus and RSTI's
  Unicode cuneiform editions; xpeo — Achemenet. Ruling: №R-49(c)
  (owner, 2026-08-28, "as recommended").
- Unblocked downstream: `~script` lect ids on these six (previously
  resolved nil), artifact-script records for Tibetan/Avestan/Old-
  Persian texts held in Latin transliteration (previously rejected as
  unregistered tags), and script-naming for the consumer's char desk.
- Deliberately unminted: any further scripts without a consuming
  collection (the table grows by measured need, per its own header).

## v1.2.0 — 2026-08-26: the Early Modern English stage (EEBO use case)

- `en:early` (Early Modern English, band [1500, 1700]) under the
  existing `en` anchor (parent `enm` — the descent chain en ← enm ←
  ang is untouched). First consumer: Nabu's eebo-tcp source
  (EEBO-TCP wave 1 = Phase I, 25,368 texts, №R-43 ruled
  2026-08-26): the corpus census puts ~130 of 60k texts before
  1500 — the collection is squarely early-modern, and imprint-year
  date-band inference stages it against this band (the no:old/
  Menota precedent). Ruling: №R-43 + the owner's explicit "en:early
  stage mint ok". Deliberately unminted: any internal EModE split
  (Elizabethan/Jacobean etc. — no consumer distinguishes one).

## v1.1.0 — 2026-08-24: the Norwegian and Danish descent ladders (Menota use case)

- `no` anchor (parent `non`, the isl/sv precedent) with stage `old`
  (Old Norwegian / gammelnorsk, band [1050, 1350]); `da` anchor
  (parent `non`) with stage `old` (Old Danish / gammeldansk, band
  [1100, 1525], wikt `gmq-oda`). Codemap: `nor: no`, `dan: da` (the
  №11 alias suite — macrolanguage rows claiming nothing historical),
  `gmq-oda: da:old` (the gmq-osw sibling). First consumer: Nabu's
  menota source (91 Medieval Nordic mss; nor 27 · dan 2 — the Menota
  Handbook's own modern-code + manuscript-dating doctrine, staged by
  date-band inference plus one facet rule). The `no` anchor note
  documents the macrolanguage status and the Bokmål/Nynorsk descent
  trap (prose, never edges); `nb`/`nn`, `no:mid` (band pre-named in
  the old stage's note), a Danish mid split, and any Scanian variety
  stay deliberately unminted. Ruling №R-42 (2026-08-24), survey on
  file in the consuming collection.

## v1.0.0 — 2026-08-23

The first tagged release. The registry ships **110 anchors, 68
stages, 19 varieties, 2 orthographies, 20 scripts; codemap.yml 67
mappings** — validator-checked (`bin/validate`, CI-wired), with one
live consumer (Nabu: 148 rule/override/codemap targets resolving,
zero drift). From this tag the README's Stability contract is
ACTIVE: renaming/removing a lect id or changing a `mode` is a major
version; new anchors/stages/varieties/orthographies and new codemap
rows are minor; bands, notes, and crosswalks are patch. An existing
codemap row never changes target within a major version.

Everything below is this release — the two pre-tag accumulation
sections folded (2026-08-09 rulings batch inline at the end).

- **GRAMMAR WIDENING (pre-v1.0.0 window item — №R-41, owner-ruled
  2026-08-21):** variety tags widen from 2–5 to 2–8 lowercase
  alphanumerics, mirroring the ortho slot, so IANA variant subtag
  names ride verbatim (`oc/lengadoc`, `oc/vivaraup`). Additive: every
  existing identifier stays valid; only consumers with the old grammar
  compiled into a regex need the one-character update — which is
  exactly why this lands before the first tag (№R-40's sequencing).
  Touches `docs/schema.md` (the stated grammar), `bin/validate`
  (LECT_RE + the variety-tag check), and the README variety bullet
  (which now also states the reuse-IANA-names doctrine the ortho axis
  always had — shared).

- **The `oc` dialect varieties** (№R-41 / Nabu P81-r2, Option A of the
  dialect-placement design): seven `kind: dialect` varieties under
  `oc`, tags IANA-verbatim per the 2018 Occitan registration —
  `gascon`, `lengadoc`, `provenc`, `auvern`, `lemosin`, `vivaraup`
  (Bec's six-dialect classification = the first consuming corpus's own
  division) plus `aranes` (the Val d'Aran variety of Gascon; the
  gascon ⊃ aranes nesting carried in prose — the flat variety set is
  deliberate). First consumers: lo-congres (6 oc docs / 5,152 aligned
  pairs, upstream's `dialect` facet carries exactly these six names
  letter-for-letter) and aranese (~420k pairs, definitionally
  `oc/aranes`); the Nabu-side facet rule and override ride the
  standing queue until this merges. Deliberately unminted:
  `nicard`/`cisaup`/`creiss` (IANA-registered, no holdings), the
  Occitan orthography variants (`grclass`/`grital`/`grmistr` — no
  source distinguishes orthography), CTILC's Catalan variants (no `ca`
  anchor; a later mint) and glaux's Greek dialect labels
  (metadata-only, their own future ruling). The `oci: oc` codemap
  alias (this PR's alias package) does double duty as this package's
  code-level rung.

- **The alias-suite completion** (Nabu P81-r1, closing the 2026-08-21
  maturity-review gap — 50.4k documents re-laddered): the №11
  639-3 ↔ 639-1 suite applied to every remaining same-language pair in
  the first consuming collection, each corpus code sample-verified
  against its held documents before earning its row. Toward the
  registry's two-letter anchors: `eng: en` (36,970 docs — the
  translation layers of oracc/rundata/elephantine/suttacentral…),
  `ger: de` (12,988 — the AES German translation layer; the 639-2/B
  bibliographic twin of the already-mapped `deu`), `fas: fa` (351,
  openiti Persian), `fra: fr` (80, RIIG French translations),
  `oci: oc` (7, Lo Congrès/Aranese), `gle: ga` (2, ogham — upstream
  distinguishes gle from its pgl/sga rows deliberately), `cym: cy` and
  `cor: kw` (1 each, local-library grammars). Mirrored where the
  registry anchored the 639-2/3 code: `ar: ara` (12, ddbdp Arabic
  papyri — bismillah openings verified) and `is: isl` (3, UD
  IcePaHC). Plus `syr: syc` (2, elephantine — Syriac-script Christian
  ostracon verified): 639-2 Syriac read in its pre-2007 classical
  scope, the gkm precedent; modern Neo-Aramaic collections override
  per-collection.

- **The Anatolian flank** (Nabu P81-r1 use case — the owner's
  2026-08-21 review request retired the standing deliberately-unminted
  note): `ine-ana` family anchor (Anatolian, parent `ine`) carrying
  `hit` (Hittite, band [-1650, -1180], 35,899 docs: tlhdig 21,209 +
  cdli 14,671), `xlu` (Cuneiform Luwian, 209), `hlu` (Hieroglyphic
  Luwian, 2) and `plq` (Palaic, 30); plus the Boğazköy-archive
  neighbors as parentless bare anchors per the Aramaic-fan discipline —
  `xht` (Hattic, isolate, 326), `xhu` (Hurrian, 832) and `xur`
  (Urartian, 703; Hurro-Urartian has no family node and no consumer
  needing one). `hit` is DELIBERATELY stage-less: the census showed no
  consuming source carries per-document stage data — CDLI's period
  facet is a single blanket ("Middle Hittite (ca. 1500-1100 BC)",
  14,653 of 14,671) and TLHdig carries only CTH numbers and project
  sigla — so the conventional Old/Middle/New grid waits for a consumer
  that can materialize it.

- **The `de:early` stage** (Nabu P80-5 use case): Early New High
  German under the existing `de` anchor (parent `gmh`), band
  [1350, 1650] per conventional Germanistik — ENHG has no ISO code
  and `gmh`'s band stops ~1500, so ReF (Referenzkorpus
  Frühneuhochdeutsch, 190 texts / 3.1M tokens, the third rung of
  the Bochum reference-corpus ladder after ReM/ReN) would otherwise
  ride bare anachronistic `de`. First consumer: Nabu's `ref` source,
  whose whole-source facet rule waits on this mint (the sv:old
  add-then-retire shape). Deliberately coarse: no internal
  ENHG-period split — nothing held distinguishes one.

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
release. (That window closed with this tag — the one doctrine
reversal it existed for, the `~script` axis, is above.)

### 2026-08-09 — the №1-№10 rulings batch (P64-6)

- Minted: ave:old/yng stages (contested-chronology bands noted) · cop/sah +
  cop/boh dialects · chu/cro (Croatian recension) · egy/trad (égyptien de
  tradition — a register, deliberately not a dating stage) · sl stage bands
  (old 950-1550, emod 1550-1850) + sl:mod · the Aramaic fan jpa/tmr/sam/myz
  as bare anchors parent arc (the standing deliberately-unminted note
  retired; sefaria arc:mid/jud rows stand — a different axis).
