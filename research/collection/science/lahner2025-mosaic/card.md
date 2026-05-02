---
slug: lahner2025-mosaic
type: paper
strand: science
year: 2025
authors: [Lahner, et al.]
venue: bioRxiv
doi: 10.1101/2025.11.28.690060
url: https://www.biorxiv.org/content/10.1101/2025.11.28.690060v1
license: bioRxiv preprint (CC-BY/NC depending)
modalities: [fmri]
tags: [foundation-model, fmri, multi-dataset, generalization, encoding, theme-5]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

MOSAIC: a scalable framework that aggregates 8 fMRI datasets (~93 subjects, mostly NSD-like visual paradigms) into a shared cortical surface space and trains generalizable encoding models that predict held-out subjects without per-subject fitting.

## Summary

Lahner and colleagues attack the "every dataset trains its own model" problem in fMRI vision research. They aggregate 8 datasets covering ~93 subjects watching images and short videos, project all subjects to a common cortical surface (fsaverage), and train a single encoding model. The aggregated model generalizes across datasets and predicts new subjects competitively with per-subject models, demonstrating that data aggregation can substitute for some of the per-subject deep sampling that NSD (8 subjects, 30+ sessions each) used. The paper extends the MindEye2 cross-subject lesson into a many-dataset, many-paradigm regime and supplies open-source pipelines, surface alignments, and pre-trained models.

## Relevance to AGI

MOSAIC is the empirical proof-of-concept of AGI's federation thesis: if many labs share canonical stimuli on a shared annotation backbone, aggregate models train better than any single dataset's model. AGI's commons + Brain Imaging Data Structure (BIDS) + HED scaffolding is the *generalization* of MOSAIC: shared stimuli and standardized event annotations across labs and paradigms, not just within a vision-encoding niche. AGI's vision-language-model annotations (caption-grade descriptions) can also be evaluated as feature spaces in the MOSAIC paradigm.

## Notable details

- 8 fMRI datasets, 93 subjects total
- Common surface space (fsaverage); per-subject linear adapters
- Encoding models trained on aggregated data; tested on held-out subjects
- Stimulus features include CLIP image embeddings and CLIP-text embeddings
- Open-source code, models, and pre-aligned subject data
- Demonstrates scaling-law-like behavior with aggregated data

## Open questions / limitations

- Visual-encoding focus; doesn't aggregate auditory/language/narrative paradigms.
- Common surface space loses subcortical structures critical for event/memory annotation work.
- Linear per-subject adapters; non-linear or low-rank adapters may improve.
- 93 subjects is small relative to HBN-scale (>5000); how the approach scales is unknown.
- Stimulus annotation is implicit in CLIP features; explicit HED-tagged annotations not yet integrated.
- Cross-modality (fMRI ↔ EEG ↔ MEG via shared stimulus) is not addressed.
- Does not characterize annotation-response curves: how much benefit per added dataset/subject?
- The aggregation pipeline's preprocessing decisions are not factorized; replicability across acquisition vendors needs documentation.
- Privacy/consent for cross-dataset model release is handled informally; AGI commons would need a formal opt-in framework.

## Citations

Primary BibTeX key: `lahner2025mosaic`

Related works:
- Allen et al. 2022; NSD foundational dataset
- Scotti et al. 2024 (MindEye2); within-NSD cross-subject
- Hebart et al. 2023 (THINGS-data); multimodal large-scale benchmark
- Conwell et al. 2024; model-bank benchmarking on NSD
- Prince et al. 2022 (GLMsingle); preprocessing tooling MOSAIC builds on
