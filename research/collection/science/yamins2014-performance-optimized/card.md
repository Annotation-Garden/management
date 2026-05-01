---
slug: yamins2014-performance-optimized
type: paper
strand: science
year: 2014
authors: [Yamins, Hong, Cadieu, Solomon, Seibert, DiCarlo]
venue: PNAS
doi: 10.1073/pnas.1403112111
url: https://doi.org/10.1073/pnas.1403112111
license: publisher-paywall
modalities: [fmri, electrophysiology]
tags: [encoding-model, deep-neural-network, ventral-stream, dnn-brain-alignment, object-recognition, theme-1]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

Performance-optimized hierarchical convolutional networks predict neural responses in inferior temporal (IT) cortex better than any prior model; establishing the "task-driven Deep Neural Network (DNN) as a model of the ventral stream" paradigm.

## Summary

Yamins and colleagues trained convolutional neural networks (CNNs) to perform object recognition on natural images and showed that intermediate layers of high-performing networks predict neural firing rates in macaque IT cortex with unprecedented accuracy. They establish a quantitative correspondence (the "brain score" idea before the term existed): networks that perform better on object recognition produce intermediate features that align better with IT neurons. Critically, the alignment is hierarchical: V4-like areas align with earlier CNN layers, IT with later layers. The result is foundational for using DNNs as feature spaces in encoding models, and it underwrites the entire current literature on DNN-brain alignment (Khaligh-Razavi & Kriegeskorte 2014, Schrimpf et al. 2018, Conwell 2024).

## Relevance to AGI

Foundation-model annotation supervision (Theme 5) inherits its theoretical justification from this paper: a model trained on a relevant task acquires representations that match brain activity, so its embeddings can serve as annotations for new stimuli. AGI's vision of using vision-language models (VLMs) to annotate stimuli is a direct extension. The paper also implicitly argues for **task diversity** in pre-training: if AGI wants commons-grade VLM annotations for neural prediction, the choice of pre-training task matters as much as scale.

## Notable details

- 296 IT neurons recorded in macaques during passive viewing of object images
- Networks: hierarchical models (HMO, HMAX-style) optimized via supervised classification
- Quantitative metric: linear-regression prediction of single neurons from network features
- Better-performing networks → better neural prediction (the "scaling-law" intuition before scaling laws)
- Established the now-canonical V1→V4→IT mapping to CNN layers

## Open questions / limitations

- Macaque single-unit data, not human Magnetic Resonance Imaging (MRI); generalization to human ventral stream took years of follow-up.
- Object-recognition task is narrow; later work shows other tasks (depth, texture) yield comparable alignment, weakening the "tightly task-specific" claim.
- Pre-Vision Transformer; how much of the alignment is architectural (convolution) vs. task is unclear and was eventually addressed by Conwell 2024 and others.
- No naturalistic-video extension here; the framework is feed-forward and ignores temporal dynamics that VideoMAE-class models target.
- Annotation-as-feature is implicit: the network's class labels are *the* annotation, but they are not exposed to the user as portable, machine-readable tags.
- Doesn't address how brain alignment scales with **dataset diversity** of pre-training (an open question for foundation-model annotation pipelines).
- Pre-deep-learning baselines are weak; the actual variance-explained gap to a well-tuned biologically inspired baseline (Gabor + sparse coding) was contested in subsequent work.

## Citations

Primary BibTeX key: `yamins2014performance`

Related works:
- Khaligh-Razavi & Kriegeskorte 2014; concurrent representational similarity analysis (RSA) demonstration of CNN-IT alignment
- Schrimpf et al. 2018; Brain-Score benchmarking framework
- Conwell et al. 2024; large-scale follow-up on Natural Scenes Dataset showing inductive biases matter
- Kell et al. 2018; auditory analog of this paper
- Cichy et al. 2016; DNN alignment with human Magnetoencephalography (MEG) dynamics
