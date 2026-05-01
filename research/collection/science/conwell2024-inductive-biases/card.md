---
slug: conwell2024-inductive-biases
type: paper
strand: science
year: 2024
authors: [Conwell, Prince, Kay, Alvarez, Konkle]
venue: Nature Communications
doi: 10.1038/s41467-024-53147-y
url: https://www.nature.com/articles/s41467-024-53147-y
license: CC-BY
modalities: [fmri]
tags: [encoding-model, deep-neural-network, nsd, vision-transformer, inductive-bias, ventral-stream, theme-1]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Massive Natural Scenes Dataset (NSD)-based comparison (~1.8 billion regressions over hundreds of pre-trained vision models) showing that **neither task, nor architecture, nor diet, nor scale alone** drives high-level visual cortex prediction; instead, every dimension contributes a modest amount and saturating performance has been reached.

## Summary

Conwell and colleagues benchmark hundreds of pre-trained vision models (Convolutional Neural Networks (CNNs), Vision Transformers (ViTs), self-supervised, contrastive, image-text) as feature spaces for voxel-wise encoding models on NSD. Across model "diet" (training data), task, architecture, and parameter count, they find that high-level visual cortex prediction is remarkably *insensitive* to any single design axis: many models reach a similar ceiling. The paper argues that the field has hit a soft plateau on the standard benchmarks and that incremental architectural changes no longer translate into prediction gains. They also document a small but consistent advantage for image-text contrastive models (Contrastive Language-Image Pretraining (CLIP)-style) in regions of higher-level cortex, hinting that semantic alignment with language helps. The work is the most rigorous "inductive-bias is overrated" statement in the encoding literature.

## Relevance to AGI

If feature-space choice has hit a ceiling on existing data, the bottleneck shifts to **annotation diversity and stimulus design**, which is exactly AGI's mission. The paper's modest CLIP-edge for higher-cortex regions also reinforces AGI's foundation-model annotation strategy: models trained on richer multimodal annotations may be the next variance source. Cards based on this work make the case that AGI's commons (broader stimulus set, richer multilayer annotations) is a more promising path than larger pre-trained models alone.

## Notable details

- ~1.8 billion encoding-model fits across NSD × model × layer × subject
- Models: hundreds of pre-trained ImageNet, CLIP, DINO, Masked Autoencoder (MAE), and language-augmented vision models
- Best models explain ~70-75% of explainable variance in higher visual cortex but only marginally beat strong baselines
- ViTs and CNNs tie on average; transformer-specific advantages disappear under matched data
- CLIP-style multimodal models gain a small edge in higher-level regions
- Authors release model-banks to enable community re-use

## Open questions / limitations

- Plateau may be specific to NSD's static-image, COCO-derived stimuli; whether dynamic, narrative, multimodal stimuli reveal new inductive-bias differences is open.
- Single 1.8-second TR fMRI obscures fast temporal dynamics where architectural differences may matter (e.g., recurrence).
- "Diet" axis treats datasets as labels; doesn't analyze what *features* of training data correlate with brain prediction (an annotation-side question AGI could answer).
- Predictions saturate at noise ceiling for many subjects' voxels; without higher signal-to-noise data, model differences are buried in noise.
- Doesn't test whether **annotation-conditioned** training (e.g., HED-grounded captions) yields different behavior from generic web captions.
- Cross-stimulus generalization (NSD-trained models tested on Forrest Gump, HBN movies) is not addressed; AGI's federation tests will need to fill this in.
- Subject-specific encoders dominate; whether a single shared model + alignment matches subject-level fits is unresolved.

## Citations

Primary BibTeX key: `conwell2024large`

Related works:
- Yamins et al. 2014; origin of task-optimized DNN-brain matching paradigm
- Schrimpf et al. 2018; Brain-Score, the benchmark Conwell critiques implicitly
- Allen et al. 2022; NSD dataset paper
- Wang et al. 2025 (Nat Mach Intel); high-level visual cortex aligned with Large Language Models (LLMs)
- Khosla & Williams 2023; what makes a good visual cortex model
