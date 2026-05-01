---
slug: hbn-eeg
type: dataset
strand: data
year: 2024
authors: [Shirazi, Truong, Saliasi, Zou, Robbins, Delorme, Cockx, Tudor, Chen, Cheng, Makeig]
venue: bioRxiv (Scientific Data revision in progress)
doi: 10.1101/2024.10.03.615261
url: https://neuromechanist.github.io/data/hbn/
license: CC-BY-4.0 (paper); data Creative Commons / Brain Imaging Data Structure (BIDS) deposit
modalities: [eeg, behavior]
tags: [naturalistic-video, despicable-me, hbn-movies, hed-tagged, developmental, n>3000, ages-5-21]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

The Findable, Accessible, Interoperable, and Reusable (FAIR) re-release of the Healthy Brain Network (HBN) high-density electroencephalography (EEG) data: more than 3,000 children and adolescents aged 5 to 21, watching Despicable Me, The Present, Pixar shorts, plus six cognitive task paradigms, all annotated with Hierarchical Event Descriptors (HED).

## Summary

Shirazi et al. (2024) describe the HBN-EEG release: a Brain Imaging Data Structure (BIDS)-formatted, HED-tagged version of the EEG data collected by the Child Mind Institute Healthy Brain Network. The dataset spans more than 3,000 participants aged 5 to 21 with deep psychiatric phenotyping. The EEG protocol includes movie viewing (Despicable Me 10-minute clip; The Present 3.5-minute animated short; Diary of a Wimpy Kid Trailer; Fun with Fractals) and structured cognitive tasks (Resting State with eyes-open / eyes-closed, Surround Suppression, Contrast Change Detection, Symbol Search, Sequence Learning, Video-Decision-Making). Each task event is described with HED tags spanning sensory presentation, cognitive operation, motor response, and stimulus features. The release is the largest pediatric EEG dataset with naturalistic stimuli and the first large-scale HED Generation 3 deployment.

## Relevance to Annotation Garden Initiative (AGI)

HBN-EEG is the proof-of-concept that motivates AGI: a single richly annotated stimulus set (Despicable Me, The Present, etc.) shared across thousands of participants, with HED metadata that lets contributors run mega-analyses. AGI inherits the annotation infrastructure (HED schema, BIDS sidecar templates, pointer architecture for copyright-restricted movies) directly from this release. The HBN-EEG cognitive task subset is also a primary entry point into the cognitive-task end of the naturalistic-to-controlled spectrum.

## Notable details

- N > 3,000 participants, ages 5 to 21, 11 release batches (R1 through R11).
- Stimuli: Despicable Me (10-min clip), The Present (3.5-min), Diary of a Wimpy Kid Trailer, Fun with Fractals (custom psychometric paradigm).
- Tasks: Resting State, Surround Suppression, Contrast Change Detection, Symbol Search Test, Sequence Learning, Video Decision Making.
- 128-channel BioSemi EEG (some ages with EGI nets).
- Brain Imaging Data Structure (BIDS) deposit on OpenNeuro (ds005505 through ds005514+).
- Hierarchical Event Descriptor (HED) Generation 3 sidecars throughout.
- License: data Creative Commons (per HBN consent); descriptor paper bioRxiv preprint.

## Open questions / limitations

- Movies (Despicable Me, The Present) are copyright; HBN distributes only stimulus pointers and timing.
- HED annotations target events, not continuous frame-level features; complementary frame-level layers (saliency, character identity) need to be community-contributed.
- Phenotyping data has a separate access agreement.

## Citations

- Primary: `Shirazi2024HBNEEG` (bioRxiv 10.1101/2024.10.03.615261).
- Related: HBN-MRI (Alexander 2017, `hbn-mri/`); Movies in the Magnet (Vanderwal 2019); HED Generation 3 (Robbins 2024).
