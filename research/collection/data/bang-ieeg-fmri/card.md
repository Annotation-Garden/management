---
slug: bang-ieeg-fmri
type: dataset
strand: data
year: 2022
authors: [Berezutskaya, Vansteensel, Aarnoutse, Freudenburg, Piantoni, Branco, Ramsey]
venue: Scientific Data
doi: 10.1038/s41597-022-01173-0
url: https://openneuro.org/datasets/ds003688
license: CC0 (deposit)
modalities: [ieeg, fmri-3t, behavior]
tags: [naturalistic-video, hitchcock, bang-youre-dead, multimodal, epilepsy-patients, n=51, scene-boundaries]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

An open multimodal intracranial EEG (iEEG) plus 3 Tesla functional Magnetic Resonance Imaging (fMRI) dataset from 51 epilepsy patients viewing a 7-minute clip of Alfred Hitchcock's Bang! You're Dead, with movie annotations of shot boundaries, faces, speech, and event structure.

## Summary

Berezutskaya and colleagues (UMC Utrecht / Donders Institute) released OpenNeuro deposit ds003688: simultaneous (per-modality) iEEG and fMRI recordings during passive viewing of a 7-minute audiovisual clip from the Alfred Hitchcock Presents television episode Bang! You're Dead. The dataset includes 51 patients (iEEG, with various electrode coverage) and 30 healthy adults (fMRI) viewing the same stimulus. Movie annotations cover shot cuts, face appearances, character speech onsets, scene-boundary markers, and "suspense" peaks. The dataset is a flagship example of multi-modal naturalistic neuroscience: identical stimulus, complementary spatiotemporal coverage, and rich event annotation.

## Relevance to Annotation Garden Initiative (AGI)

Bang! is the canonical short-clip benchmark for cross-modal naturalistic encoding. AGI's pointer-architecture annotation model fits this dataset perfectly: the clip itself sits behind a license at OpenNeuro, while AGI can host enriched, community-curated annotation layers (HED-tagged scene boundaries, character emotion, gaze priority, semantic novelty). Berezutskaya et al. already provide a baseline annotation set in the deposit; AGI extends it.

## Notable details

- 51 epilepsy patients with iEEG; 30 healthy adults with 3T fMRI.
- Stimulus: 7-minute clip from Bang! You're Dead (Alfred Hitchcock Presents, 1961).
- Brain Imaging Data Structure (BIDS)-compliant; OpenNeuro ds003688 (iEEG + fMRI; current version 1.0.6).
- Companion deposit ds004798 adds single-unit and additional iEEG recordings (Aly et al.; see `bang-multimodal/`).
- Movie annotations (in deposit): shot boundary timestamps, face appearances, speech onsets, scene-boundary candidates.
- License: CC0 (deposit metadata) plus stimulus-specific terms.

## Open questions / limitations

- Patient sample is heterogeneous (electrode coverage varies dramatically).
- Annotation set in the deposit is moderate; deeper layers (continuous suspense, character cognition, gaze priority) are not provided.
- Stimulus is short (7 minutes) compared to feature-length naturalistic studies.

## Citations

- Primary: `Berezutskaya2022OpenMI`.
- Related: ds004798 multimodal Bang! (`bang-multimodal/`); studyforrest (`studyforrest/`); Naturalistic Neuroimaging Database (Aliko 2020).
