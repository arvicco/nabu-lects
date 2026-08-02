---
title: "Schema — lects.yml and codemap.yml, field by field"
---

# Schema — lects.yml and codemap.yml, field by field

## The identifier grammar

```
lect-id = anchor [ ":" stage ] [ "/" variety ] [ "@" ortho ]
```

Axes are **ordered** (`:` before `/` before `@`) and all-lowercase.

- `anchor` — 2–3 lowercase letters, optionally hyphen-extended
  (`roa-opt`, `ine-bsl`): an ISO 639-1/2/3/5 or established Wiktionary
  code naming the most specific genealogical node the lect hangs from.
  A bare anchor is a legal lect and means the anchor's whole span.
- `stage` — 2–5 lowercase letters from the anchor's registered stage set.
- `variety` — 2–5 lowercase letters from the anchor's registered
  variety set.
- `ortho` — 2–8 lowercase alphanumerics (starting with a letter) from
  the anchor's registered orthography set.

Identifiers sort by anchor lexicographically; **chronological order
within an anchor comes from the registry's `ord` fields, never from tag
spelling**.

## lects.yml

Top level: one `anchors:` mapping, keyed by anchor code.

### Anchor fields

| Field | Meaning |
|---|---|
| `name` | Display name. |
| `kind` | `family` on ISO 639-5 / Wiktionary family codes; absent on languages. A family anchor is read genealogically as its **root lineage** — the clade viewed from its common ancestor (which is what its `pro` stage reconstructs). |
| `glottocode` | Crosswalk to Glottolog (`[a-z]{4}[0-9]{4}`), **not** an identity: the world tree beyond this registry is reachable through it. Stated only where verified; never guessed. |
| `band` | `[start, end]` in years; negative = BCE; `null` = open. A per-anchor recorded decision, always paired with `band_note`. Bands document and aid per-document assignment; they are never derivation inputs. |
| `band_note` | Names the convention the band follows ("ISO 639-2/MARC reference name", "approximate Egyptological convention", …). Required wherever `band` is stated. |
| `parent` | A descent edge (see below). |
| `note` | Free prose: cross-references, caveats, contact-language and subgrouping commentary that deliberately does not get edges. |
| `stages` / `varieties` / `orthos` | The registered tag sets, below. |

### Stage fields

| Field | Meaning |
|---|---|
| `name` | Display name. |
| `ord` | Integer, **unique within the anchor**: chronological display order. |
| `mode` | `attested` (default, omitted) or `reconstructed`. The one machine-load-bearing field: consumers' reconstruction predicates read it — never the tag spelling, never a code suffix. |
| `band`, `band_note` | As on anchors; stage bands may overlap where a tradition's grid is dialect × period rather than a single ladder (e.g. Neo-Assyrian beside Neo-Babylonian). |
| `wikt` / `iso` | Provenance crosswalks to the code that motivated the entry (`wikt: la-med`, `iso: och`). |
| `note` | Free prose. |

### Variety fields

`name`, `kind` (one of `register`, `sociolect`, `recension`, `dialect`),
optional `wikt`/`iso` crosswalks and `note`. Varieties carry the axis the
standards conflate with stage: Literary Chinese is `kind: register`; the
Church Slavonic recensions are `kind: recension`. Where a script choice is
constitutive of a community (aljamiado traditions), it is modeled as a
variety, not an orthography.

### Orthography fields

`name` and optional `note`. Orthography tags name spelling reforms
**within one script** (kyūjitai, the Bohorič alphabet) and reuse IANA
variant names where they exist (`bohoric`, `petr1708`). Each tag is
implicitly scoped to its script — stated in its note. Script itself is
never part of a lect id: it lives in BCP 47 script subtags on the
consumer's side, and a document's full identity is the composition of its
coded tag and its lect.

### The parent edge

`parent:` holds a lect id (bare anchor or staged lect) and means: **this
lineage continues from that one.** One edge kind covers every node pairing,
because a family anchor is identified with its root lineage —
`roa: {parent: lat}` (family→language), `gmw: {parent: gem}`
(family→family, i.e. subgrouping as descent of the root),
`lat: {parent: itc:pro}` (language→reconstructed lect).

- **Not stage succession.** Stages of one anchor are ordered by `ord`;
  they are never each other's parents. Where standards coded stages as
  separate languages (`ang`/`enm`/`en`), those *anchors* chain by parent.
- **Most-specific rule**: point to the most specific ancestor on record —
  attested lect over reconstructed proto over bare family anchor.
- **Precision policy**: default to the bare anchor; refine to a staged
  lect only where scholarship is settled; nuance goes in `note:`.
- **Walk rule**: a staged lect inherits its anchor's parent unless it
  declares its own — so a walk up from `roa` runs `lat → itc:pro →` (via
  `itc`) `→ ine` without every stage needing an edge.
- **Single-parent tree**: contact, creolization, and disputed
  subgroupings get `note:` prose and the Glottolog crosswalk, not edges.

## codemap.yml

Top level: one `map:` mapping from standard codes (ISO 639, Wiktionary —
including etymology-only and `-pro` codes) to lect ids.

**Identity is the default rule.** Any code not listed maps to itself as a
bare anchor; the file lists only non-identity mappings, so every line is a
decision. Bare-anchor targets need no registry entry; any target carrying
a stage, variety, or orthography must resolve against `lects.yml`.

**Precedence for consumers**, highest first:

1. per-document assignment (a consumer's own overlay),
2. per-collection overrides (a consumer's knowledge about its holdings —
   e.g. that one dictionary's use of a code means the reconstruction),
3. this file's universal defaults,
4. identity.

Entries here state only what is true of the *code itself*, for any
consumer. Knowledge about particular collections never enters this file.

## Validation

`bin/validate` (standard-library Ruby) enforces: YAML well-formedness;
the identifier grammar everywhere; referential integrity (codemap targets
and parent edges resolve; stage/variety/ortho tags are defined on their
anchors); `ord` uniqueness per anchor; band sanity (`start ≤ end`);
Glottocode shape; parent-graph acyclicity. CI runs it on every push and
pull request.
