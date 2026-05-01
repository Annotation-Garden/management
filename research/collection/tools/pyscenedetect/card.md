---
slug: pyscenedetect
type: tool
strand: tools
year: 2024
authors: [Castellano]
venue: Open-source Python package (continuous release since 2014)
doi: null
url: https://github.com/Breakthrough/PySceneDetect
license: BSD-3-Clause
modalities: [video]
tags: [PySceneDetect, scene-cut, shot-boundary, preprocessing, FFmpeg, video, HSV-difference]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-applicable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

PySceneDetect is a Python and command-line tool for automatic shot-boundary detection in video, with multiple detector strategies (content, adaptive, threshold, histogram, perceptual hash) and direct FFmpeg integration for splitting clips.

## Summary

PySceneDetect computes per-frame difference statistics (default ContentDetector uses Hue Saturation Value (HSV) deltas) and reports shot-boundary timestamps when those deltas exceed a configurable threshold. The AdaptiveDetector handles slow fades better; ThresholdDetector handles fade-to-black; HistogramDetector and HashDetector provide alternative robustness profiles. The tool emits CSV / TSV / JSON listings of shot start / end timestamps and frame indices, can split a long video into per-shot files via FFmpeg, and produces an HTML report with thumbnails. It is BSD-3-Clause and pip-installable.

## Relevance to AGI

For AGI's video stimulus repositories (Forrest Gump, Despicable Me, The Present, Pixar shorts), PySceneDetect is the natural first preprocessing step. Its output directly maps onto a BIDS events.tsv with one row per shot: onset, duration, plus optional HED tags later layered on by automated annotators (LLaVA-Video, GroundingDINO) or human reviewers. By committing the PySceneDetect parameters used (detector, threshold, version) into the AGI repository's metadata, AGI guarantees that the shot list is reproducible. PySceneDetect therefore underpins every AGI annotation that is anchored to shot boundaries.

## Notable details

- Detectors: ContentDetector, AdaptiveDetector, ThresholdDetector, HistogramDetector, HashDetector.
- Outputs CSV / TSV / JSON with timestamps and frame indices.
- FFmpeg integration for splitting per-shot clip files.
- HTML report with per-shot thumbnails.
- BSD-3-Clause; pip-installable; cross-platform.

## Open questions / limitations

- Default thresholds are tuned for typical broadcast content; documentary or animated content may need retuning.
- Soft transitions (cross-fades, dissolves) detected less reliably than hard cuts.
- Does not detect scene boundaries beyond shot level (semantic scenes spanning multiple shots).
- No native HED tagging.
- Memory usage scales with video resolution; 4K video needs sufficient resources.

## Citations

Primary: `castellano2014pyscenedetect`. Related:
- `zhang2024llavavideo`, companion video-language model for per-shot captions.
- `radford2023whisper`, speech model often run alongside PySceneDetect on movie audio.
- `mcnamara2017pliers`, orchestration tool that wraps shot detectors.
- `delavega2022neuroscout`, analysis platform that consumes shot boundaries as predictors.
- `gorgolewski2016bids`, target schema where shot lists become events.tsv rows.
