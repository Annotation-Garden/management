---
slug: han2025-diver1
type: paper
strand: science
year: 2025
authors: [Han, et al.]
venue: arXiv
doi: 10.48550/arXiv.2512.19097
url: https://arxiv.org/abs/2512.19097
license: arXiv preprint
modalities: [eeg, ieeg]
tags: [foundation-model, eeg, ieeg, scaling, transformer, theme-5]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

DIVER-1: a 1.82-billion-parameter Transformer trained on 5.3k hours of intracranial Electroencephalogram (iEEG) and 54k hours of scalp EEG (>1.6 million channel-hours), the largest electrophysiology foundation model to date and the first to jointly handle invasive and non-invasive recordings.

## Summary

DIVER-1 (Deep Integration of Vast Electrophysiological Recordings at Scale) pushes the EEG foundation-model agenda beyond LaBraM by combining scalp and intracranial corpora and scaling parameters and tokens by an order of magnitude. The model uses a standardized channel-patch tokenization and large-scale masked reconstruction. Downstream evaluations span sleep staging, abnormality detection, motor imagery, and event-related classification. The paper reports favorable scaling behavior (loss decreases continue with data and parameters) but acknowledges that downstream improvements are uneven; large data and large models do not uniformly translate into clinical-task gains. The paper is the most explicit empirical instance of the foundation-model promise *and limits* in electrophysiology.

## Relevance to AGI

DIVER-1 is the upper bound of the current "scale your way to a brain encoder" approach. AGI's complementary strategy; federate richly annotated stimuli and align them across modalities; could provide the *annotated supervision* DIVER-1 lacks: shared narrative stimuli with HED-tagged events would let DIVER-1 (or successors) learn embeddings that explicitly track stimulus annotations rather than only intrinsic neural statistics. AGI's commons can also serve as a benchmark suite where DIVER-1's encoder predictions for movies, narratives, or NSD images are evaluated against canonical annotations.

## Notable details

- 1.82B parameters
- 5.3k hours iEEG + 54k hours scalp EEG (>1.6M channel-hours)
- Tokenization handles variable-channel layouts and variable durations
- Demonstrates scaling-law-like loss curves
- Downstream gains are stronger on classification benchmarks than on continuous decoding
- arXiv preprint at the largest scale published to date in the field

## Open questions / limitations

- Downstream gains do not consistently exceed strong baselines (Riemann methods on motor imagery, hand-engineered features for sleep); corroborating Xiong 2025's critique.
- Pre-training data is dominated by clinical / abnormal recordings; naturalistic-stimulus EEG/iEEG is under-represented.
- No event-aware annotation supervision: model trained only on raw signal statistics.
- Cross-modality alignment (DIVER-1 EEG ↔ fMRI ↔ behavior on the same subjects) not addressed.
- Model card / data card formality limited; some training corpora have unclear redistribution rights.
- Annotation-response evaluation is absent: how does DIVER-1's downstream accuracy scale with task-specific data on top of pretraining?
- Generalization to developmental cohorts (HBN children) and clinical populations is not characterized.
- Compute and energy footprint are large; benefit-vs-cost analysis vs. simpler methods is not provided.

## Citations

Primary BibTeX key: `han2025diver`

Related works:
- Jiang et al. 2024 (LaBraM); predecessor at smaller scale
- Yang et al. 2024 (EEGPT); generative pre-training alternative
- Wang et al. 2024 (BIOT); biosignal foundation model
- Xiong et al. 2025; critical review of EEG foundation models
- Aristimunha et al. 2025 (NeurIPS EEG Challenge); community benchmarking effort
