---
slug: nsd-fmri
type: dataset
strand: data
year: 2022
authors: [Allen, St-Yves, Wu, Breedlove, Prince, Dowdle, Nau, Caron, Pestilli, Charest, Hutchinson, Naselaris, Kay]
venue: Nature Neuroscience
doi: 10.1038/s41593-021-00962-x
url: https://naturalscenesdataset.org/
license: CC-BY-4.0 (data); paper paywalled (Nature Neuroscience)
modalities: [fmri-7t, behavior]
tags: [naturalistic-images, coco, deep-sampling, encoding-models, adults, n=8, ventral-stream]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

Deep 7T functional Magnetic Resonance Imaging (fMRI) of 8 adults viewing roughly 10,000 distinct natural scenes drawn from Microsoft Common Objects in Context (COCO), with 30 to 40 sessions per participant. The benchmark for image-driven neural encoding and decoding.

## Summary

The Natural Scenes Dataset (NSD) is the canonical "deep sampling" naturalistic image dataset. Allen et al. collected whole-brain, 1.8-mm isotropic, 1.6-second sampling-rate Blood Oxygen Level Dependent (BOLD) responses from 8 healthy adult subjects across 30 to 40 scan sessions per subject. Stimuli were 73,000 COCO images (each subject saw a unique 9,000- to 10,000-image subset, plus a shared 1,000-image subset for cross-subject analyses). Participants performed a continuous recognition memory task. The dataset includes the GLMsingle-derived single-trial beta estimates, plus pre-computed regions of interest (ROIs), pRF (population receptive field) localizers, and category localizers (faces, bodies, places, words). NSD has become the dominant benchmark for image-to-brain encoding (deep convolutional neural networks, vision transformers) and decoding (MindEye, Brain Diffuser, and so on).

## Relevance to Annotation Garden Initiative (AGI)

NSD is the flagship visual-stimulus dataset that AGI must support end-to-end. Each of the roughly 70,000 unique COCO images is a candidate annotation target: COCO already provides bounding boxes, segmentation masks, and free-form captions, but visual saliency maps, semantic-feature embeddings, scene categories, and per-object Hierarchical Event Descriptor (HED) tags are still partially or completely missing. Stim-Brain Imaging Data Structure (BIDS, Brain Extension Proposal 044, BEP044) compatibility allows a single AGI repository to point at the 73k images and accumulate community annotation layers. The paired NSD-iEEG (Huang 2024) and NSD-EEG / Natural Object Dataset (NOD) extensions make NSD the cross-modal anchor for visual-system Garden contributions.

## Notable details

- 8 subjects, 30 to 40 sessions of 7T fMRI each. Total roughly 213,000 trials, with images repeated 1 to 3 times.
- Stimuli: 73,000 COCO images. 9,000 unique per subject + 1,000 shared subset.
- Continuous recognition task (button press: "have you seen this image before?") to maintain attention.
- Beta weights estimated with GLMsingle (Prince 2022): hemodynamic response function (HRF) optimization, GLMdenoise, fractional ridge regression. Test-retest reliability roughly 2x to 3x standard general linear model (GLM).
- Includes Functional Localizer Task (fLoc) for category-selective ROIs, prfStim for retinotopic mapping.
- License: data CC-BY 4.0; access requires registration on naturalscenesdataset.org.

## Open questions / limitations

- Only 8 subjects, all young adults; limited generalization to development, aging, or clinical populations.
- COCO images are crowd-curated; biased toward Western object/scene distributions.
- Single-trial beta estimation, while improved, still has substantial noise; many encoding-model results require averaging or denoising.
- Annotations are primarily image-level; pixel-level / region-level / semantic-tag metadata curation is fragmented across community projects.

## Citations

- Primary: `Allen2021AM7` (NSD descriptor)
- Related: GLMsingle (Prince 2022, 10.7554/eLife.77599); NSD-iEEG (Huang 2024, jov.arvojournals.org/article.aspx?articleid=2801527); MindEye (Scotti 2023, NeurIPS); BOLD5000 (Chang 2019); THINGS-fMRI (Hebart 2023).
