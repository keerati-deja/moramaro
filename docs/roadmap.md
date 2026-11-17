# Scope and roadmap

[Documentation home](../README.md) · [Source audit](implementation-audit.md) · [Proposed architecture](architecture.md)

These are staged candidates and exit criteria, not release dates or promises. MoraMaro currently contains documentation only.

## Existing PLP functionality

The inspected development snapshots contain kana-based mora-like grouping, supplied-accent validation, Tokyo-style symbolic projection, annotation helpers, six display modes, and a PLP-specific Japanese editor with manually maintained readings, accent profiles, and forms. The source and pure-function tests are documented in the [audit](implementation-audit.md).

The lexical graph supports separate written forms, readings, senses, accents, grammatical analyses, morphological components, and explicit associations. These are storage/editor capabilities. No automatic conjugation, form-reading determination, accent lookup, accent prediction, phrase contour generation, speech synthesis, or regional phonological model was established by this inspection.

## Candidate initial MoraMaro release

| Milestone | Work to consider next | Exit criterion |
| --- | --- | --- |
| 1. Owner decisions | Confirm independent repository, PLP extraction rights, code/documentation licensing, supported runtime(s), and initial scope | Recorded decisions; no assumed third-party dataset rights |
| 2. Input and representation contract | Specify normalization, valid reading input, special morae, numeric range, empty input, unknown/invalid states, dialect labeling, and source spans | Reviewable design and compatibility decisions for identified PLP edge cases |
| 3. Minimal extraction | Extract only agreed pure segmentation, validation, symbolic projection, and rendering/serialization responsibilities | Independent dependency without PLP schema, authentication, services, configuration, or new linguistic prediction claims |
| 4. Verification and integration | Preserve relevant pure-function checks, add evidence-based edge cases, implement a PLP adapter in a separately authorized PLP task | Documented parity and deliberate differences; PLP association/review ownership retained |
| 5. Initial release preparation | Select packaging and versioning, document real installation/API only after they exist, review provenance | Reproducible package checks and owner-approved release; publication remains a separate action |

No production code was extracted, runtime dependencies introduced, or package published in this documentation task.

## Future research and development

| Area | Open work | Required evidence |
| --- | --- | --- |
| Reading representation | Orthography/reading/pronunciation distinctions; halfwidth and combining input; long vowels and contractions | Explicit policies and a reviewed multilingual/Unicode edge-case corpus |
| Morphology/conjugation | Godan/ichidan/irregular forms; grammatical ambiguity; voice, polarity, politeness, and auxiliaries | Analysis-specific tests and documented exceptions, independently of accent tests |
| Conjugation-aware accent resolution | Form-specific observations, supported rules, exception handling, provenance and conflicts | Licensed evidence; expert-reviewed examples; task/variety-specific evaluation |
| Compound and suffix behavior | Structure, lexicalization, accentual domains, suffix effects, and alternate patterns | Structural analyses and construction-specific sources; no universal concatenation rule |
| Phrase-level modeling | Accentual phrases, boundaries, downstep, focus, particles and auxiliaries | Contextual speech evidence and a model beyond independent word H/L strings |
| Dialect support | Variety-specific pattern models and compatible renderers | Named varieties, appropriate representations, qualified review, and rights-cleared observations |
| Acoustic or synthesis integration | Optional F0 alignment or external speech tools | Explicit distinction between lexical models, measured data, and synthesized output |

These capabilities are unimplemented here and, in several cases, research-dependent. Broader coverage and accuracy must be demonstrated against specified data; they cannot be inferred from a schematic table or a passing SVG test.
