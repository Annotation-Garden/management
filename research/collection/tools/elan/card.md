---
slug: elan
type: tool
strand: tools
year: 2006
authors: [Wittenburg, Brugman, Russel, Klassmann, Sloetjes]
venue: LREC 2006 / Max Planck Institute for Psycholinguistics
doi: null
url: https://archive.mpi.nl/tla/elan
license: GPL-3.0
modalities: [video, audio, behavior, eyetrack]
tags: [annotation, multimodal, sign-language, video-coding, time-aligned, linguistics, MPI, Nijmegen]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

ELAN is a desktop annotation tool for hierarchical, time-aligned annotations of audio and video, originally built at the Max Planck Institute for Psycholinguistics for sign-language and gesture research, and the de facto standard for naturalistic stimulus annotation in linguistics, ethology, and infant research.

## Summary

ELAN (EUDICO Linguistic Annotator) provides multi-tier annotation of synchronized audiovisual recordings, with strict temporal alignment and parent/child tier dependencies that enforce annotation grammars. It supports up to four simultaneous video streams, waveform display, controlled vocabularies, and external lexicon links. The native EAF format is XML-based and widely supported by downstream phonetic, gestural, and corpus-linguistic toolchains. Releases are GPL-3, run on Windows, macOS, and Linux, and are maintained by The Language Archive (TLA) at MPI Nijmegen. ELAN interoperates with Praat (TextGrid import / export), CLAN, FLEx, and several BIDS conversion scripts.

## Relevance to AGI

ELAN is the dominant tool researchers reach for when annotating naturalistic video stimuli (Forrest Gump, HBN Movies, Pixar shorts) at sub-second precision. AGI must (a) ingest EAF files into the Stim-BIDS events.tsv schema, (b) preserve tier hierarchies as nested HED tags or sidecar JSON, and (c) round-trip annotations so contributors can keep working in ELAN while the AGI repository holds a versioned, validated form. Without an EAF importer, AGI cannot capture the existing investment of linguistics and infant-cognition labs in ELAN-based corpora.

## Notable details

- Tier types: symbolic association, symbolic subdivision, time subdivision, included-in.
- Native format: EAF (XML); also exports to Praat TextGrid, CSV, Toolbox, FLEx, subtitle (SRT), and JSON.
- Supports controlled vocabulary import from ISO Data Category Registry (DCR).
- Plays multiple videos in lock-step and aligns to PCM waveform.
- Used in CHILDES, TalkBank, DGS (German Sign Language) corpora, and ManyBabies.
- ELAN-CV (computer vision plugin) integrates OpenPose / face detectors as automatic annotation tiers.

## Open questions / limitations

- No native HED schema validation; users hand-roll controlled vocabularies that drift across labs.
- EAF lacks a stable identifier system for media or annotations, complicating provenance once files are renamed.
- Performance degrades for files longer than 4 hours or more than 30 tiers.
- No first-class support for tracking inter-annotator agreement at scale.
- Single-user desktop; no built-in versioning, review, or merge primitives.

## Citations

Primary: `wittenburg2006elan`. Related:
- `friard2016boris` — comparable open-source video event logger.
- `boersma2024praat` — companion tool for phonetic annotation, interoperates via TextGrid.
- `mcnamara2017pliers` — programmatic alternative for automated multimodal feature extraction.
- `gorgolewski2016bids` — target schema for bringing ELAN annotations into reproducible workflows.
