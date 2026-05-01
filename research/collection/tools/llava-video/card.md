---
slug: llava-video
type: tool
strand: tools
year: 2024
authors: [Zhang, Wu, Li, Li, Ma, Liu, Li]
venue: arXiv preprint arXiv:2410.02713 (TMLR 2025)
doi: 10.48550/arXiv.2410.02713
url: https://arxiv.org/abs/2410.02713
license: Apache-2.0 (model and code)
modalities: [video, text]
tags: [video-LLM, instruction-tuning, captioning, video-QA, multimodal, open-source, dense-frame-sampling]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

LLaVA-Video is a video Large Multimodal Model (LMM) trained on LLaVA-Video-178K, a 178,510-clip synthetic instruction-following dataset built with GPT-4o that emphasizes dynamic, untrimmed video and dense frame sampling.

## Summary

The authors argue that existing video instruction-tuning datasets are too static and too coarsely sampled, leading to hallucinations on detailed temporal queries. They construct LLaVA-Video-178K by surveying ten major existing video sources, filtering for dynamic untrimmed clips (5 to 180 seconds), and generating captions through a recurrent three-level pipeline (10-second, mid-range, full-video) at one frame per second. They then generate 1.3M instruction samples spanning detailed captions, open-ended question-answering (QA), and 16 categories of multiple-choice QA. The LLaVA-Video model itself uses a SlowFast token allocation that lets it consume up to three times more frames than uniform-token baselines, and achieves strong results across video benchmarks. The dataset, generation pipeline, and checkpoints are released openly.

## Relevance to AGI

For AGI's video stimulus repositories (Forrest Gump, Despicable Me, The Present, Pixar shorts), a model that generates detailed timestamped captions for untrimmed clips is the missing piece between raw video and HED-tagged events.tsv. LLaVA-Video's recurrent caption pipeline maps naturally onto AGI's needs: produce dense per-second captions, then post-process them into HED tags, scene boundaries, or character-presence flags via lightweight rule-based or LLM-based extractors. The 178K-clip synthetic dataset itself is also a candidate "tool dataset" that AGI could index for reuse by labs without resources to query GPT-4o directly.

## Notable details

- 178,510 videos, 1.3M instruction samples, 16 question categories.
- One frame per second sampling rate; recurrent three-level captioning pipeline.
- SlowFast token allocation to fit more frames in fixed GPU memory.
- Source video pool drawn from ten datasets covering activities, cooking, TV, egocentric, etc.
- Code, dataset, checkpoints, and demo released; built on the LLaVA codebase.

## Open questions / limitations

- Synthetic data inherits GPT-4o biases and hallucinations.
- Underlying video sources have diverse and sometimes unclear licenses; downstream redistribution needs care.
- Dense-frame sampling raises compute cost; deployment at AGI repository scale needs caching.
- No first-class temporal grounding output (start/end timestamps) without prompt engineering.
- Model performance varies sharply across video genres; performance on cinematic features is not separately benchmarked.

## Citations

Primary: `zhang2024llavavideo`. Related:
- `radford2021clip`, visual encoder feeding into LLaVA-style models.
- `radford2023whisper`, companion speech model for audio tracks.
- `liu2024groundingdino`, frame-level grounding to complement clip-level captions.
- `castellano2014pyscenedetect`, preprocessor for shot boundaries before captioning.
- `delavega2022neuroscout`, downstream consumer that could ingest LLaVA-Video features.
