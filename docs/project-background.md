# Project background

[Documentation home](../README.md)

## Origin and purpose

MoraMaro (モラマロ), intended repository identity `keerati-deja/moramaro`, originates in Polyglot Learning Pipeline (PLP). PLP first developed mora segmentation and Japanese pitch-accent visualization to support vocabulary and pronunciation features. MoraMaro establishes a separate, reusable project around that foundation. This documentation task does not extract, move, or change the PLP implementation.

The goals are to support PLP's Japanese vocabulary, pronunciation, and grammatical-form modules; make reusable linguistic functionality available to developers, learners, researchers, and learning applications; and prepare a linguistically grounded basis for later morphology and pitch analysis.

The name is a playful reversal of “Mora” inspired by Thai wordplay. Its Japanese-looking form is a brand, not an etymological claim.

## Independence and ownership

MoraMaro should accept plain linguistic input and return results with provenance and diagnostics. It should not require PLP database schemas, user accounts, authentication, web services, deployment configuration, or infrastructure. PLP should retain its lexical entries, meanings, human review, grammatical analyses, and associations between those records.

For example, PLP may decide that a written form belongs to a particular sense and grammatical analysis, then supply its selected reading and accent observation to MoraMaro. MoraMaro can eventually validate and visualize that input without knowing the database IDs or changing their ownership. A future optional generator or resolver would produce candidates for PLP to review; a candidate would not silently become an authoritative lexical fact.

## Intended users

Developers need stable representations and honest failure states. Learners and teachers need accessible diagrams with a stated variety and context. Researchers need alternate readings, alternative patterns, explicit analytical assumptions, and traceable evidence. These needs motivate separate linguistic records and display preferences rather than a spelling-to-one-contour shortcut.

## Present boundary

This is a documentation-only foundation. [The audit](implementation-audit.md) distinguishes inspected code and test assertions from historical validation reports. [The roadmap](roadmap.md) distinguishes extraction candidates from unimplemented and research-dependent capabilities. No package, API, accuracy rate, coverage guarantee, or performance claim follows from the existence of these documents.
