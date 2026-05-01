---
slug: jiang2024-labram
type: paper
strand: science
year: 2024
authors: [Jiang, Zhao, Lu]
venue: ICLR / arXiv
doi: 10.48550/arXiv.2405.18765
url: https://arxiv.org/abs/2405.18765
license: arXiv preprint
modalities: [eeg]
tags: [foundation-model, eeg, masked-modeling, neural-tokenizer, transformer, theme-5]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Large Brain Model (LaBraM): a unified Electroencephalogram (EEG) foundation model trained on ~2,500 hours from ~20 datasets via masked-channel-patch reconstruction with a vector-quantized neural tokenizer; up to ~370M parameters and state-of-the-art on multiple downstream BCI tasks at ICLR 2024.

## Summary

LaBraM is one of the first scaled EEG foundation models. Jiang and colleagues address the **heterogeneity problem** (varying channel counts, sampling rates, durations across datasets) by segmenting raw EEG into per-channel time patches and using a vector-quantized neural tokenizer (predicting Fourier spectrum codes) to produce a discrete vocabulary. A neural Transformer is then pre-trained with masked patch prediction on the full corpus. Three model sizes (5.8M, 46M, 369M) are released. Downstream evaluations on abnormal-EEG detection, event-type classification, emotion recognition, and gait prediction show LaBraM outperforms task-specific baselines. The paper also contains a small data-scaling study showing performance plateaus around ~2k hours for the 369M model; an early "annotation-response" curve for EEG foundation models.

## Relevance to AGI

EEG foundation models are the **annotation-supervised analytical engine** for the FAIR commons: when AGI hosts thousands of subjects watching shared stimuli (HBN, future commons cohorts), pre-trained EEG models can map BOLD-style annotations onto EEG. LaBraM's specific innovation; the channel-patch tokenization; is critical for handling AGI's heterogeneous EEG datasets (different caps, vendors). Foundation-model-derived per-trial embeddings are themselves a candidate annotation layer for BIDS / HED commons.

## Notable details

- ~2,500 hours of EEG, ~20 public datasets
- Architecture: per-channel time patches + spatial-temporal embeddings + Transformer
- Vector-quantized neural tokenizer pre-training with Fourier-spectrum prediction
- Sizes: 5.8M / 46M / 369M parameters
- Beats task-specific baselines on TUAB, TUEV, SEED-V, TUSL, FACED downstream tasks
- Code at https://github.com/935963004/LaBraM

## Open questions / limitations

- Training data is dominated by clinical EEG (TUH series); naturalistic, task-rich EEG (HBN movies, NSD-EEG) is under-represented.
- Downstream tasks are mostly classification benchmarks; **encoding-style** (continuous prediction of stimulus features) evaluations are absent.
- No HED / BIDS event integration: the model treats EEG as raw channels, not as annotation-aware time series.
- Cross-population (developmental, clinical) generalization not benchmarked.
- Annotation-response curves not characterized: how does fine-tuning data scale with downstream task difficulty?
- Whether LaBraM features beat hand-engineered baselines (Riemann manifold, CSP, FBCSP) on motor-imagery decoding remains contested (Xiong 2025 critique).
- Doesn't release per-stimulus embeddings for canonical commons stimuli (HBN movies, etc.); a Phase-2 AGI deliverable.
- Model card / data card formality is light; license and data-provenance for downstream re-use need formalizing.
- Cross-modality (EEG ↔ fMRI ↔ iEEG via shared stimulus) not addressed.

## Citations

Primary BibTeX key: `jiang2024labram`

Related works:
- Han et al. 2025 (DIVER-1); larger EEG/iEEG foundation model
- Wang et al. 2024 (BIOT); biosignal foundation model
- Cui et al. 2024 (Brant); BCI foundation model
- Yang et al. 2024 (EEGPT); EEG-specific generative pretraining
- Xiong et al. 2025; critical review of EEG foundation models
