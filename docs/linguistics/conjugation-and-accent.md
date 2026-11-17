# Conjugation, morphology, and pitch accent

[Documentation home](../../README.md) · [Mora](mora.md) · [Pitch accent](pitch-accent.md) · [Variation](accent-variation.md) · [References](../references-and-credits.md)

**Linguistic reference and future design requirements. No conjugation or accent-prediction engine is implemented in this workspace.** All numeric examples below concern the stated Tokyo-style reference patterns. They do not license one rule for every member of a grammatical class.

## Three different kinds of change

**Grammatical inflection** realizes a lexeme in a grammatical form: for example, past rather than nonpast. **Morphological structure** describes the pieces and their relationships: a stem, voice-related morphology, a negative element, a politeness auxiliary, and so on. **Accentual alternation** concerns whether a nucleus is present and where it is realized. These dimensions interact but are not interchangeable.

“Conjugation” (活用) in learner materials often groups together simple inflected forms, derived predicates, and combinations with auxiliaries. A list headed “conjugations” is therefore not itself a theory of word structure. Japanese school grammar, pedagogical grammars, and linguistic analyses also differ in their treatment of boundaries. [Hasegawa (2014), chapter 6](https://www.cambridge.org/core/books/abs/japanese/word-structure/27CCD8A3730F21D4C1BFC36CCD162070) explicitly discusses choices in organizing a paradigm and the role of auxiliary elements.

The distinction matters for accent because suffix identity, lexical accent class, stem shape, sound alternations, and prosodic grouping can all condition the result. Adding morae need not preserve the original index or simply place an accent a fixed distance from the new end. The same surface can also realize distinct grammatical analyses.

## How to read the examples and their evidence

`[0]` is positively unaccented. `[k]` locates the nucleus after mora k in the complete displayed reading. A slash between numbers denotes alternatives displayed by the cited source, not uncertainty resolved by choosing the first. The notation is explained in the [pitch chapter](pitch-accent.md).

The short example comparisons were checked on **2026-11-17** against OJAD's rendered word-search records with **Accent Variation: Show**. OJAD's marked mora position was converted to the bracket convention used here; plain-text search extracts alone lose that marking. This is source verification, not a new acoustic experiment or independent native-speaker judgment. The [provenance register](../references-and-credits.md#example-provenance-register) records search links, row IDs, and category labels. No source audio, diagrams, or dictionary database is distributed here.

The morphological operations below are descriptive recipes for these standard forms, not complete executable algorithms. Where a broader construction lacks a checked accent example here, its value is explicitly **unverified** and no number is supplied.

## Verb classes and accent classes are separate

| Verbal class | Morphological basis | What the class does not determine |
| --- | --- | --- |
| Godan — 五段動詞, often Group 1 | Consonant-final stems in a common linguistic analysis; kana endings alternate across vowel rows according to the following material | Whether the lexeme is accented, every sound alternation, or the accent of every construction |
| Ichidan — 一段動詞, often Group 2 | Vowel-final stems; many learner operations remove final る before attaching an ending | Whether an apparent -いる/-える verb belongs here; short-stem behavior and accent class |
| Irregular — 不規則動詞, often Group 3 | する and 来る require individually specified form relationships; compounds with them need lexical analysis | A single shared “irregular accent” pattern |

Godan and ichidan are grammatical classes, while accented/unaccented is an accentual distinction. Ending in る does not establish ichidan membership. Likewise, the ending -ない does not establish one invariant accent. Lexical identity and analysis must be selected before prediction can be attempted.

The two main examples are **書く** かく `[1]` (godan) and **食べる** たべる `[2]` (ichidan). Their checked outputs are listed below. Sources: [OJAD 書く](https://www.gavo.t.u-tokyo.ac.jp/ojad/eng/search/index/word:書く), row 192; [OJAD 食べる](https://www.gavo.t.u-tokyo.ac.jp/ojad/eng/search/index/word:食べる), row 1238. These are individual observations, not representative accuracy measurements.

| Category | Morphological transformation for these examples | From 書く かく `[1]` | From 食べる たべる `[2]` |
| --- | --- | --- | --- |
| Dictionary / nonpast | Citation form; godan -u / ichidan -ru in a common stem analysis | かく `[1]` | たべる `[2]` |
| Polite -ます | Godan i-row base + ます; ichidan stem + ます | かきます `[3]` | たべます `[3]` |
| Past -た / -だ | Apply class-specific past allomorphy; ichidan stem + た | かいた `[1]` | たべた `[1]` |
| Te-form -て / -で | Apply corresponding te allomorphy; ichidan stem + て | かいて `[1]` | たべて `[1]` |
| Negative -ない | Godan a-row base + ない; ichidan stem + ない | かかない `[2]` | たべない `[2]` |
| Volitional | Godan o-row + う; ichidan stem + よう | かこう `[2]` | たべよう `[3]` |
| Conditional -ば | Godan e-row + ば; ichidan stem + れば | かけば `[1]` | たべれば `[2]` |
| Potential | Godan e-row + る; ichidan stem + られる | かける `[2]` | たべられる `[4]` |
| Passive | Godan a-row + れる; ichidan stem + られる | かかれる `[3]` | たべられる `[4]` |
| Causative | Godan a-row + せる; ichidan stem + させる | かかせる `[3]` | たべさせる `[4]` |
| Imperative | Godan e-row ending; ichidan stem + ろ in these examples | かけ `[1]` | たべろ `[2]` |

The table changes the grammatical form and the reading together for readability. An engine must not assume those are one operation. For instance, correct generation of the kanji surface 食べられる still leaves its grammatical interpretation and accent evidence to be represented.

### Dictionary form and accentual conditioning

Dictionary forms provide lexical information, not a contour to paste unchanged over every derived form. Compare **買う** かう `[0]` with 書く かく `[1]`: both are godan, but they differ in accent class. OJAD's [買う record](https://www.gavo.t.u-tokyo.ac.jp/ojad/eng/search/index/word:買う), row 780, also gives かわない `[0]` and かえば `[2]`. An initially unaccented dictionary form can thus have an accented output in a particular construction.

Phonological structure matters as well as mora count. A purely numerical “penultimate mora” rule can target a dependent part of a heavy syllable; lexical and structural exceptions require attention. [Kawahara (2015), §5, pp. 464–467](https://shigetokawahara.github.io/pdf/HandbookAccentPublished.pdf) surveys accented versus unaccented predicates and their conditioned paradigms, including complications involving heavy syllables. This motivates analysis-specific rules rather than a universal class transform.

### Polite -ます forms

The polite nonpast adds the auxiliary ます to the appropriate base. In the checked examples the accent falls on ま, giving かきます `[3]` and たべます `[3]`; unaccented 買う also gives かいます `[3]` in OJAD row 780. This is evidence of a constructional accent effect, not preservation of the dictionary-form nucleus.

Polite past ました, negative ません, and volitional ましょう involve different following morphology and must be resolved as their own constructions. Their numeric accents are **unverified in this document**. Do not infer them by retaining the index of ます or treating every polite ending as an identical string replacement. Contractions, register, and prosodic context add further conditioning.

### Past and te-forms: sound change does not determine accent

Godan past/te formation includes 音便 (*onbin*) and allomorphy. Common correspondences are -く → -いた/-いて, -ぐ → -いだ/-いで, -す → -した/-して, -う/-つ/-る → -った/-って, and -む/-ぶ/-ぬ → -んだ/-んで. Ichidan 食べる uses 食べた/食べて. These correspondences describe segmental structure; they do not supply accent values. [Oshima (2014), §2.1, Tables 1–3](https://www.hum.nagoya-u.ac.jp/~oshima/docs/tetataratari.pdf) documents the classes and the exceptional behavior of 行く.

For the checked accented examples, 書く `[1]` → 書いた/書いて `[1]`, while 食べる `[2]` → 食べた/食べて `[1]`. The mora-index relation differs. **行く** いく `[0]` → いった/いって `[0]` illustrates exceptional segmental formation without introducing a nucleus in the cited patterns ([OJAD 行く](https://www.gavo.t.u-tokyo.ac.jp/ojad/eng/search/index/word:行く), row 740). It remains godan despite this exception.

Past and te-form similarity does not prove that their morphology or phrasing is identical in every environment. Oshima contrasts attachment-to-stem and attachment-to-infinitive analyses and argues from accentual-phrase evidence for the latter. That is an attributed analytical argument, not a settled implementation requirement. A future representation should allow a declared analysis instead of encoding a pedagogical shortcut as the only theory.

### Negative -ない and negative past

Godan negative formation uses the a-row base; verbs in -う use わ before ない, as in 買う → 買わない. Ichidan uses the stem directly. The checked accent comparisons include かく `[1]` → かかない `[2]`, たべる `[2]` → たべない `[2]`, and かう `[0]` → かわない `[0]`. The first case alone refutes a fixed dictionary-index copy.

Negative past adds a further layer: the negative element changes to なかった. OJAD row 780 gives **かわなかった `[3]`**, whereas row 1238 gives **たべなかった `[2]`**. Consequently, “negative is unaccented when the dictionary form is unaccented” cannot be extended unchanged to negative past. Lexical exceptions such as the special negative of ある also require separate treatment; no unverified accent number is asserted for them here.

### Volitional

The godan o-row plus う and ichidan よう create a long vowel at the end of these forms. In the examples, かこう `[2]` and たべよう `[3]` place the nucleus before the written final う. Buying gives かおう `[2]` despite かう `[0]` in the dictionary form. Thus volitional formation can introduce a nucleus and changes the reading's mora structure.

This discussion concerns the cited standard plain volitional forms. Polite volitional, contractions, dialectal alternatives, and pragmatic intonation cannot be assigned a contour merely by extrapolating from these three examples.

### Conditionals are several constructions

The -ば forms in the main table use an e-row base for godan and -れば for ichidan. Their accents depend on more than the surface ending: かけば `[1]` and たべれば `[2]` contrast with the checked unaccented-base output かえば `[2]`.

The -たら construction is distinct from -ば. **食べる** たべる `[2]` → **たべたら `[1]`** is independently supported by [Kawahara (2015), §6, example (29e), p. 468](https://shigetokawahara.github.io/pdf/HandbookAccentPublished.pdf), whose accented-mora apostrophe is converted here to `[1]`. The common surface recipe uses the past-shaped form plus ら, but morphological analyses differ. Do not substitute a -ば rule or assume that adding ら always leaves an accent unchanged.

Conditional と and なら also differ in syntax and prosodic structure. Their complete construction accents are **unverified here**. A future resolver needs the selected construction, not just a generic `conditional=true` flag.

### Potential, passive, and causative

Potential and voice-related morphology can create predicates that themselves take tense, polarity, and politeness. This motivates representing an ordered structure rather than a flat list of independent switches. Whether these operations are classified as inflection or derivation varies with the analysis; a user-facing “conjugation” label need not decide that issue.

The main table gives source-checked outputs for all three categories. In 食べられる, the standard potential and passive share the same surface and cited reading/accent; contextual meaning and syntactic structure still differ. Godan 書ける and 書かれる differ visibly and accentually. Generating the right surface therefore neither disambiguates the analysis nor proves the accent independently.

Colloquial ら抜き potential forms, shorter causatives, causative-passive combinations, and lexicalized predicates require their own usage and accent evidence. They are not automatically sanctioned by the standard examples. The potential of する is especially instructive: OJAD gives **する `[0]` → できる `[2]`**, a suppletive relationship rather than ordinary suffix substitution. No single voice/potential rule handles this exception.

### Imperative

Godan 書け and ichidan 食べろ illustrate two imperative formations. Their cited accents are `[1]` and `[2]` respectively. Alternate ichidan -よ, prohibitives, requests, and polite directives are different forms/constructions; none should be conflated with an imperative ending on the basis of communicative function alone.

The irregular imperative **する `[0]` → しろ `[0]` / せよ `[1]`** directly demonstrates that alternate forms can have different patterns. Source: [OJAD する](https://www.gavo.t.u-tokyo.ac.jp/ojad/eng/search/index/word:する), row 2317, *Group 3* (not the homophonous godan 擦る or 刷る rows). Register and lexical identity belong in the record.

## Irregular verbs: reading alternation is not optional

来る requires different readings of its written root across forms. The following comparisons are checked in [OJAD 来る](https://www.gavo.t.u-tokyo.ac.jp/ojad/eng/search/index/word:来る), row 1853:

| From 来る くる `[1]` | Result | Why it matters |
| --- | --- | --- |
| Polite | きます `[2]` | Reading changes to き before ます |
| Te / past | きて `[1]` / きた `[1]` | Shared reading alternation does not equal dictionary-reading concatenation |
| Negative | こない `[1]` | Reading changes to こ |
| Conditional -ば | くれば `[1]` | Uses a different base from the negative |
| Potential / passive | こられる `[3]` | Same surface can support different analyses |
| Causative | こさせる `[3]` | Additional morphology changes the nucleus position |
| Imperative | こい `[1]` | Individually specified formation |
| Volitional | こよう `[2]` | Individually specified base plus volitional material |

The する comparisons above show a different paradigm: します `[2]`, して `[0]`, and できる `[2]` do not follow the 来る alternations. Compounds ending in する or 来る may have lexicalized readings, structure, and accent behavior. A class named “irregular” is a request for lexical information, not a predictive rule.

## Auxiliary constructions and prosodic domains

The verified ます and ない comparisons already show why auxiliary identity matters. More elaborate expressions can combine a te-form with いる, おく, しまう, or みる; an appropriate base with たい, そうだ, or らしい; or voice-related morphology with negative and polite elements. The attachment site, intended meaning, contraction, and phrase grouping need specification.

For example, the te-form in 書いている is the **verified component** かいて `[1]`; the full expression's accent is **unverified here**. Likewise, 書きたい and 書いてしまう are morphological illustrations with **unverified complete-expression accent**. No numeric contour is implied by joining the components. A complete-expression observation, or an applicable documented construction rule with its assumptions, is needed before assigning one.

[OJAD Verb Suffix Search](https://www.gavo.t.u-tokyo.ac.jp/ojad/kouzokugo) is a relevant future checking resource; it is not a dataset bundled with MoraMaro. [Minematsu et al. (2017)](https://doi.org/10.1587/transinf.2016AWI0007) distinguishes resources for conjugations, verb-plus-auxiliary expressions, and sentence prosody. That distinction informs the separation of responsibilities here; OJAD's functionality and published evaluations are not MoraMaro functionality or accuracy results.

## I-adjectives — い形容詞

An i-adjective has its own paradigm. It is not a verb with an interchangeable suffix table, and it is not normally made predicative by simply adding だ to its dictionary form. The following checked example starts from **高い** たかい `[2]`. Source: [OJAD 高い](https://www.gavo.t.u-tokyo.ac.jp/ojad/eng/search/index/word:高い), row 2939. Both displayed alternatives are retained.

| Category | Morphological operation | Checked result from たかい `[2]` |
| --- | --- | --- |
| Dictionary / nonpast | Citation -い form | たかい `[2]` |
| Negative | Replace final い with く and combine with ない | たかくない `[1]` / `[2]` |
| Past | Replace final い with かった | たかかった `[1]` / `[2]` |
| Negative past | Negative construction with なかった | たかくなかった `[1]` / `[2]` |
| Adverbial | Replace final い with く | たかく `[1]` / `[2]` |
| Conditional -ければ | Replace final い with ければ | たかければ `[1]` / `[2]` |
| Connective -くて | Adverbial-shaped form plus て | たかくて `[1]` / `[2]` |

These alternatives are especially important for a resolver: choosing a historically familiar “shift left” pattern alone would discard a displayed alternative. [Kobayashi (2003)](https://doi.org/10.24467/onseikenkyu.7.2_101) reports adjective paradigm leveling and conditioning by grammatical and phonetic factors. Her study is evidence that variation deserves explicit representation, not a claim that every speaker accepts every listed alternative in every context.

In the simplified H/L model, the negative alternatives た・か・く・な・い yield `H L L L L` for `[1]` and `L H L L L` for `[2]`. These strings are independently derived renderings of the source-checked indices, not copied acoustic contours.

Conditional -かったら is another construction, e.g. 高かったら. Its accent is **unverified here**; the table's -ければ values do not automatically apply. Negative conditionals involve still more morphology and need their own evidence. Adjectives with an irregular or suppletive stem relationship, notably いい and よい-related forms, cannot be generated by blindly replacing the last character. Compounds and lexicalized adjectives also need separate treatment. No unverified values are supplied for them.

## Na-adjectives — な形容詞 / 形容動詞

Na-adjectives are often analyzed as adjectival nominals or nominal/adjectival stems combining with copular material. The labels 形容動詞 and “adjectival noun” reflect different grammatical traditions. Keep the lexical stem distinct from its construction: 静か, 静かな…, 静かだ, 静かです, and 静かに… occupy different environments.

Checked comparisons from [OJAD 静か](https://www.gavo.t.u-tokyo.ac.jp/ojad/eng/search/index/word:静か), row 3149, are **しずかだ `[1]`**, attributive **しずかな `[1]`**, polite **しずかです `[1]`**, past **しずかだった `[1]`**, negative **しずかじゃない `[1]`**, negative past **しずかじゃなかった `[1]`**, conditional **しずかならば `[1]`**, and adverbial **しずかに `[1]`**. These compare complete listed forms; no independent isolated-stem accent is inferred.

Morphologically, the stem remains while the copular/linking material changes: な in the attributive environment, だ/です in predication, だった for past, じゃない in the cited negative construction, ならば for this conditional, and に for adverbial use. Uncontracted ではない, other politeness forms, and differing phrase boundaries must be recorded as their own constructions rather than substituted without checking.

Retention of `[1]` throughout this example is a fact about the listed 静か patterns. It is not a rule that all na-adjectives retain one index, nor that following nouns never affect prosody. The +N column shows the adjectival portion before a noun; it does not establish the accent of an arbitrary full noun phrase. Variation, lexicalization, and accentual-phrase boundaries remain relevant even when the stem spelling stays unchanged.

## Compounds and suffix-driven changes

Compound words require structure: which constituents combine, whether the result is lexicalized, and which domain carries the accent. Concatenating the isolated accents of both constituents can produce an impossible representation for the intended single Tokyo accentual domain. Suffixes likewise differ in whether they preserve, introduce, shift, or suppress accent; suffix identity is a linguistic input.

A small source-verified illustration is **うまい `[2]` → うまさ `[1]`** (nominalizing -さ), alongside the -たら comparison above. [Kawahara (2015), Table 5 and §6](https://shigetokawahara.github.io/pdf/HandbookAccentPublished.pdf) supplies the former in accented-mora notation. These examples show that nominalization and conditional morphology are distinct accentual environments; they do not establish a general “all suffixes shift left” rule. No compound-specific numeric example is asserted without an identified structural and lexical source.

## Four responsibilities for an eventual engine

1. **Generate a grammatical form:** produce a candidate surface with class, features, and structure. Correct spelling is the output of this step, not proof of pronunciation.
2. **Determine its reading:** select or derive the appropriate reading, including irregular alternations and alternatives. A grammatical analysis can constrain the reading without uniquely determining it.
3. **Determine its accent pattern:** consult matching observations, documented exceptions, and supported rules for the selected variety and construction. Preserve unknowns, alternatives, and conflicts; label predictions.
4. **Render that pattern:** align a selected, valid pattern to morae and display it. Rendering is deterministic only after its inputs and model are specified; a valid diagram is not independent evidence for its accent.

Rule-based prediction should stop when class, reading, structure, or prosodic context is missing, or when the rule's documented domain does not cover the case. Source disagreement should remain visible. Schökler's [2019 ICPP abstract/program entry](https://www2.ninjal.ac.jp/past-projects/crosslinguistic-studies/prosody/index6f6d.html) is included as a structural research reference; its PDF was not substantively verified during this task, and no examples here depend on it. The proposed engine must not advertise this research as an implemented algorithm.
