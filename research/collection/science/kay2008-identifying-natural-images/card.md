---
slug: kay2008-identifying-natural-images
type: paper
strand: science
year: 2008
authors: [Kay, Naselaris, Prenger, Gallant]
venue: Nature
doi: 10.1038/nature06713
url: https://www.nature.com/articles/nature06713
license: publisher-paywall
modalities: [fmri]
tags: [decoding, encoding-model, gabor, identification, voxel-wise, theme-2]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

Foundational paper showing that an encoding model trained on Gabor-style features can identify which natural image a subject viewed from BOLD activity, picking the correct image out of 1,000 candidates with high accuracy.

## Summary

Kay and colleagues recorded fMRI from 2 subjects viewing 1,750 natural images. They built a voxel-wise encoding model with Gabor-like spatial-frequency filters and used the inverted model to identify which of 1,000 held-out images each fMRI pattern corresponded to. Identification accuracy far exceeded chance (~92% for one subject, ~72% for the other when picking from 120 images), demonstrating that the encoded representation is rich enough to disambiguate among many naturalistic stimuli. The paper anchors annotation-driven decoding: with explicit feature-space modeling, fMRI patterns carry stimulus-specific information that can be decoded back. Every subsequent decoder (semantic decoder, image reconstruction with MindEye, language decoder Tang & Huth 2023) is a descendant of this approach.

## Relevance to AGI

The "identification" framing; given a candidate set, find which stimulus produced this brain pattern; directly motivates the FAIR commons. If AGI publishes versioned annotation sets for each commons stimulus, downstream researchers can run identification on shared data and benchmark new feature spaces against canonical encoding models without re-annotating from scratch. The paper also illustrates the limits of low-level features alone: identification accuracy plateaus, motivating semantic and multi-perspective annotation layers (Theme 5, 6).

## Notable details

- 2 subjects, 1,750 training images, 120 held-out images for identification
- Gabor wavelet pyramid features per voxel
- Identification accuracy: 92% (subject 1), 72% (subject 2) on 120-image candidates
- Pre-deep learning; demonstrates that the strategy works with classical features
- Released a curated dataset (vim-1) that became a community benchmark

## Open questions / limitations

- Two subjects only; cross-subject generalization untested.
- Static low-level features (Gabor); cannot represent semantic categories explicitly.
- No annotation provenance: the "feature space" is defined operationally, not as a curated annotation layer that another lab could substitute.
- Paper does not address how identification accuracy scales with the size of the candidate set, the data used, or the diversity of categories; Theme 6 questions.
- Trials are static images; how the same approach extends to dynamic, narrative stimuli is an open extension.
- Doesn't compare to category-level decoders (semantic decoding from cortex came later).
- Identification framework presupposes the candidate set is known; open-set identification ("from any natural image") was the next big challenge, partly solved by Naselaris 2009 Bayesian reconstruction.

## Citations

Primary BibTeX key: `kay2008identifying`

Related works:
- Naselaris et al. 2009; Bayesian reconstruction extending Kay 2008 to image generation
- Nishimoto et al. 2011; natural movie reconstruction
- Huth et al. 2016; semantic-feature-space encoding (modality jump from images to language)
- Takagi & Nishimoto 2023; diffusion-model image reconstruction from fMRI (Stable Diffusion)
- Scotti et al. 2024; MindEye2 cross-subject visual reconstruction
