---
slug: cichy2014-resolving-object-recognition
type: paper
strand: science
year: 2014
authors: [Cichy, Pantazis, Oliva]
venue: Nature Neuroscience
doi: 10.1038/nn.3635
url: https://www.nature.com/articles/nn.3635
license: publisher-paywall
modalities: [meg, fmri]
tags: [meg-fmri-fusion, rsa, object-recognition, cross-modal, theme-7]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

Foundational MEG-fMRI fusion study using Representational Similarity Analysis (RSA) on 92 object images: combining the millisecond temporal resolution of MEG with the millimeter spatial resolution of fMRI yields a spatiotemporal map of object processing that neither modality alone provides.

## Summary

Cichy and colleagues recorded MEG and fMRI from human subjects viewing the same 92 object images. Within each modality, they computed pairwise representational dissimilarity matrices (RDMs) per time point (MEG) or per region (fMRI). They then correlated the time-resolved MEG RDMs with the region-resolved fMRI RDMs to produce a fusion map: when does each fMRI region's representation emerge in time? The result reveals a temporal cascade from V1 (~80 ms) through ventral stream regions to inferotemporal cortex (~150-300 ms). The paper formalizes MEG-fMRI fusion via RSA and is the foundation of subsequent cross-modal naturalistic studies (Cichy 2016 with DNNs, Hebart 2023 THINGS multimodal).

## Relevance to AGI

Cross-modal RSA requires **shared stimuli** with **shared annotations**; exactly AGI's commons. The 92-image set in this paper has been re-used dozens of times across labs because of stimulus identity. AGI's commons would extend this to thousands of images (NSD, THINGS) and dynamic stimuli (Forrest Gump, HBN movies), enabling MEG-fMRI fusion at a scale impossible today. AGI's HED-annotated stimuli also enable **annotation-conditioned RSA**: RDMs computed from annotations rather than brain activity become the cross-modal alignment basis.

## Notable details

- 92 object images (a dataset that became a community standard)
- 16 subjects in MEG, 15 in fMRI (subset overlap)
- Temporal cascade: V1 ~80 ms → V4 ~150 ms → IT ~200-300 ms
- Methodology: RSA fusion via correlation of RDMs across modalities and time
- Released stimuli + RDMs publicly

## Open questions / limitations

- Static images only; dynamic-stimulus MEG-fMRI fusion is more complex (event-aligned vs. continuous).
- 92 stimuli is small; statistical power for fine timing dissociations is limited.
- Doesn't integrate annotation layers; RDMs are built from low-level features or category labels.
- Single subject group; cross-subject MEG-fMRI alignment was a later concern (Hebart 2023).
- Pre-deep-learning; integrating CNN/ViT-derived RDMs came in Cichy 2016.
- Doesn't address how annotation richness affects cross-modal alignment quality.
- Cross-population (developmental, clinical) not addressed.
- Same-subject MEG and fMRI on the same stimuli was rare at the time; THINGS-data (Hebart 2023) finally provides this at scale.

## Citations

Primary BibTeX key: `cichy2014resolving`

Related works:
- Cichy et al. 2016; DNN comparison via the same MEG-fMRI fusion
- Hebart et al. 2023 (THINGS-data); multimodal benchmark scaling cross-modal RSA
- Kriegeskorte et al. 2008; RSA framework foundation
- Cichy et al. 2017; DNN-MEG-fMRI integration
- Khaligh-Razavi & Kriegeskorte 2014; DNN-RSA in fMRI
