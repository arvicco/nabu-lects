# Changelog

## Unreleased

Additions since the initial registry (counts now 41 anchors, 59
stages, 8 varieties, 2 orthographies; `codemap.yml` 20 mappings):

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
