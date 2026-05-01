---
slug: naspi2021-perceptual-semantic
type: paper
strand: science
year: 2021
authors: [Naspi, Hoffman, Devereux, Morcom]
venue: Journal of Neuroscience
doi: 10.1523/JNEUROSCI.0677-21.2021
url: https://www.jneurosci.org/content/41/41/8676
license: author-accepted-manuscript
modalities: [fmri]
tags: [memory-encoding, granularity, perceptual-features, semantic-features, ventral-temporal, theme-6]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Encoding-model fMRI study showing that **fine-grained perceptual and semantic features** drive true-recognition memory in ventral temporal cortex, while coarse taxonomic features predict subsequent forgetting; a direct empirical link between annotation granularity and memory outcomes.

## Summary

Naspi and colleagues had subjects encode object images during fMRI and tested recognition memory afterwards. They built encoding models with three feature spaces: low-level perceptual (image-derived), fine-grained semantic (specific properties from feature norms), and coarse taxonomic (Living/Non-living, etc.). At encoding, fine-grained perceptual and semantic features predicted later **true recognition** in fusiform gyrus and posterior ventral temporal cortex. Coarse taxonomic features predicted **forgetting / lure-related false alarms** in anterior temporal lobe and inferior frontal gyrus. This is one of the cleanest demonstrations that **annotation granularity matters**: coarse labels are not just less informative, they are *behaviorally* associated with weaker memories.

## Relevance to AGI

This paper is the empirical anchor for AGI's "annotation richness > annotation quantity" thesis. If memory and cortical processing dissociate by annotation granularity, then the value of multilayer fine-grained HED annotations on commons stimuli is directly testable: subjects who view stimuli with rich annotations available should show different downstream cortical and behavioral patterns when those annotations align with stimulus features. AGI's commons can host the annotation-granularity-controlled experiments that this paper hints at but cannot run alone.

## Notable details

- 27 healthy adults, fMRI during incidental encoding
- 3 feature spaces: perceptual (HMAX-derived), fine semantic (McRae feature norms), coarse taxonomic
- Behavioral measure: recognition memory with similar lures (true recognition vs. false alarm)
- Region-level dissociation of granularity: fusiform/pVTC for fine features, ATL/IFG for coarse
- Voxel-wise encoding methodology

## Open questions / limitations

- Discrete object stimuli only; whether the granularity dissociation holds for naturalistic narratives is open.
- 27 subjects, single session; cross-population (developmental, clinical) replication needed.
- Fine semantic features come from a single feature-norm corpus; alternative feature spaces (BERT, CLIP) would test robustness.
- Doesn't directly compare HED-tagged annotation layers; AGI's HED-LANG could extend this paradigm.
- Doesn't quantify how memory performance scales with annotation depth (a direct sufficiency curve experiment).
- Single modality (fMRI); whether MEG or EEG would show the same granularity dissociation is unknown.
- Doesn't address how multi-rater consensus (vs. single-rater) annotation affects the encoding-memory link.
- Cross-stimulus generalization within the same subject not tested.

## Citations

Primary BibTeX key: `naspi2021perceptual`

Related works:
- Devereux et al. 2018; feature-norm-based encoding
- Cooper et al. 2017; event memory and feature integration
- Martin et al. 2018; Anterior Temporal Lobe and conceptual hubs
- Clarke & Tyler 2014; graded category specificity in vision
- Naspi et al. 2024; extension to event memory
