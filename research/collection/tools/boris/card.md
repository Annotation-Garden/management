---
slug: boris
type: tool
strand: tools
year: 2016
authors: [Friard, Gamba]
venue: Methods in Ecology and Evolution
doi: 10.1111/2041-210X.12584
url: https://www.boris.unito.it/
license: GPL-3.0
modalities: [video, audio, behavior]
tags: [BORIS, video-coding, ethology, behavior, manual-annotation, ELAN-export, cross-platform]
agi_relevance: low
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

Behavioral Observation Research Interactive Software (BORIS) is a free desktop application for time-aligned event coding of video and audio, originally built for ethology and now widely used across animal-behavior, child development, and naturalistic-stimulus research.

## Summary

BORIS supports both state events (with start and stop times) and point events, multi-coder workflows, configurable ethograms with modifiers and exclusions, and standard reliability statistics (Cohen's kappa, intraclass correlation coefficient). It exports to CSV, TSV, XLSX, JWatcher, and ELAN EAF formats, enabling round-tripping with the broader linguistic and behavioral annotation ecosystem. The 2016 Methods in Ecology and Evolution paper presents the architecture, the time-budget analysis features, and benchmarks against commercial alternatives. BORIS is GPL-3.0 and runs on Windows, macOS, and Linux. It is the open-source counterpart to Datavyu and a complement to ELAN, with a stronger emphasis on quantitative ethogram analysis.

## Relevance to AGI

For AGI video and audio stimuli, BORIS is the natural manual-annotation entry point for labs that prefer a Graphical User Interface (GUI) over scripting. AGI must (a) ingest BORIS-exported CSV / EAF into BIDS events.tsv with HED tag mapping, and (b) round-trip annotations so that contributors can keep coding in BORIS while AGI maintains a versioned canonical form. BORIS's strength on inter-rater reliability matters because AGI's quality story depends on agreement metrics across contributors.

## Notable details

- State events and point events; configurable ethogram with modifiers.
- Inter-rater reliability: Cohen's kappa, intraclass correlation coefficient, time-bin analysis.
- Multi-camera and multi-coder workflows.
- Export to CSV, TSV, XLSX, JWatcher, ELAN EAF.
- GPL-3.0; cross-platform (Windows, macOS, Linux).

## Open questions / limitations

- No native HED tagging; controlled vocabularies remain ad hoc per ethogram.
- Single-user desktop application; collaboration relies on file exchange.
- Performance degrades on very long recordings (>4 hours) or large multi-camera setups.
- No native versioning or merge primitives; conflicting edits require manual reconciliation.
- Limited support for continuous-valued ratings; designed around discrete events.

## Citations

Primary: `friard2016boris`. Related:
- `wittenburg2006elan`, peer tool for hierarchical multi-tier annotation.
- `boersma2024praat`, phonetic counterpart for audio.
- `datavyu2014`, comparable open video-coding tool.
- `gorgolewski2016bids`, target schema for bringing BORIS exports into BIDS.
- `labelstudio2020`, modern web-based alternative for general annotation.
