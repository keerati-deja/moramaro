# Accent variation and ambiguity

[Documentation home](../../README.md) · [Pitch accent](pitch-accent.md) · [Conjugation](conjugation-and-accent.md) · [Architecture](../architecture.md)

## A spelling does not identify one pattern

A written form can have several readings. A reading can belong to several lexical entries or senses, and one reading in one variety can have more than one documented accent. The useful unit of evidence is therefore an observation about a selected lexical/form/reading/context combination, not an unconditional spelling-to-number mapping.

Homographs share a written form; homophones share a pronunciation. Neither relation guarantees identical meaning, grammatical class, or accent. OJAD's [search for する](https://www.gavo.t.u-tokyo.ac.jp/ojad/eng/search/index/word:する) illustrates the identity problem: the irregular する entry and the godan entries 擦る/刷る appear under the same kana query. A future resolver must identify the intended entry before applying a verb-class rule. No extra accent values are inferred for those godan homophones here.

An inflected surface can also be grammatically ambiguous. The standard 食べられる example can be potential or passive even when the cited reading and accent coincide. Retain the analyses separately; agreement in one representation does not make the analyses equivalent.

## Named varieties, not a generic dialect switch

Tokyo Japanese does not supply a universal template. [Kubozono (2014), §1](https://www.isca-archive.org/tal_2014/kubozono14_tal.pdf) contrasts varieties with different distinctive pitch movements, numbers of patterns, domains, and counting units. Broad labels such as “Kansai” should not imply a single fully specified phonology. A future dataset should name the locality/variety, source convention, and relevant speaker or recording context.

A Tokyo numeric index is meaningful under the Tokyo model described in the [pitch chapter](pitch-accent.md). A variety requiring register distinctions or a different tonal domain needs an appropriate representation and renderer. The current PLP behavior of retaining a non-Tokyo label while applying Tokyo projection is metadata preservation, not dialect analysis. MoraMaro must disclose that boundary until a variety-specific model exists.

## Lexical, contextual, and constructional alternatives

Alternate pronunciations may involve reading, vowel length, contraction, or segmental realization as well as accent. Store alternatives at the layer where they occur. Two notations for one reading should not automatically become two separate pronunciations; two phonological readings should not be collapsed merely because their orthography is identical.

Inflection and following grammatical elements can condition accent. The [conjugation chapter](conjugation-and-accent.md) preserves OJAD's `[1]` and `[2]` alternatives for several 高い forms. [Kobayashi (2003)](https://doi.org/10.24467/onseikenkyu.7.2_101) studies variation and paradigm leveling in Tokyo adjectives, including grammatical and phonetic conditioning. A resource listing two patterns does not establish their frequency, social distribution, or interchangeability in every environment.

Compounds can acquire a pattern different from those of their independent constituents. Their grammatical structure, lexicalization, and suffixes matter. [Kawahara (2015), §§4 and 6](https://shigetokawahara.github.io/pdf/HandbookAccentPublished.pdf) provides a survey. A spelling containing two familiar words is insufficient evidence for two independent accent phrases or a particular compound accent.

Within speech, phrase boundaries, focus, and downstep affect surface realization. The same lexical observation can participate in different utterance contours. Conversely, an acoustic difference need not mean a dictionary entry has acquired a different lexical accent. A contextual record should distinguish lexical-pattern evidence from evidence about phrase realization; see [Venditti (1995/1997)](https://files.eric.ed.gov/fulltext/ED409733.pdf).

## Source disagreement and review states

Two sources may use different notation, editions, headword identities, varieties, or elicitation contexts. Apparent disagreement should first be checked for these differences. If the observations still conflict, retain both with their locators and scope. Choosing a preferred display is not permission to delete the other observation.

The proposed engine should represent at least these distinctions:

| State or method | Meaning | What it must not imply |
| --- | --- | --- |
| Unknown | No usable accent observation or applicable prediction | `[0]`, an error, or evidence of no accent |
| Provisional | A candidate or analysis awaits sufficient checking | Authoritative dictionary status |
| Verified | A reviewer checked an observation against identified evidence within a stated scope | Universality across speakers, varieties, forms, or contexts |
| Disputed | Incompatible evidence/analyses remain | Arbitrary automatic resolution by insertion order |
| Rule-derived prediction | A rule produced the candidate under recorded assumptions | Direct observation or measured speech |

Review status and derivation method are independent. A human may review a rule application without converting it into an observed pronunciation. “Verified against OJAD's displayed row” is also narrower than “independently verified by acoustic and speaker analysis.” The examples in this foundation use the former description.

## Practical record and display requirements

Retain the source/edition or access date, exact entry/form/reading, variety, context, notation convention, alternative identity, review state, and prediction method where applicable. Permit multiple observations without requiring a universal winner. Keep preference rank separate from confidence and from the accent index.

When context is missing, describe the assumption used for a diagram. When accent is unknown, show the reading and that state. When a pattern is unsupported by the renderer, preserve the source observation without fabricating a Tokyo contour. When a reading changes, revalidate alignment rather than silently preserving an index that now points to another mora. These are proposed behavior requirements, not already implemented MoraMaro features.
