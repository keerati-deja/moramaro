# Documentation foundation delivery report

Date: **2026-11-17**. Scope: documentation only, prepared in the separate MoraMaro workspace. No PLP files, database, branches, deployment, or configuration were changed. No engine features, package, runtime dependencies, remote repository, deployment, or license grant were introduced.

## 1. Created files

| File | Purpose |
| --- | --- |
| [README.md](../README.md) | Public project introduction, name, PLP origin, audience, current status, navigation, and licensing status |
| [project-background.md](project-background.md) | Project identity, intended users, independence, and ownership boundaries |
| [architecture.md](architecture.md) | Six proposed responsibilities, optional manual-input path, candidate/provenance model, resolution priority, and PLP adapter boundary |
| [roadmap.md](roadmap.md) | Existing PLP functionality, extraction candidates, research areas, and staged exit criteria |
| [linguistics/mora.md](linguistics/mora.md) | Mora/syllable distinction, rhythm, ordinary/special morae, checked counts, orthography/phonology, and Unicode policies |
| [linguistics/pitch-accent.md](linguistics/pitch-accent.md) | Tokyo H/L and nucleus conventions, four pattern types, sourced noun examples, particles, phrases, downstep, intonation, F0, and dialect limits |
| [linguistics/conjugation-and-accent.md](linguistics/conjugation-and-accent.md) | Extended treatment of verb classes and forms, auxiliaries, i-/na-adjectives, structure, suffixes, verified comparisons, variation, and prediction limits |
| [linguistics/accent-variation.md](linguistics/accent-variation.md) | Multiple readings/patterns, lexical/contextual ambiguity, variety-specific models, conflicts, and independent review/provenance dimensions |
| [references-and-credits.md](references-and-credits.md) | Bibliography, example locators, consultation limits, attribution, data rights, and license recommendation |
| [implementation-audit.md](implementation-audit.md) | Inspected PLP source/test behavior, model requirements, coupling, and extraction edge cases |
| [documentation-report.md](documentation-report.md) | This report |

The requested layout is retained, with two additional evidence/report documents. All project files created by this task are Markdown.

## 2. Linguistic chapter findings

The mora chapter separates phonological weight from syllables and Unicode characters. Its examples show yōon, sokuon, hatsuon, and vowel length, with explicit counts and limits on kana-based heuristics.

The pitch chapter separates lexical accent, symbolic H/L, phrase intonation, and acoustic F0. It uses sourced 兜・心・男・魚 examples, explains `[0]` versus unknown, distinguishes local accentual fall from phrase-register downstep, and limits the model to its stated Tokyo convention.

The conjugation chapter is the largest chapter. It covers dictionary, polite, past, te, negative, volitional, conditional, potential, passive, causative, and imperative forms; contrasts godan, ichidan, and irregular paradigms; and covers i-adjective and copular/na-adjective constructions. Source-checked indices are distinguished from explicitly unverified complete-expression accents. OJAD's multiple 高い patterns are retained. Morphology, reading, accent resolution, and rendering remain separate responsibilities.

The variation chapter requires entry/reading/form/variety/context identity, alternatives, and source disagreements. Review state and prediction method are independent; a reviewed prediction does not become an observed pronunciation.

## 3. Existing PLP capabilities identified

The inspected development code contains kana-based mora-like grouping, supplied-accent validation, symbolic Tokyo projection, non-mutating annotation helpers, and six display modes. PLP owns an editor for manually supplied readings, accent profiles, and grammatical forms, plus explicit lexical and morphological association models. Dialect labels are retained, but projection is Tokyo-style.

The audit covers thirteen PLP source/model files from local development snapshots. Working files were compared against their committed contents, and the six requested pitch files were checked against a second integration snapshot. These findings describe inspected development code, not every PLP branch or a deployed service.

## 4. Unimplemented or research-dependent capabilities

No independent MoraMaro runtime exists yet. Automatic conjugation, form-reading determination, accent lookup/prediction, lexical exception resolution, compound analysis, phrase-aware contours, dialect-specific phonology, and speech/F0 processing are unimplemented here. Later work must separately establish linguistic evidence, input policies, data permissions, and evaluation methods. No accuracy, coverage, or performance guarantees are claimed.

## 5. References, verification, and unresolved questions

The [bibliography and provenance register](references-and-credits.md) includes all four requested resources, plus Kawahara, Oshima, Hasegawa, Kobayashi, Warner/Arai, Youngberg, Venditti, downstep scholarship, and Unicode references. It identifies when only metadata or an abstract was consulted.

Checks completed:

- Relative document paths and the explicit bibliography anchor were checked programmatically across all eleven Markdown files; no missing targets remain.
- Kana segmentation examples were checked for count consistency, and displayed symbolic H/L examples were checked against their stated indices.
- OJAD numeric examples were checked from rendered marked-mora records, with alternative patterns visible and exact row/category locators recorded. Plain-text extraction alone was not treated as accent evidence.
- The existing JavaScript suite passed **83 tests, 0 failures, 0 skips**, using Node v24.21.0 in an isolated temporary copy. The historical V4 report says 82; it is attributed as historical, not substituted for this result.
- All **7 existing Python test functions passed** by direct invocation in that isolated copy, including Python/JavaScript parity and the JavaScript-suite subprocess. This was **not a pytest run**: pytest is absent, and a minimal import shim provided only the unused skip entry point; no functions were skipped. No dependency was installed.
- No tests were added to the project. Database/browser acceptance and full PLP regression suites were not rerun. Temporary test copies were removed after the run.
- Source files were checked against local committed objects. PLP's Git status remained clean after inspection/checks. Documentation whitespace and Markdown fence checks passed.

External-link limitations:

- Primary articles, publisher/author pages, OJAD pages, and Unicode references were opened where available. Four DOI resolver URLs could not be opened by the web tool; corresponding bibliographic metadata and alternate publisher/abstract pages were verified. Resolver failure is not reported as proof the DOI is broken.
- OJAD's 買う and 静か individual short-query links did not resolve through the web extractor. Their exact rows were successfully inspected in the rendered multiword search. Their short query links remain locators to recheck if routing changes.
- The Schökler conference program confirms author/title/session, but the supplied one-page PDF yielded no readable text and its screenshot fetch failed. No substantive rule/example depends on it.
- PLP implementation source remains outside this documentation repository. Source paths are given as identifiers; no PLP code was copied here.

Open decisions are independent linguistic review, complete accent verification for the expressly unverified constructions, licensed data-source selection, input-contract edge cases, extraction rights, and owner licensing decisions. MIT is a recommendation only; no LICENSE file was created.

## 6. Recommended next milestones

1. Confirm repository access, ownership/extraction rights, license, supported runtimes, and minimal release scope.
2. Specify normalization, accepted readings, unknown/invalid states, numeric limits, empty input, and dialect labeling; resolve the documented PLP contract differences.
3. Authorize a minimal pure-core extraction and compatibility work as a separate implementation task.
4. Design the PLP adapter around exact analysis/reading/accent associations and human review ownership.
5. Develop a rights-cleared, linguistically reviewed evidence set before attempting conjugation-aware accent prediction or claiming measured accuracy.

## 7. Repository boundary

This project begins with documentation only. It contains no PLP implementation code, package, runtime dependencies, or license grant. PLP remains the origin of the inspected implementation and an intended consumer of a future independent engine. Confirm code ownership and contributor permissions before any extraction.
