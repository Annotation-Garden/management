---
slug: xiong2025-eegfm-review
type: paper
strand: science
year: 2025
authors: [Xiong, et al.]
venue: arXiv
doi: 10.48550/arXiv.2507.11783
url: https://arxiv.org/abs/2507.11783
license: arXiv preprint
modalities: [eeg]
tags: [foundation-model, eeg, critical-review, baselines, theme-5, sufficiency]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Critical systematic review showing that EEG foundation models often fail to outperform classical, hand-engineered baselines (Riemannian geometry, Common Spatial Pattern (CSP), Filter Bank CSP) on downstream tasks like motor imagery; challenging the "scale solves everything" narrative.

## Summary

Xiong and colleagues conduct a careful comparative evaluation of recent EEG foundation models (LaBraM, BIOT, BENDR, NeuroGPT, EEGPT) against well-tuned classical baselines on a battery of standard Brain-Computer Interface (BCI) downstream tasks. The headline finding: across multiple datasets and tasks (motor imagery, P300, sleep staging), foundation models often **match but do not consistently exceed** Riemannian-geometry classifiers and similar low-parameter approaches. They argue that the EEG heterogeneity problem (variable montages, vendor-specific artifacts, individual differences) does not yield to scale alone. The review proposes an evaluation protocol (matched compute, matched fine-tuning data, multiple seeds) and recommends task-specific benchmarks plus careful baselines. The paper is the most rigorous "is the bet paying off?" critique of EEG foundation models to date.

## Relevance to AGI

Xiong's findings reframe AGI's value proposition: if scale alone doesn't solve EEG, then **shared canonical stimuli with rich annotations** (AGI's commons) become the primary axis of progress. Foundation models pre-trained on AGI-curated corpora with annotation supervision should outperform raw-signal-only foundation models on annotation-driven tasks. The review's evaluation protocol can be adopted as the standard for benchmarking annotation-conditioned vs. unconditioned EEG models.

## Notable details

- arXiv preprint review (multiple revisions through 2025)
- Compares LaBraM, BIOT, BENDR, NeuroGPT, EEGPT, Brant
- Baselines: Common Spatial Pattern, Riemannian-geometry classifiers, hand-engineered ConvNets
- Downstream tasks: motor imagery (BCI Competition IV), P300, sleep staging, emotion recognition
- Key finding: no foundation model is dominant across all benchmarks
- Calls for protocol standardization

## Open questions / limitations

- Doesn't evaluate on naturalistic-stimulus tasks (encoding-style annotation prediction); the authors acknowledge this as future work.
- Foundation models tested were not pre-trained with annotation supervision (a possibly missing ingredient).
- Compute-budget matching is approximate; some baselines are over-optimized for specific datasets.
- HBN-style large naturalistic EEG corpora are absent from the evaluation suite.
- Doesn't quantify how *fine-tuning data* scales (the key sufficiency curve for downstream practitioners).
- Cross-modality (EEG ↔ fMRI) generalization isn't part of the benchmark.
- Doesn't propose a positive program: what kind of annotation supervision would shift the conclusion?
- Limited treatment of clinical / patient-specific generalization.

## Citations

Primary BibTeX key: `xiong2025eegfm`

Related works:
- Jiang et al. 2024 (LaBraM); central object of critique
- Han et al. 2025 (DIVER-1); newer scaled model that the review predates
- Aristimunha et al. 2025; NeurIPS EEG Foundation Challenge benchmarking
- Lahner et al. 2025 (MOSAIC); analogous "scale + share" approach in fMRI
- Goldberger et al. 2000 (PhysioNet); seminal community-benchmark paradigm
