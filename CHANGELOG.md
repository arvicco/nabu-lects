# Changelog

## Unreleased

Initial registry:

- `lects.yml` — 38 anchors, 50 stages, 8 varieties, 2 orthographies:
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
