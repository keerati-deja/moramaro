# Mora — 拍 / モーラ

[Documentation home](../../README.md) · [Pitch accent](pitch-accent.md) · [References](../references-and-credits.md)

## Mora, syllable, and rhythm

A **mora** (拍, モーラ; plural *morae*) is a unit of phonological weight and rhythmic organization. A **syllable** (音節) groups sounds around a nucleus. In a familiar syllabic analysis of Japanese, a short open syllable such as か /ka/ has one mora, while a heavy syllable such as かん /kaN/ has two. Thus counting syllables and counting morae answer different questions. Syllable structure in Japanese also has competing theoretical analyses; a kana display should not silently settle that debate.

Japanese makes extensive use of mora counts in rhythm, word formation, and verse. “Mora-timed” is useful as a structural description and teaching cue, but it does not mean every mora has the same measured duration. Speech rate, segments, devoicing, and phrase position affect timing. [Warner and Arai (2001)](https://pubmed.ncbi.nlm.nih.gov/11096367/) review the evidence and competing timing hypotheses. Equal horizontal spacing in MoraMaro diagrams is an alignment convention, not a duration measurement.

## Ordinary and special morae

An ordinary or independent mora (自立拍) commonly contains a vowel, optionally preceded by consonantal material: あ, か, and きゃ each represent one mora in the examples below. **Yōon** (拗音) combines a kana such as き with a small ゃ/ゅ/ょ: きゃ is one mora, whereas きや has two. The small kana does not supply another timing position. Similar grouping occurs in loanword spellings such as ティ, but treating every small kana after every character as a valid combination is only a software heuristic.

The **special morae** (特殊拍) include:

| Term | Typical spelling | Phonological interpretation |
| --- | --- | --- |
| Sokuon — 促音 | っ / ッ | A mora associated with consonant gemination, often represented /Q/. In がっこう it contributes closure duration before /k/, not an independently pronounced “tsu” |
| Hatsuon — 撥音 | ん / ン | The moraic nasal, often /N/. Its realization depends on surrounding sounds; it is not always an alveolar [n] |
| Chōon — 長音 | ー or vowel kana | A long vowel occupies two morae; the length portion supplies the second. /R/ or /H/ is sometimes used as an analytical symbol, not a literal kana |

[Youngberg (2018), introduction and §2](https://www.soas.ac.uk/sites/default/files/2023-09/The%20Japanese%20Moraic%20Nasal%20Revisited%20-%20A%20First%20Glance.pdf) discusses the special morae, the context-sensitive realization of /N/, and competing representations. This documentation uses /N/, /Q/, and a vowel-length unit descriptively; it does not adopt his proposed nasal-vowel analysis as the only analysis. Some accounts also discuss the second member of a diphthong among special morae; that classification needs a stated phonological analysis.

## Checked segmentation examples

The dots below separate **mora positions**, not necessarily syllables, morphemes, or Unicode characters. The table is independently composed. Counts follow the stated conventional reading analysis; the PLP tests independently corroborate the overlapping software cases, not every phonetic interpretation.

| Word / reading | Mora segmentation | Count | What it illustrates |
| --- | --- | --- | --- |
| 仮名 — かな | か・な | 2 | Two ordinary morae |
| 客 — きゃく | きゃ・く | 2 | Yōon occupies one position |
| 今日 — きょう | きょ・う | 2 | Long /oː/ after yōon; two morae, commonly one heavy syllable |
| 学校 — がっこう | が・っ・こ・う | 4 | /gaQkoR/; sokuon and vowel length both count |
| 新聞 — しんぶん | し・ん・ぶ・ん | 4 | Two nasal morae |
| ティー | ティ・ー | 2 | Loanword combination plus length |
| おばさん | お・ば・さ・ん | 4 | Short vowel |
| おばあさん | お・ば・あ・さ・ん | 5 | Added vowel length distinguishes the word |
| 東京 — とうきょう | と・う・きょ・う | 4 | Two long vowels; kana spelling differs from /toːkʲoː/ |
| 本 — ほん | ほ・ん | 2 | Commonly one heavy syllable, two morae |

For school and Tokyo, the final う is retained as a display unit because it is present in the reading. This does not claim that an independent [ɯ] is pronounced. Counting a long vowel as two morae likewise does not imply two separate vowel articulations.

## Orthography is not phonological analysis

Kana provides unusually useful cues, but the relationship is not one character to one mora. きょ uses two characters for one mora; a decomposed voiced kana can use a base character plus a combining mark for one kana; a single kanji can represent several morae. A segmentation function cannot determine the reading of 生 merely by splitting its written characters.

Long vowels can be written with ー, repeated vowels, or sequences such as おう/えい. Whether a sequence is realized as a long vowel or a vowel sequence can depend on the lexeme, morphological boundary, and speaking style. Orthographic counts may coincide while phonological structure differs. Retain that distinction instead of replacing every vowel sequence mechanically.

Particles は, へ, and を also illustrate spelling/pronunciation differences. Devoicing does not automatically remove a phonological mora. Expressive spellings, sentence-final っ, iteration marks, historical kana, punctuation, and mixed-script text need separate policy; a display heuristic is not evidence of their full phonological treatment.

## Unicode and segmentation policy

The proposed engine should preserve the original input and state any normalization policy. **NFC** can compose a canonically equivalent voiced-kana sequence such as `か` + U+3099 into `が`. **NFKC** additionally performs compatibility folding, useful for halfwidth forms such as `ｶﾞ`, but may change distinctions a caller wants to retain. Normalization does not itself determine mora boundaries. See [Unicode UAX #15](https://www.unicode.org/reports/tr15/).

Unicode extended grapheme clusters group user-perceived characters; they are not Japanese morae. A grapheme algorithm need not combine き and ゃ into one mora. Conversely, UTF-16 code units or Unicode scalar values are not reliable mora counts. [Unicode UAX #29](https://www.unicode.org/reports/tr29/) defines general text segmentation, which needs language-specific interpretation for this task.

The current PLP implementation attaches listed small kana and combining marks to preceding units and trims outer whitespace. It does **not** normalize, expand kanji readings, validate legitimate kana combinations, or reject all non-kana input. Standalone small kana and internal punctuation can therefore become counted units; halfwidth sequences are not promised to work. See the [implementation audit](../implementation-audit.md). Future work should specify rejection versus preservation, retain source offsets across normalization, and separate orthographic segmentation from optional phonological interpretation.

## Consequences for accent alignment

Accent indices count mora positions, not kanji or individual small kana. A reading edit can change the count and invalidate a stored index. Some phonological analyses restrict accent placement on dependent positions in heavy syllables; a numeric range check alone cannot verify those restrictions. For example, accepting an integer within 0…N establishes a renderable index, not a linguistically attested lexical accent. MoraMaro must keep these two validations distinct.
