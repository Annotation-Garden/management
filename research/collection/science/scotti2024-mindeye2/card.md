---
slug: scotti2024-mindeye2
type: paper
strand: science
year: 2024
authors: [Scotti, Tripathy, Villanueva, Kneeland, Chen, Narang, Santhirasegaran, Chen, Norman, Abraham]
venue: ICML / arXiv
doi: 10.48550/arXiv.2403.11207
url: https://arxiv.org/abs/2403.11207
license: arXiv (CC-BY-equivalent)
modalities: [fmri]
tags: [decoding, image-reconstruction, cross-subject, nsd, clip, diffusion, theme-2]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Cross-subject visual-image reconstruction from fMRI on Natural Scenes Dataset (NSD): a single shared-backbone model fine-tuned per subject with as little as **one hour** of new data matches state-of-the-art per-subject decoders.

## Summary

MindEye2 is a follow-up to MindEye that solves the cross-subject generalization problem in fMRI-to-image reconstruction. The architecture pretrains a backbone on 7 NSD subjects and then adapts to a held-out subject via a small number of trainable subject-specific layers. With only ~1 hour of new fMRI data, MindEye2 reaches the reconstruction quality previously requiring tens of hours per subject. The pipeline maps voxel patterns to Contrastive Language-Image Pretraining (CLIP) embeddings, then uses a fine-tuned Stable Diffusion XL Unet to generate images. Outputs include both pixel reconstructions and CLIP-based retrieval metrics. The paper is the clearest demonstration that **shared-subject pretraining + per-subject light fine-tuning** is the right pattern for naturalistic-stimulus decoding.

## Relevance to AGI

A FAIR commons of shared annotated stimuli is exactly the precondition that makes shared-subject pretraining work. AGI provides the commons; MindEye2-style decoders provide the downstream science. The paper's "1 hour to a working decoder" result is precisely what makes annotation-driven analytics tractable for clinical or developmental populations; populations where deep per-subject sampling is infeasible. AGI's mission to lower the per-stimulus annotation cost via foundation-model assistance (HED-MCP, Vision-Language Models for caption-grade annotations) directly enables this analytic regime.

## Notable details

- Trained on NSD: 7 subjects × ~30,000 trials each
- Held-out subject adapts with 150 (1 hour), 1500 (10 hours), or full data
- Features: CLIP image embeddings + Stable Diffusion XL Unet for image generation
- Achieves ~1-hour adaptation parity with full per-subject baselines on most retrieval metrics
- Open-source code; weights public on HuggingFace
- Establishes the prior-art ceiling for NSD reconstruction as of 2024

## Open questions / limitations

- NSD is static images only; cross-subject pretraining for video/narrative stimuli is open.
- COCO-derived stimuli; whether the cross-subject adapter generalizes to non-COCO image distributions (artwork, abstract, faces-only) is untested.
- Subject-specific layers are still required; "zero-shot" decoding (no new subject data) is unsolved.
- Reconstruction quality is high on object/scene content but degrades for fine details and out-of-distribution semantics.
- Model card / data card formality (annotations, licensing, demographic coverage) is sparse; exactly the area AGI's FAIR commons would standardize.
- Doesn't compare to **annotation-conditioned** decoders that use HED tags or per-image semantic graphs as auxiliary supervision.
- Privacy implications of cross-subject decoders are not addressed; consent frameworks for sharing brain-image-decoder weights are not yet community-standard.
- Whether multimodal pretraining (image + text + audio) further reduces per-subject cost is open.

## Citations

Primary BibTeX key: `scotti2024mindeye2`

Related works:
- Scotti et al. 2023 (MindEye 1); single-subject precursor
- Takagi & Nishimoto 2023; Stable Diffusion fMRI reconstruction
- Allen et al. 2022; NSD dataset
- Lahner et al. 2025 (MOSAIC); multi-dataset aggregation extending the cross-subject idea
- Ozcelik & VanRullen 2023; alternative diffusion-based reconstruction
