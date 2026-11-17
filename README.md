# MoraMaro (モラマロ)

MoraMaro is an independent Japanese linguistic engine project for mora segmentation and pitch-accent representation. It originates in **Polyglot Learning Pipeline (PLP)**, where the initial segmentation and pitch-display code supports Japanese vocabulary and pronunciation work. PLP remains its original supporting product and an intended consumer.

The project is intended for application developers, Japanese learners and teachers, and researchers who need explicit readings, accent alternatives, and traceable linguistic evidence. Its long-term scope includes morphology-aware accent resolution, while keeping grammatical form generation, reading determination, accent resolution, and visualization separate.

**Current status: documentation foundation, before engine extraction.** This repository contains no independent runtime package, installation command, or supported usage API. Existing functionality described here belongs to the inspected PLP source snapshots; it has not yet been released as MoraMaro. See the [implementation audit](docs/implementation-audit.md) for exact evidence and limitations.

## The name

“MoraMaro” playfully reverses “Mora,” inspired by Thai wordplay. モラマロ is branding; it makes no claim to a special Japanese historical or linguistic meaning.

## Scope

| Status | Capability |
| --- | --- |
| Existing in inspected PLP code | Kana-based mora-like segmentation; validation of supplied accent numbers; symbolic Tokyo-style H/L projection; six pitch-display modes; manually edited readings, accent alternatives, and grammatical-form associations |
| Candidate initial MoraMaro release | Extract and stabilize the pure segmentation, validation, projection, and rendering responsibilities, with documented input limits and compatibility tests |
| Future research and development | Reading representation, morphology/conjugation integration, evidence-aware accent resolution, lexical exceptions, compound analysis, phrase-aware and dialect-specific modeling |

An unknown accent is **unknown**, never automatically `[0]`. `[0]` positively specifies an unaccented Tokyo-style pattern. A pitch diagram is a symbolic representation, not measured fundamental frequency (F0), speech synthesis, or an accent prediction.

## Documentation

- [Project background](docs/project-background.md): origin, identity, audience, and independence from PLP.
- [Mora — 拍 / モーラ](docs/linguistics/mora.md): phonological units, kana, special morae, examples, and Unicode limits.
- [Pitch accent — 高低アクセント](docs/linguistics/pitch-accent.md): Tokyo conventions, particles, phrases, and acoustic interpretation.
- [Conjugation, morphology, and accent](docs/linguistics/conjugation-and-accent.md): verb classes, auxiliaries, adjective paradigms, verified examples, and prediction limits.
- [Accent variation and ambiguity](docs/linguistics/accent-variation.md): dialects, alternative analyses, context, and uncertainty.
- [Proposed architecture](docs/architecture.md): responsibilities, conceptual records, and the PLP boundary.
- [Roadmap](docs/roadmap.md): existing PLP functionality, extraction candidates, and research milestones.
- [References and credits](docs/references-and-credits.md): bibliography, example provenance, and licensing decisions.
- [Documentation report](docs/documentation-report.md): delivered files, checks, unresolved questions, and next steps.

## Credits and licensing status

PLP is the origin of the initial implementation. The linguistic documentation acknowledges scholarship and educational resources including OJAD, Kubozono, Minematsu and colleagues, Schökler, and the additional sources listed in [references and credits](docs/references-and-credits.md). Citation does not imply institutional endorsement, contribution, or permission to redistribute a resource.

MoraMaro is intended to become an open-source project. **A license has not been selected or applied.** MIT is recommended for owner consideration, subject to the rights in any extracted PLP code. Dictionary databases, audio, third-party diagrams, and other components require their own provenance and permission checks; a future code license would not automatically cover them.
