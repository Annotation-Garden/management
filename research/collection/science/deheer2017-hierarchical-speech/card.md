---
slug: deheer2017-hierarchical-speech
type: paper
strand: science
year: 2017
authors: [de Heer, Huth, Griffiths, Gallant, Theunissen]
venue: Journal of Neuroscience
doi: 10.1523/JNEUROSCI.3267-16.2017
url: https://www.jneurosci.org/content/37/27/6539
license: publisher-paywall
modalities: [fmri]
tags: [encoding-model, variance-partitioning, hierarchical-speech, multi-perspective, theme-7]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

Variance-partitioning encoding study using *three* hierarchical feature spaces; spectral, articulatory, and semantic; fit to the same fMRI data, revealing a cortical hierarchy where each feature level uniquely predicts a distinct cortical zone.

## Summary

de Heer and colleagues recorded fMRI from subjects listening to natural narratives and built three voxel-wise encoding models: (1) low-level spectral features (cochleagram), (2) mid-level articulatory features (phoneme distinctive features), (3) high-level semantic features (lexical co-occurrence). They fit each model alone, then together, and partitioned variance across the three feature spaces. Each feature level uniquely predicts a distinct cortical band: early auditory cortex by spectral features, lateral superior temporal gyrus by articulatory features, and a distributed semantic network by semantic features. The paper is the canonical multi-perspective encoding study and the methodological template for any analysis where multiple annotation layers compete for variance.

## Relevance to AGI

Multi-perspective encoding is exactly the use-case AGI's multilayer HED annotations enable. With multiple machine-actionable annotation layers (visual cuts, dialogue, semantic content, character actions, social interactions) on a shared stimulus, every lab can run de Heer-style variance partitioning and identify which annotation layer best explains each cortical region. The paper's variance-partitioning protocol; easily integrated with any HED-tagged stimulus in the AGI commons; is the experimental backbone of Phase 2 synthesis.

## Notable details

- 6 subjects, ~3 hours of "Moth" stories during fMRI
- Feature spaces: spectral (cochleagram), articulatory (phoneme distinctive features), semantic (985-d word co-occurrence)
- Encoding model: voxel-wise ridge regression with hemodynamic-response convolution
- Variance partitioning via separate and joint model fits
- Spectral / articulatory / semantic each predicts a distinct cortical zone

## Open questions / limitations

- 3 feature spaces; modern multi-perspective analysis would also include syntactic, social, emotional layers.
- 6 subjects, narrow demographic; cross-population generalization untested.
- Auditory only; whether the same partitioning logic applies to vision (multi-perspective movie annotation) was an inspiration for later studies but not directly tested.
- Doesn't address how variance partitioning scales with annotation richness; Theme 6 sufficiency.
- Pre-foundation-model: doesn't compare LLM contextual embeddings to lexical co-occurrence.
- Doesn't directly use HED tagging or any portable annotation standard.
- Cross-modality generalization (does the same hierarchy emerge in EEG-listening encoding?) is open.
- Cross-language/cross-cultural validation would test universality of the hierarchy.

## Citations

Primary BibTeX key: `deheer2017hierarchical`

Related works:
- Huth et al. 2016; semantic atlas based on the same encoding paradigm
- Mesgarani et al. 2014; phonemic encoding in superior temporal gyrus
- Holdgraf et al. 2017; predictive features in continuous speech
- Norman-Haignere et al. 2015; auditory cortex spectro-temporal hierarchy
- Antonello et al. 2023; modern LLM-feature scaling on related data
