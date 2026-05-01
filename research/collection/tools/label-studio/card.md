---
slug: label-studio
type: tool
strand: tools
year: 2020
authors: [Tkachenko, Malyuk, Holmanyuk, Liubimov]
venue: HumanSignal (Heartex) open source project
doi: null
url: https://github.com/HumanSignal/label-studio
license: Apache-2.0
modalities: [image, video, audio, text, time-series, multimodal]
tags: [Label-Studio, web-annotation, ML-backend, multimodal, polygons, bounding-boxes, segmentation]
agi_relevance: low
imported_from: null
added: 2026-04-30

pdf_status: not-applicable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

Label Studio is a free, open-source web-based data labeling platform that supports text, image, audio, video, and time-series annotation, with a pluggable Machine Learning (ML) backend that lets model predictions pre-fill annotations for human correction.

## Summary

Label Studio is the most widely adopted general-purpose annotator outside specialized linguistic and ethological tools. It uses an Extensible Markup Language (XML)-defined labeling configuration that mixes input components (Image, Audio, Text, Video, Time Series) with output components (Choices, Labels, Rectangle, Polygon, Brush, Audio Region) to specify any annotation task. Annotations live in a Postgres or SQLite backend; a Python Software Development Kit (SDK) supports import / export. The ML backend interface lets researchers wrap a pretrained model (CLIP, GroundingDINO, Whisper) so it generates pre-annotations that human reviewers correct, dramatically reducing labeling cost. Apache-2.0 license; a commercial Enterprise edition adds team management.

## Relevance to AGI

Label Studio is the most plausible front-end for AGI's manual review workflow. AGI annotations produced by automated tools (CLIP-derived scene tags, Whisper transcripts, GroundingDINO bounding boxes) can be pushed into Label Studio as pre-annotations; human contributors review and correct them; corrected annotations export back to BIDS events.tsv with HED tags. The XML labeling configuration also lets AGI define a single shared template for, say, "naturalistic image annotation" that every AGI repository can reuse. The ML backend interface aligns naturally with CrowdAgent-style multi-source workflows.

## Notable details

- XML labeling configuration combines input components and output components.
- ML backend protocol allows model pre-annotation and active learning.
- Python SDK for batch operations; REST API for programmatic access.
- Storage backends: file system, S3, Google Cloud Storage, Azure Blob.
- Apache-2.0 community edition; commercial Enterprise edition available.

## Open questions / limitations

- No native HED tagging; would require custom validation hook.
- Self-hosting at scale needs operational expertise (Postgres tuning, storage management).
- Default UI is general-purpose; cinematic or eye-tracking-specific tasks need custom configurations.
- Versioning of annotations is project-internal; integration with Git plus DataLad needs export step.
- Inter-rater reliability statistics are not first-class; users compute them externally.

## Citations

Primary: `labelstudio2020`. Related:
- `wittenburg2006elan`, domain-specific peer for hierarchical multi-tier annotation.
- `friard2016boris`, peer event-logging tool.
- `datavyu2014`, research-focused peer video-coding tool.
- `qin2025crowdagent`, multi-agent system that complements Label Studio's manual layer.
- `mcnamara2017pliers`, automated annotator that can feed Label Studio pre-annotations.
