# ELAN — Linguistic Annotator (canonical README snapshot)

Source: https://archive.mpi.nl/tla/elan and https://www.mpi.nl/corpus/manuals/manual-elan.pdf
Retrieved: 2026-04-30

## Overview

ELAN is a professional tool for the creation of complex annotations on video and audio resources. With ELAN a user can add an unlimited number of textual annotations to audio and/or video recordings. An annotation can be a sentence, word, gloss, comment, translation, or a description of any feature observed in the media. Annotations can be created on multiple layers, called tiers. Tiers can be hierarchically interconnected. An annotation can either be time-aligned to the media or refer to other existing annotations.

## Key features

- Up to 4 video streams plus audio waveform displayed simultaneously.
- Multi-tiered, hierarchical annotation (parent-child constraints).
- Controlled vocabularies and inter-tier dependency rules.
- Search across tiers, constraints, regular expressions, multi-document corpora.
- Multimedia formats: MPEG-1/2/4, AVI, WAV, MP3, MOV.
- Annotation export to FLEx, Praat TextGrid, Toolbox, CSV, subtitle formats, JSON.
- Imports MPEG7 XML, Praat TextGrid, Transcriber, CHAT, subtitles.

## Tier types

| Type | Stereotype |
|---|---|
| time-alignable | Independent, anchored to a time interval |
| symbolic association | One-to-one with a parent annotation |
| symbolic subdivision | One-to-many (e.g., word -> phonemes) |
| time subdivision | Equal time-divisions of a parent interval |
| included-in | Time interval contained in a parent interval |

## Data model

ELAN's native format is EAF (ELAN Annotation Format), an XML format defined by an external XSD schema. Each EAF references one or more media files by relative or absolute path. Tiers carry linguistic type metadata, optional controlled vocabularies, and parent-tier references. Annotations carry start/end time-slot references, an optional reference to a parent annotation, and the annotation value as text.

## License

ELAN is free software released under the GNU General Public License v3.0.

## Citations

The canonical reference is:
- Wittenburg, P., Brugman, H., Russel, A., Klassmann, A., & Sloetjes, H. (2006). ELAN: A Professional Framework for Multimodality Research. Proceedings of LREC 2006.

## Maintainer

The Language Archive (TLA), Max Planck Institute for Psycholinguistics, Nijmegen. https://www.mpi.nl/tla
