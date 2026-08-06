---
title: nabu-lects
---

# nabu-lects

A small, curated registry of **lects** — language varieties identified by
genealogical anchor × historical stage × variety × orthography — with a
universal mapping from the standard language codes (ISO 639, Wiktionary)
onto them.

[![xkcd 927: Standards — "Situation: there are 14 competing standards. 'We need one universal standard that covers everyone's use cases.' Soon: there are 15 competing standards."](https://imgs.xkcd.com/comics/standards.png)](https://xkcd.com/927/)

<sup>[xkcd #927, "Standards"](https://xkcd.com/927/) by Randall Munroe,
[CC BY-NC 2.5](https://xkcd.com/license.html).</sup>

Yes — we know. So this registry is deliberately **not the fifteenth
standard**: it mints no new language codes. Every identifier is *anchored in
a code you already use*, and the registry's whole job is to write down how
the fourteen existing standards line up — and precisely where each one
stops.

## The problem, in four codes

- `lat` covers Plautus, Cicero, the Vulgate, and twelfth-century monastic
  charters alike — there is no ISO code for Old, Late, Medieval, or
  Neo-Latin.
- `grc` ("Ancient Greek, to 1453") spans Homer to the fall of
  Constantinople — a cataloguing convention, not a linguistic boundary.
- `lzh` codes Literary Chinese, a *written register* used across two
  millennia, as if it were a historical stage.
- `la-vul` names both *attested* Vulgar Latin (the Appendix Probi) and the
  *reconstructed* Proto-Romance of the comparative method — evidence and
  inference fused in one code.

The full argument — with a review of every prior system, from ISO 639-6's
rise and withdrawal to Glottolog, BCP 47, and Wiktionary — is in
**[Prior art and the case for lects](prior-art.md)**.

## The answer, in one line

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

Anchors are ISO 639 / Wiktionary codes, so every identifier stays legible
to anyone who knows the standard codes. Stages carry date bands with their
provenance recorded; genealogy is explicit `parent:` edges (`roa: {parent:
lat}` — no pseudo-family nodes); reconstruction is a data field, never a
naming convention; the `~` axis claims the script of the text **as held**
(ISO 15924, lowercased, from a global table), never the artifact's
original writing system. Field-by-field semantics: **[the schema](schema.md)**.

## Integrating the registry in your tool

The registry is two plain YAML files, consumable with any parser:

```
https://raw.githubusercontent.com/arvicco/nabu-lects/main/lects.yml
https://raw.githubusercontent.com/arvicco/nabu-lects/main/codemap.yml
```

**The identity default.** `codemap.yml` lists only *non-identity* mappings.
Any code not listed maps to itself as a bare anchor — so your tool needs no
registry entry for a code to keep working, and adopting the registry cannot
break codes it doesn't mention.

**Precedence.** Layer your own knowledge above the universal defaults:

```
per-document override  >  per-collection override  >  codemap.yml  >  identity
```

The registry states what is true of a *code* for anyone; what is true of
*your holdings* (this corpus's `lat` is `lat:med`; that dictionary's
`la-vul` is `roa:pro`) belongs in your own override layer, keyed however
your tool keys collections.

**The one machine-load-bearing field.** A stage with `mode: reconstructed`
marks a comparative-method reconstruction. Key asterisk display,
etymological-closure rules, or evidence filters on that field — never on
the spelling of a tag or the suffix of a code.

**Validating a vendored copy.** If you vendor the files, run the bundled
validator (plain Ruby, standard library only) against them:

```
bin/validate
```

It checks the identifier grammar, referential integrity (every mapping
target and parent edge resolves), `ord` uniqueness, band sanity, Glottocode
shape, and parent-graph acyclicity — the same script CI runs here.

> **Stability**: pre-1.0 instability window — identifiers may be renamed or
> restructured without notice until the first tagged release. After v1.0.0,
> semantic versioning applies to the identifier space itself; see the
> [README](https://github.com/arvicco/nabu-lects#stability).

**Attribution.** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/):
use freely, credit "nabu-lects" with a link to this repository.

## The family

This registry was born from the holdings of
**[Nabu](https://github.com/arvicco/nabu)** — a personal research library
of ancient-text corpora, roughly a million documents across more than 120
language codes — and is the frame that library describes its holdings
with. Sister projects:
[nabu-data](https://github.com/arvicco/nabu-data), the datasets the
library publishes, and the
[School](https://arvicco.github.io/nabu-edubba), the scribal-school
reading environment built on top.

Contributions and corrections: issues and pull requests on
[github.com/arvicco/nabu-lects](https://github.com/arvicco/nabu-lects) —
every change passes `bin/validate`, and band or genealogy corrections are
welcome with a source note.
