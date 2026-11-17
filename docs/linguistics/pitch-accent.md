# Japanese pitch accent — 日本語の高低アクセント

[Documentation home](../../README.md) · [Mora](mora.md) · [Conjugation and accent](conjugation-and-accent.md) · [Variation](accent-variation.md)

## Lexical accent and the Tokyo model

Lexical pitch accent concerns contrasts associated with words and morphological forms. In Tokyo Japanese, the presence and position of an accentual fall distinguish patterns. This differs from a stress-accent account organized around stressed syllables and their prominence. Pitch, duration, and intensity can interact in real speech; “pitch accent” does not mean every other acoustic dimension is irrelevant. See [Kawahara (2015), §1](https://shigetokawahara.github.io/pdf/HandbookAccentPublished.pdf).

This chapter uses a **Tokyo-style symbolic model**. H (High) and L (Low) indicate relative levels in that model, not fixed frequencies, universal speaker ranges, or one pitch target per written kana. The **accent nucleus** (アクセント核) is the position associated with the lexical fall, conventionally the mora immediately before it. A high plateau can contain several high morae but only one nucleus.

## Accent numbers and pattern names

For a reading of N morae, `[k]` with 1 ≤ k ≤ N marks a fall after mora k. `[0]` means **unaccented** (無核): no lexical nucleus in this representation. An unknown accent is missing or explicitly unknown data, never automatically zero. An out-of-range number is invalid input, not an unknown linguistic pattern.

| Pattern | Japanese | Index | Simplified profile for a 3-mora word plus a neutral が in the same phrase |
| --- | --- | --- | --- |
| Heiban | 平板型 | `[0]` | L H H + H |
| Atamadaka | 頭高型 | `[1]` | H L L + L |
| Nakadaka | 中高型 | `[k]`, 1 < k < N | L H L + L for `[2]` |
| Odaka | 尾高型 | `[N]` | L H H + L |

These names describe a familiar pedagogical classification. A one-mora accented word has its nucleus both initially and finally; positional names do not create two distinct patterns in that case. Some dictionaries use other symbols or relative-to-end indices. Convert a source's notation only after establishing its convention.

The independently typeset examples below are traceable to [Kubozono (2014), examples (2)–(3), p. 195](https://www.isca-archive.org/tal_2014/kubozono14_tal.pdf). They describe those Tokyo patterns, not all speakers or contexts.

| Word | Reading and index | Word + が, aligned by mora | Gloss |
| --- | --- | --- | --- |
| 兜 | かぶと `[1]` | か ぶ と ＋ が → H L L ＋ L | helmet |
| 心 | こころ `[2]` | こ こ ろ ＋ が → L H L ＋ L | heart |
| 男 | おとこ `[3]` | お と こ ＋ が → L H H ＋ L | man |
| 魚 | さかな `[0]` | さ か な ＋ が → L H H ＋ H | fish |

An abstract diagram makes the odaka/heiban distinction visible without relying on a particular spelling:

```text
positions:        1   2   3  | particle
unaccented [0]:   L ─ H ─ H ─ H
final accent [3]: L ─ H ─ H ↓ L
```

The diagram is original schematic notation, not a copied source image or an F0 trace. The particle lies outside the lexical word's N positions.

## Initial rise and following particles

The simplified Tokyo projection starts low and rises after the first mora unless the first mora is accented. This **initial lowering/rise** belongs to phrase-level tonal organization; it is not a separate lexical nucleus. A word inside an existing phrase need not receive a fresh dictionary-style rise. Heavy initial syllables and phonetic realization also complicate a literal “first mora low, second high” reading of the diagram.

Following material matters because an odaka fall occurs at the word edge. A word alone can conceal the difference between final accent and no accent. A neutral particle in the same accentual phrase helps display the contrast, as the examples above show. This does not license appending が to every verb, adjective, or inflected form. Grammatical compatibility and the actual particle/construction must be established first.

Particle behavior cannot be generalized from a one-mora neutral continuation to all 助詞. Some particles and combinations introduce their own tonal or phrasing effects. A phrase boundary can reset the relevant tonal domain. The existing PLP renderer's contextual-particle option is a display aid, not a particle grammar or prosodic resolver.

## Accentual phrases and downstep

An **accentual phrase** (アクセント句) is a prosodic grouping with its own tonal organization. It may include a lexical word and following grammatical material; orthographic spaces are not its definition. Several accentual phrases can belong to a larger intonational phrase. Boundaries, focus, and syntactic grouping affect how lexical patterns are realized.

Two uses of “downstep” should be kept distinct. Learner diagrams often use a downstep mark for the local fall after an accent nucleus. In phonetic/intonational analysis, **downstep** also denotes the lowering/compression of the following phrase's pitch register after an accented phrase within the relevant larger domain. Simply joining independently drawn word-level H/L strings does not model this register relation. [Kubozono (1992), pp. 368–397](https://www.cambridge.org/core/books/abs/gesture-segment-prosody/modeling-syntactic-effects-on-downstep-in-japanese/3D345B4D7EE4999479654F630F991C6D) discusses this distinction in modeling Japanese downtrend.

**Declination**, a more gradual downward trend, is also not synonymous with a lexical fall. A phrase boundary may introduce a reset; an utterance-final rise can interact with a word's lexical accent. A future phrase module needs boundaries and context rather than a rule that every written word restarts at L.

## Symbolic pitch, intonation, and F0

Keep three representations separate:

1. **Lexical accent:** an abstract property such as a known nucleus position or unaccented class.
2. **Intonation:** phrase and utterance organization, including boundary tones, discourse prominence, and pitch-range changes.
3. **Acoustic F0:** an estimated fundamental-frequency trajectory from voiced portions of actual speech, or a trajectory generated by a synthesis system.

H/L is a symbolic simplification. Voiceless closure and devoiced vowels may have no reliable local F0 estimate even though their morae remain in a phonological representation. Peaks need not align exactly with equal-width boxes; segmental perturbations and tracking errors are not necessarily accents. [Venditti's Japanese ToBI guidelines (1995/1997), §§2–4](https://files.eric.ed.gov/fulltext/ED409733.pdf) distinguish lexical labels, tonal events, and prosodic boundaries. MoraMaro's proposed records are not a claim of J_ToBI conformance.

A smooth “Pitch Curve” display is still a drawing of the symbolic model. It becomes measured speech evidence only when accompanied by actual audio, an analysis method, and time alignment; it becomes synthesized speech only through a separate synthesis process. Neither exists in this documentation-only workspace.

## Dialect and coverage limits

Tokyo Japanese is one accent system. Other varieties differ in the number of contrastive patterns, rise versus fall, register distinctions, domains, or the unit used to count prosodic distance. [Kubozono (2014), §1](https://www.isca-archive.org/tal_2014/kubozono14_tal.pdf) explicitly compares these dimensions. A Tokyo index plus a different dialect label is not sufficient dialect modeling.

The existing PLP formula accepts supplied indices mechanically. It neither establishes a word's dictionary accent nor proves that every 0…N index is possible for every reading. Compound structure, inflection, lexical exceptions, alternate readings, and contextual phrasing require separate evidence. See [variation and ambiguity](accent-variation.md) and the [architecture proposal](../architecture.md).
