---
slug: whisper
type: tool
strand: tools
year: 2023
authors: [Radford, Kim, Xu, Brockman, McLeavey, Sutskever]
venue: ICML 2023
doi: 10.48550/arXiv.2212.04356
url: https://github.com/openai/whisper
license: MIT
modalities: [audio]
tags: [speech-recognition, ASR, multilingual, transcription, alignment, weak-supervision, OpenAI]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Whisper is a multilingual, multitask Automatic Speech Recognition (ASR) model trained on 680,000 hours of weakly supervised internet audio and released under MIT license, achieving strong zero-shot performance across languages and accents without dataset-specific fine-tuning.

## Summary

The Whisper paper argues that prior ASR research over-relied on small, high-quality, English-only labeled datasets while leaving the much larger pool of weakly supervised internet audio underused. The authors collect 680,000 hours of audio paired with internet transcripts, including 117,000 hours across 96 non-English languages and 125,000 hours of speech-translation pairs. They train an encoder-decoder Transformer that performs transcription, translation, language identification, and voice activity detection through a joint multitask interface. The released model checkpoints (tiny through large-v3) are MIT-licensed and have spawned downstream ecosystems including WhisperX (forced alignment), faster-whisper (CTranslate2), and Distil-Whisper (compressed models).

## Relevance to AGI

For AGI's audio-bearing stimuli (Forrest Gump dialog, HBN movies, podcast-style auditory tasks, Pixar shorts), Whisper provides timestamped transcription as the foundation layer for any subsequent linguistic annotation (phonemes via Praat, semantic surprisal via language models, scene-level themes). WhisperX's forced alignment yields word-level timestamps that fit directly into BIDS events.tsv as one row per word, with HED tags layered on top. Whisper is therefore the speech analogue of CLIP for AGI: a near-zero-cost first pass that turns raw stimulus media into an annotation skeleton.

## Notable details

- 680,000 hours of training audio, including 117k non-English and 125k translation hours.
- Encoder-decoder Transformer; checkpoints: tiny, base, small, medium, large, large-v2, large-v3.
- Mel spectrogram input at 16 kHz, 25 ms windows, 10 ms stride.
- Multitask: transcription, translation, language ID, voice activity detection.
- Downstream ecosystem: WhisperX, faster-whisper, Distil-Whisper, whisper.cpp.

## Open questions / limitations

- Hallucinated transcriptions on long silences or noisy audio.
- Performance gap remains for low-resource languages and code-switching speech.
- No native speaker diarization; requires external tools.
- Word-level timestamps come from external alignment, not from Whisper itself.
- Training data is not redistributable; reproductions rely on alternative datasets.

## Citations

Primary: `radford2023whisper`. Related:
- `radford2021clip` — companion vision-language model.
- `crosse2016mtrf` — uses speech envelope features that Whisper output can produce.
- `boersma2024praat` — phonetic annotation tool that consumes Whisper transcripts.
- `mcnamara2017pliers` — orchestration tool that wraps Whisper.
- `delavega2022neuroscout` — analysis platform that ingests Whisper-derived predictors.
