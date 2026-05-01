---
slug: pliers
type: tool
strand: tools
year: 2017
authors: [McNamara, "de la Vega", Yarkoni]
venue: KDD 2017
doi: 10.1145/3097983.3098075
url: https://github.com/PsychoinformaticsLab/pliers
license: BSD-3-Clause
modalities: [image, audio, video, text, multimodal]
tags: [Pliers, feature-extraction, orchestration, multimodal, pipeline, Neuroscout, BIDS]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

Pliers is a Python framework that wraps heterogeneous feature extractors (CLIP, OpenCV, librosa, Whisper, language models, cloud Application Programming Interfaces (APIs)) behind a unified Stim plus Extractor abstraction, letting researchers compose multimodal pipelines that produce time-aligned feature tables.

## Summary

The 2017 KDD paper introduces Pliers as a solution to the "feature extraction tax" in naturalistic neuroscience: every paper hand-rolls an ad hoc pipeline to convert video into faces, audio into envelopes, and text into sentiment scores. Pliers standardizes that pipeline. Stims represent input media; Extractors wrap a single feature-producing tool; Filters and Converters move data between modalities (frame sampling, audio extraction from video). The output ExtractorResult is a pandas DataFrame of features over time, ready to feed into BIDS events.tsv columns or directly into General Linear Model (GLM) regressors. Pliers is the backbone of Neuroscout's automated annotation database, and is widely used in studyforrest-style and naturalistic-fMRI work.

## Relevance to AGI

Pliers is the closest existing implementation of AGI's automated-annotator orchestration layer. AGI repositories that use foundation models (CLIP for scene tags, Whisper for speech, GroundingDINO for object localization) should structure their pipelines as Pliers Extractors so they interoperate with Neuroscout, can be cached, and inherit a reproducibility model with provenance metadata. Where Pliers stops short (multi-agent quality control, HED tag mapping), AGI extends it. The Pliers + Neuroscout pairing is also the most concrete blueprint for what AGI's analysis side could look like.

## Notable details

- Stim hierarchy: ImageStim, AudioStim, VideoStim, TextStim, ComplexTextStim, plus Iterators.
- Extractor wrappers for OpenCV, librosa, spaCy, NLTK, Google Vision, Microsoft Cognitive, transformers.
- Cached intermediate outputs to avoid recomputation.
- ExtractorResult emits pandas DataFrames with timestamp columns.
- BSD-3-Clause license; pip-installable.

## Open questions / limitations

- Cloud Application Programming Interface (API) keys required for some extractors.
- HED-tag emission is not native; users post-process Pliers DataFrames.
- Pipeline composition is Python-only; no GUI for non-programmers.
- Performance on long videos limited by single-process design without parallel orchestration.
- Recent foundation models (LLaVA-Video, Qwen-Omni) need new Extractor wrappers.

## Citations

Primary: `mcnamara2017pliers`. Related:
- `delavega2022neuroscout`, primary platform built on top of Pliers.
- `radford2021clip`, foundation model commonly wrapped as a Pliers extractor.
- `radford2023whisper`, speech model commonly wrapped as a Pliers extractor.
- `liu2024groundingdino`, open-set detector that fits the Pliers extractor pattern.
- `qin2025crowdagent`, multi-agent layer that complements Pliers's static extraction.
