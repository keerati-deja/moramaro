# Proposed architecture

[Documentation home](../README.md) · [Source audit](implementation-audit.md)

**Design proposal, not an implemented MoraMaro API.** Record names below express responsibilities, not committed class names, field spellings, transport formats, or package boundaries.

## Processing paths

```text
Lexical Entry → Grammatical Form → Reading → Accent Resolution → H/L Contour → Visualization
                                      ↑            ↑
                           supplied reading    supplied pattern
```

The full path permits optional morphology and reading providers. A caller may instead supply a reading and an accent pattern directly, validate them, and render a diagram. Neither lexical lookup nor conjugation generation should be required for this path. A supplied reading with unknown accent may still be segmented and displayed as text; the contour remains unavailable.

Each arrow may produce zero, one, or several candidates. An ambiguous analysis is not resolved merely because one downstream renderer expects one contour. A caller should select an explicit candidate or display the alternatives.

## Six responsibilities

| Responsibility | Inputs and outputs | Boundary |
| --- | --- | --- |
| Mora segmentation | Reading representation and segmentation policy → units, source spans, diagnostics | Kana grouping must not masquerade as a complete phonological analysis. Retain original and normalized text separately |
| Reading representation | Orthography plus a supplied or externally resolved reading → kana/phonological representation, alternatives, notation mappings | Kanji spelling, reading, romanization, and pronunciation are different layers |
| Morphological analysis / conjugation | Lexeme/class/features or externally supplied analysis → grammatical form candidates and structure | Generating a grammatical surface does not establish its reading or accent |
| Pitch accent resolution | Selected lexeme/form/reading/variety/context plus evidence providers → accent candidates or unknown | Record derivation and uncertainty. Do not infer `[0]` from a failed search |
| Accent pattern representation | Variety-specific pattern and alignment → validated abstract accent structure; optionally symbolic levels | Tokyo accent numbers are one representation, not a universal Japanese dialect schema |
| Visualization and serialization | Validated selected pattern plus presentation options → diagram/text/data | Rendering must not silently invent linguistic content; serialization preserves alternatives and evidence |

The first release may expose only the manually supplied reading/pattern path. The source audit identifies candidate pure functionality; it does not require an initial release to contain all six modules.

## Conceptual records

| Concept | Information to preserve |
| --- | --- |
| Lexical/form context | Opaque caller reference; lemma; selected surface; part of speech/class; grammatical features; optional morphological structure |
| Reading candidate | Original string; normalized string and policy/version; notation; optional phonological interpretation; source spans; variety; evidence |
| Accent candidate | Reading reference; model/variety; Tokyo accent number where applicable; domain/context; alternative identity; evidence; resolution method |
| Evidence record | Source and locator; edition or access date; attribution and reuse status; reviewer; scope; observation versus prediction; rule/version if derived |
| Resolution result | Candidates; applicable constraints; conflicts; explanation; explicit unknown/unsupported/invalid diagnostics |
| Display result | Mora units; symbolic H/L where supported; drop location; textual alternative; assumptions and warnings; display settings kept separate |

Use two independent dimensions for provenance: **method** (supplied observation, dictionary consultation, rule-derived prediction) and **review state** (unknown, provisional, verified, disputed). A reviewed prediction remains a prediction. A source-backed observation can be disputed by another source. A numeric confidence score, if later introduced, must be calibrated and must not replace these distinctions.

For a Tokyo pattern with N morae, a known index is an integer 0…N. Unknown has no numeric value. Invalid input is a diagnostic, not an accent category. A proposed example result may say “reading supplied; accent unknown; no applicable rule”; that is preferable to an attractive but fabricated `[0]` graph.

## Proposed resolution priority

1. Match the requested variety, exact reading, grammatical analysis, and contextual scope. Reject incompatible records from consideration rather than overriding them by rank.
2. Prefer a manually verified record for that exact scope when the caller's policy permits it. Preserve other verified observations and source disagreements.
3. Consult documented lexical exceptions with evidence for the relevant construction. An exception for one reading or form must not automatically override every form of a spelling.
4. Apply a linguistically supported rule only if its class, structure, phonological, and prosodic preconditions are known. Record the rule and version; label its output as predicted.
5. Return alternatives, a conflict, or unknown when evidence is insufficient. An optional user preference may select a display candidate, but it cannot erase conflicting observations or promote a prediction to fact.

This is a policy proposal. No resolver, exception lexicon, inference algorithm, or production data source exists in this workspace.

## PLP as an independent consumer

PLP should supply a narrow adapter that converts its selected reading/accent/analysis records into plain linguistic input. It should retain stable form, reading, sense, analysis, and accent IDs in its own association layer. In particular, `form_analysis_readings` and `lexical_realizations` are explicit assertions, not instructions to construct a Cartesian product of all forms and readings. See the [model audit](implementation-audit.md).

MoraMaro should never load PLP environment files, connect to its database, manage reviews, or depend on authentication or web routes. PLP would own persistence, authorization, review decisions, revision checks, and compatibility migration. The engine would return diagnostics and candidate results for PLP to present or review.

Language/runtime packaging remains undecided. Python and JavaScript implementations currently duplicate pure behavior in PLP; options include maintained parity or a single normative representation with bindings. Choose after an extraction design review, without promising a public API now.

## Design validation before implementation

Define invariants for unknown values, alignment, source spans, alternatives, and provenance. Separate algorithmic tests of symbolic projection from a licensed, expert-reviewed linguistic evaluation set. An H/L projector can be correct for a supplied index even when that index is wrong for the word. Later accuracy reporting must identify the task, variety, evidence set, and evaluation method.
