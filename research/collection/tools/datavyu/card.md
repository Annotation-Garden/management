---
slug: datavyu
type: tool
strand: tools
year: 2014
authors: [Datavyu Team]
venue: Databrary Project, New York University
doi: null
url: https://datavyu.org
license: GPL-3.0
modalities: [video, audio, behavior]
tags: [Datavyu, Databrary, video-coding, infant, developmental, manual-annotation, Ruby-scripting]
agi_relevance: low
imported_from: null
added: 2026-04-30

pdf_status: not-applicable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

Datavyu is an open-source video and audio coding tool built around a sheet-based annotation interface, used heavily in developmental psychology and infant research, and integrated with the Databrary repository for managed-access video sharing.

## Summary

Datavyu descends from MacSHAPA / OpenSHAPA and is maintained by the Databrary Project at New York University. The interface treats annotations as rows in a structured sheet where each row is an event with start, stop, and user-defined columns; the tool supports multiple synchronized video and audio panels, frame-level navigation, and per-pass code dictionaries. A Ruby scripting Application Programming Interface (API) lets users automate batch processing and inter-coder reliability. Datavyu is GPL-3.0 and runs on macOS, Windows, and Linux. It pairs naturally with Databrary, which provides managed-access video sharing under institutional review board (IRB) constraints.

## Relevance to AGI

For developmental and infant-cognition stimuli (Healthy Brain Network movies, ManyBabies, infant looking-time paradigms), Datavyu is the dominant manual coding tool. AGI must (a) ingest Datavyu sheets into Brain Imaging Data Structure (BIDS) events.tsv with appropriate column mapping and Hierarchical Event Descriptors (HED) layering, (b) cooperate with Databrary's managed-access model when annotated stimuli themselves cannot be redistributed (consented child videos), and (c) document round-trip workflows so labs can keep their preferred coding interface.

## Notable details

- Sheet-based interface with per-pass code dictionaries.
- Ruby scripting API for batch operations and reliability.
- XML-friendly project file format.
- Tight integration with Databrary's managed-access video archive.
- GPL-3.0; cross-platform binaries for macOS, Windows, Linux.

## Open questions / limitations

- No native HED tagging.
- Single-user desktop with no concurrent editing.
- Performance issues on very long recordings or complex multi-camera setups.
- Limited modern UI affordances; learning curve is real for new users.
- Sharing path through Databrary works only for user-uploaded video, not open-stimulus collections.

## Citations

Primary: `datavyu2014`. Related:
- `wittenburg2006elan`, peer multi-tier video annotation tool.
- `friard2016boris`, peer event-logging tool.
- `boersma2024praat`, phonetic annotation companion.
- `gorgolewski2016bids`, target schema for BIDS export.
- `labelstudio2020`, modern web-based alternative.
