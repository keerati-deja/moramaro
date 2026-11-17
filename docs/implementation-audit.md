# Read-only audit of the PLP implementation

[Documentation home](../README.md) · [Architecture](architecture.md) · [Roadmap](roadmap.md)

Inspection date: **2026-11-17**. This describes source snapshots, not a deployment inventory or an assertion that these changes have merged to PLP's `main`.

## Source identity

The audit inspected local PLP development snapshots. MoraMaro does not include or redistribute PLP source code. Source paths below identify the files inspected; they are not links to the upstream repository.

The six requested pitch files were byte-identical in two inspected development snapshots. A third lexical-data snapshot matched five; its Japanese editor differed. The editor and model conclusions use the snapshots that contained those files. The locally available PLP baseline was older and lacked several V4 files, so this audit is not a claim about every PLP branch or a deployed service.

## Capabilities and test evidence

| Source | Confirmed behavior | Evidence and limits |
| --- | --- | --- |
| `pipeline/japanese_pitch.py` | `segment_morae` trims outer whitespace; attaches listed small kana and Unicode category `M` marks to an existing unit; keeps っ/ッ, ん/ン, and ー separate | An orthographic grouping heuristic. No NFC/NFKC operation, kana-only validation, phonemic reading conversion, or morphological analysis |
| `pipeline/japanese_pitch.py` | `validate_accent_number` accepts exact Python integers from 0 through `min(count, 500)`; optional stored count must match and be positive | A validator for supplied records, not a dictionary lookup. Rejects booleans. Empty reading with 0 and no stored count passes this validator, although projection returns no contour |
| `pipeline/japanese_pitch.py` | `pitch_contour` projects supplied 0…N values into `morae`, `levels`, and `drop_after_last`; invalid input returns `None` | Symbolic Tokyo convention. Its range check does not share the validator's 500 ceiling. It does not check dialect or whether an accent is linguistically possible on a special mora |
| `pipeline/japanese_pitch.py` | Annotation helpers add contours to copies of supplied reading/accent records | Preserve original fields and alternatives; no accent discovery, ranking inference, or mutation of input records |
| `web/japanese-pitch-display.js` | Matching grouping and projection; blank accent input remains `null`; validates preferences and supplied server-contour agreement | Tests compare Python and JavaScript. Integer/string parsing and validation are distinct functions, not one universal contract |
| `web/japanese-pitch-display.js` | Six modes: Mora Graph, Pitch Curve, Overline, Downstep Mark, H/L Pattern, Accent Number | Shared symbolic contour and SVG geometry; escaped output and accessible descriptions; curve is not F0 or audio |
| `web/japanese-pitch-display.js` | Contextual particle display requires explicit context and kana particle text | A simplified continuation, displayed as one appended unit even for multi-kana text. It is not general particle segmentation or phrase accent resolution |
| `web/lexical-japanese.js` | Reading/profile selection, inline accent editing, alternate profile handling, local display preferences, and shared graph/save integration | Coupled to PLP DOM, graph IDs, row menus, Notes, deletion confirmations, and browser storage. Following Particle is disabled in this editor because structured example context is absent |
| `web/lexical-japanese.js` | Existing forms marked `metadata.form_kind=inflection` support a manually managed conjugation view | No automatic conjugation, reading generation, accent lookup, or form-specific pitch prediction |

`tests/test_japanese_pitch.py` asserts representative kana combinations and special morae, invalid inputs, annotation preservation, combining marks, and Python/JavaScript parity. The tests deliberately project arbitrary accent numbers on the same reading; those fixtures are algorithm tests, **not verified lexical accents**. Dialect-preservation tests even project a Kansai-labeled record using the Tokyo formula; metadata retention does not establish Kansai phonological support.

`tests/js/japanese-pitch-display.test.cjs` covers lengths 1–10 and all indices 0…N, an explicit four-mora table, invalid/unknown/inconsistent inputs, all six display modes, geometry, preferences, escaping, non-mutation, contextual particles, and accent input parsing. These tests establish implementation behavior on tested inputs, not universal segmentation correctness or accent accuracy.

`docs/japanese-pitch-v4.md` is a historical implementation/validation report. It reports 82 pure JavaScript tests and additional database/browser acceptance work. The current documentation task reran the pure JavaScript suite and the seven Python test functions in an isolated temporary copy; see the [delivery report](documentation-report.md). Historical database/browser results were not rerun or independently re-established.

## Lexical and morphological integration requirements

The following models were inspected as source, without opening a database or applying migrations:

| PLP model | Meaning and implication for a future adapter |
| --- | --- |
| `047_korean_japanese_vocabulary.sql` | Written forms and readings have separate stable identities; multiple accent records belong to a reading. Persisted `accent_number` is non-null; unknown is represented by absence of an accent row |
| `051_japanese_pitch_preference_rank.sql` | `preference_rank` is ordered within a reading/dialect; it is not an accent location, confidence score, or linguistic truth ranking |
| `074_lexical_data_v2.sql` | Readings can have notation, dialect, and metadata; alternate notations describe a reading. Explicit `lexical_realizations` associate forms/readings/senses/POS/accent. Missing references do not assert every combination |
| `079_forms_morphology.sql` | `form_analyses` attach labels/features to a form. `morph_analyses` and ordered `morph_components` represent analyses using reusable morphemes or entries, with source/evidence/review fields. Storage does not perform morphological analysis |
| `084_form_analysis_readings.sql` | `form_analysis_readings` ties a particular grammatical analysis to a reading and optionally sense, accent, dialect, and context; identical surfaces need not imply identical analyses |
| `pipeline/lexical_graph.py` and `pipeline/lexical_adapter.py` | Transactional graph/adapter code preserves IDs, explicit associations, ownership and validation; the Japanese save boundary validates supplied accent values |

UI drafts can temporarily contain null accent values. That is not evidence that the persisted accent table accepts null: the editor's save behavior and the non-null schema must be understood together.

An independent engine should receive selected linguistic values and opaque caller references. The PLP adapter must map results back to the exact analysis/reading/profile, retain alternatives, and leave saves, revisions, deletion cascades, review status, and permissions to PLP. Exporting every reading against every form would manufacture assertions absent from the model.

## Extraction risks to resolve before a package release

1. Specify normalization and allowed input independently from the existing grouping heuristic, including halfwidth kana, isolated small kana, punctuation, iteration marks, and malformed combining sequences.
2. Decide whether the validation/projection range and empty-input differences are intentional. Document or reconcile them before promising a public contract.
3. Preserve unknown values; keep server-contour mismatch diagnostics distinct from absence of lexical knowledge.
4. Keep non-Tokyo metadata without presenting Tokyo projections as dialect-specific analysis.
5. Separate pure functions/rendering from PLP editor state, schemas, authentication, and infrastructure. Confirm extraction rights before copying production code into the independent repository.
