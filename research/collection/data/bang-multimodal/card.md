---
slug: bang-multimodal
type: dataset
strand: data
year: 2024
authors: [Aly, Tsao, Rey, Reber, Adolphs, Rutishauser]
venue: OpenNeuro / Scientific Data
doi: null
url: https://openneuro.org/datasets/ds004798
license: data-use-agreement (Cedars-Sinai / Caltech IRB) plus CC0 metadata
modalities: [ieeg, single-unit, fmri-3t, behavior]
tags: [naturalistic-video, hitchcock, bang-youre-dead, single-neuron, hippocampus, amygdala, event-cells, n=29, epilepsy-patients]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: not-available
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

OpenNeuro ds004798: simultaneous single-neuron, intracranial EEG (iEEG), and 3 Tesla functional Magnetic Resonance Imaging (fMRI) from 29 epilepsy patients while watching an 8-minute Alfred Hitchcock clip, with rich movie annotations including event boundaries, faces, and characters.

## Summary

Aly, Reber, Adolphs, Rutishauser and collaborators (Cedars-Sinai / Caltech) released OpenNeuro deposit ds004798 to extend the Berezutskaya et al. Bang! You're Dead corpus with single-neuron data. The dataset includes 29 patients with microwire (Behnke-Fried) electrodes implanted in mesial temporal lobe (amygdala, hippocampus, entorhinal, parahippocampal cortex) plus broader iEEG coverage and a 3T fMRI cohort. Subjects watched an 8-minute clip from the Alfred Hitchcock Presents episode Bang! You're Dead while neural activity at three spatial scales was recorded. The deposit ships with movie annotations (faces, locations, semantic events) and behavioural ratings. It has anchored seminal work on hippocampal "event cells" responding to narrative boundaries (Zheng 2022 Nature Neuroscience).

## Relevance to Annotation Garden Initiative (AGI)

ds004798 demonstrates the upper bound of multimodal naturalistic neuroscience: a single 8-minute clip yielding three complementary neural readouts plus rich behavioural data. AGI's pointer-architecture annotations on the clip can drive analyses across all three modalities and across both ds003688 and ds004798. The dataset's "event cell" findings depend on accurate event-boundary annotation, exactly the kind of layer the Garden hosts.

## Notable details

- 29 epilepsy patients with single-unit recordings (Behnke-Fried microwires) plus iEEG and fMRI cohorts.
- Stimulus: 8-minute clip from Bang! You're Dead.
- Stimulus annotations included: shot boundaries, face appearances, character identity, location changes, narrative event-boundary ratings (continuous human ratings).
- Companion FigShare release (Zheng et al., 25037045) adds detailed manual annotations of cuts, faces, characters, locations.
- License: data-use-agreement plus CC0 metadata; no formal descriptor paper at retrieval (analysis paper Zheng 2022).

## Open questions / limitations

- No standalone Scientific Data descriptor; reliant on the OpenNeuro deposit README.
- Patient sample heterogeneous in electrode placement.
- Movie clip is copyright; requires DUA.

## Citations

- Primary: `OpenNeuroDs004798` (deposit).
- Related: Zheng et al. 2022 Nature Neuroscience event cells; Berezutskaya 2022 (`bang-ieeg-fmri/`); studyforrest (`studyforrest/`).
