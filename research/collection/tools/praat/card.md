---
slug: praat
type: tool
strand: tools
year: 2024
authors: [Boersma, Weenink]
venue: University of Amsterdam (continuous release since 1992)
doi: null
url: https://www.fon.hum.uva.nl/praat/
license: GPL-3.0
modalities: [audio, behavior]
tags: [Praat, phonetics, TextGrid, spectrogram, formants, pitch, scripting, linguistics]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-applicable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

Praat is the canonical desktop tool for phonetic analysis and time-aligned audio annotation, built around the TextGrid annotation format and a built-in scripting language for reproducible analyses.

## Summary

Praat has been continuously developed by Paul Boersma and David Weenink at the University of Amsterdam since 1992 and is the dominant tool for phonetic annotation, acoustic analysis, and speech synthesis in linguistic and cognitive-science research. Its TextGrid format supports multiple interval and point tiers with arbitrary string labels and is supported by ELAN, Phon, EMU, BIDS-converters, and most downstream phonetic toolchains. Praat includes spectrogram, pitch, formant, and intensity displays, statistical pattern analyses, multiple speech-synthesis backends, and a scripting language that lets users automate pipelines. It is GPL-3.0 and runs on every major platform.

## Relevance to AGI

For AGI's audio-bearing stimuli (Forrest Gump dialog, Pixar shorts, podcast excerpts, infant directed speech), Praat is the dominant phonetic-annotation tool that downstream linguistic labs use. AGI must (a) ingest TextGrid annotations into BIDS events.tsv with phonemes, words, and prosody as separate annotation types, (b) emit TextGrids back to contributors who prefer the Praat workflow, and (c) document HED-LANG-style mappings from Praat tier labels to formal vocabulary. Whisper plus Praat is also a natural pairing: Whisper produces an initial transcription and word-level timestamps that Praat annotators refine.

## Notable details

- TextGrid format is the lingua franca of phonetic annotation.
- Tier types: interval (with start, stop, label) and point (with time, label).
- Scripting language enables reproducible batch analyses.
- Cross-platform: Windows, macOS, Linux, FreeBSD, Solaris.
- License: GPL-3.0.

## Open questions / limitations

- No native HED tagging.
- Single-user desktop with no concurrent editing.
- Older user-interface conventions; learning curve for new users.
- TextGrid format does not record provenance (who annotated, with what version).
- Performance on long recordings (>2 hours) requires careful chunking.

## Citations

Primary: `boersma2024praat`. Related:
- `wittenburg2006elan` — peer multi-tier annotation tool that imports TextGrids.
- `friard2016boris` — peer event-logging tool for video plus audio.
- `radford2023whisper` — companion ASR model whose transcripts feed Praat.
- `gorgolewski2016bids` — target schema for TextGrid conversion.
- `crosse2016mtrf` — analysis toolbox that consumes phonetic boundaries.
