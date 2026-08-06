# nabu-lects

**Project site: [arvicco.github.io/nabu-lects](https://arvicco.github.io/nabu-lects)** — the case, the grammar, and an integration guide.

A small, curated registry of **lects** — language varieties identified by
genealogical anchor × historical stage × variety × orthography — with a
universal mapping from standard language codes (ISO 639, Wiktionary) onto
them.

Standard codes routinely under-describe historical text collections: `lat`
covers Plautus and twelfth-century charters alike, `grc` spans Homer to 1453,
`lzh` codes a written register as if it were a stage, and `la-vul` names both
an attested register and a comparative-method reconstruction. This registry
gives each such distinction a stable, human-readable identifier, without
replacing the standard codes — they remain the anchors. The full argument,
with a review of every prior system, is in
[docs/prior-art.md](docs/prior-art.md).

Born from the holdings of the [Nabu](https://github.com/arvicco/nabu)
research library, but universal by construction: nothing here depends on any
particular collection, and every mapping states something true for any
consumer of the code.

## The identifier

```
lect-id = anchor [ ":" stage ] [ "/" variety ] [ "~" script ] [ "@" ortho ]
```

| Example | Meaning |
|---|---|
| `lat` | Latin, the whole span — honest coarseness |
| `lat:med` | Medieval Latin |
| `lat:late/ecc` | Late Latin, ecclesiastical register |
| `grc:koi` | Koine Greek |
| `zho/lit` | Literary Chinese (wenyan) — a register, not a stage |
| `roa:pro` | Proto-Romance — `mode: reconstructed` in the registry |
| `jpn:mod@kyu` | Modern Japanese in pre-reform (kyūjitai) orthography |
| `san~latn` | Sanskrit held as a romanized edition |
| `sga~ogam` | Old Irish as the reader meets it in ogham |

- **anchor** — an ISO 639 or established Wiktionary code: the most specific
  genealogical node (language or family) the lect hangs from. Every
  identifier stays legible to anyone who knows the standard codes.
- **stage** — a broad historical development stage from that anchor's
  registered set. Reconstruction is the stage `pro`, but machine behavior
  keys on the registry field `mode: reconstructed`, never on the tag
  spelling.
- **variety** — register, sociolect, or recension (`/lit`, `/vul`, `/ecc`).
- **script** — the writing system of the text AS HELD (`~latn`, `~ogam`):
  the surface a reader of the document meets, drawn from the global
  `scripts:` table (ISO 15924 codes, lowercased). Never the artifact's
  original writing system — a consumer records that separately when it
  differs (a Latin-transliterated cuneiform tablet is `~latn`; the
  tablet's Xsux belongs in the consumer's own artifact field).
- **ortho** — an orthography reform *within* a script (`@kyu`, `@bohoric`),
  reusing IANA variant names where they exist; rows may carry a `script:`
  scope naming the script the reform lives in.

**Why a script axis?** An earlier revision of this registry argued script
should stay in BCP 47 (`sr-Cyrl`, `san-Latn`) and out of the lect id — one
fact, one home. Measurement overturned that: in real catalogs the BCP 47
suffix convention carries **two different claims with no way to say
which** — `san-Latn` usually means the held edition is romanized (a surface
fact), while `egy-Egyd` usually means the papyrus was written in demotic
(an artifact fact, riding text that is itself Latin transliteration). A
registry that wants one nomenclature for *which lect, presented how* has
to say this precisely, so the `~` axis is defined to claim exactly one of
them: **the script of the text as held** — machine-checkable against the
bytes. The artifact's differing original script is real and worth keeping,
but it is the consumer's separate field, never folded into the lect id. A
romanized Veda is `san:ved~latn` and still the same lect; where a script
choice is constitutive of a community (Ladino in Hebrew script), it
belongs in the variety slot instead.

## The genealogy model

Two relations, kept strictly apart:

- **Stage succession** — one lineage through time (`lat:arch → cla → late →
  med`) — is carried by each stage's `ord` field, never by parent links.
- **Descent** — one lineage continuing from another — is carried by `parent:`
  edges: `en ← enm ← ang ← gmw:pro ← gem ← ine`. Where ISO coded historical
  stages as separate languages, those anchors simply chain.

A family anchor is read as its **root lineage** (the clade viewed from its
common ancestor), so one edge kind serves throughout: `roa: {parent: lat}`
states plainly that the Romance clade's common ancestor is a continuation of
the Latin lineage — no pseudo-family nodes needed. Edges default to bare
anchors (honest coarseness); nuance lives in `note:` fields. The tree is
single-parent by design: contact and disputed subgroupings get prose and the
Glottolog crosswalk, not edges.

## The files

- **[lects.yml](lects.yml)** — the registry: anchors with their stages
  (name, date band with a `band_note` naming the convention, `ord`, `mode`),
  varieties, orthographies, parent edges, and Glottocode crosswalks.
- **[codemap.yml](codemap.yml)** — universal code → lect defaults.
  *Identity is the default rule*: any code not listed maps to itself as a
  bare anchor, so every line in the file is a decision. Consumers layer
  their own per-collection and per-document overrides above these defaults.
- **[docs/schema.md](docs/schema.md)** — field-by-field semantics.
- **[docs/prior-art.md](docs/prior-art.md)** — why this registry exists:
  the problem, the prior art, and why none of it suffices.

## Quickstart

Both data files are plain YAML, consumable with any parser:

```ruby
require "yaml"
lects   = YAML.safe_load(File.read("lects.yml"))
codemap = YAML.safe_load(File.read("codemap.yml"))

codemap["map"].fetch("gkm", "gkm")             # => "grc:byz"
lects["anchors"]["grc"]["stages"]["byz"]        # => name, band, ord, crosswalks
```

Validate after any edit:

```
bin/validate
```

Plain Ruby, standard library only; checks the identifier grammar,
referential integrity (every mapping target and parent edge resolves),
`ord` uniqueness, band sanity, Glottocode shape, and parent-graph
acyclicity. CI runs the same script on every push.

## Stability

**Pre-1.0 instability window: identifiers may be renamed or restructured
without notice until the first tagged release.** After v1.0.0, semantic
versioning applies to the identifier space itself: renaming or removing a
lect id, or changing a `mode`, is a major version; new anchors, stages,
varieties, or orthographies are minor; band edits, notes, and crosswalks are
patches. Changes are logged in [CHANGELOG.md](CHANGELOG.md).

## License

[CC BY 4.0](LICENSE) — use freely with attribution.

## Sister projects

Part of a small family: [nabu](https://github.com/arvicco/nabu), a personal
research library for ancient-text corpora;
[nabu-data](https://github.com/arvicco/nabu-data), the datasets it publishes;
and [nabu-edubba](https://arvicco.github.io/nabu-edubba), the scribal school
built on top. This registry is the frame the library describes its holdings
with.
