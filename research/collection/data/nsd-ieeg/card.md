---
slug: nsd-ieeg
type: dataset
strand: data
year: 2024
authors: [Huang, Magnotti, Tandon]
venue: Vision Sciences Society / Journal of Vision
doi: null
url: https://jov.arvojournals.org/article.aspx?articleid=2801527
license: data-use-agreement (Texas Medical Center / patient consent)
modalities: [ieeg, behavior]
tags: [naturalistic-images, nsd, intracranial, broadband-gamma, epilepsy-patients, n=12, ventral-stream]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: not-available
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

Intracranial electroencephalography (iEEG) recorded from 12 epilepsy patients viewing a 1,000-image subset of the Natural Scenes Dataset (NSD), enabling millisecond-resolution dynamics of broadband gamma activity (BGA) co-registered with fMRI Blood Oxygen Level Dependent (BOLD) responses to the same stimuli.

## Summary

Huang and colleagues (Tandon Lab, McGovern Medical School / University of Texas Health Science Center) extended NSD to invasive electrophysiology by recording iEEG from 12 patients undergoing surgical evaluation for epilepsy while they viewed 1,000 NSD images selected from the shared NSD subset. The recordings sample the ventral visual stream (lateral occipital, fusiform, parahippocampal, anterior temporal) plus prefrontal regions in some patients. Broadband gamma activity (70 to 150 Hz envelope) is the primary feature; the dataset enables direct comparison between high-resolution functional Magnetic Resonance Imaging (fMRI) Blood Oxygen Level Dependent (BOLD) topography and millisecond-resolution neural dynamics on identical stimuli. Initial analyses identify event-selective electrodes responding to specific semantic categories (faces, food, etc.).

## Relevance to Annotation Garden Initiative (AGI)

NSD-iEEG is a "Rosetta Stone" complement to NSD-fMRI: the same 1,000 stimuli, two modalities, complementary spatiotemporal precision. AGI's Stim-BIDS image annotations on NSD therefore propagate trivially to this dataset, and the Garden becomes the natural place to host shared annotation layers that researchers across modalities can pull from. Patient consent constraints mean the raw iEEG is not openly redistributable, but Brain Imaging Data Structure (BIDS) sidecars and stimulus annotations are.

## Notable details

- 12 patients (variable electrode coverage); typical 100 to 200 channels per patient, including stereo-EEG (sEEG) depth electrodes.
- 1,000 NSD images, presented 2 to 3 times each.
- Sampling rate 1024 Hz or 2048 Hz; broadband gamma envelope (70 to 150 Hz) standard analytic feature.
- Reported in Huang et al., Vision Sciences Society 2024 abstract; full descriptor in preparation.

## Open questions / limitations

- Patient sample limits generalizability and electrode coverage is heterogeneous.
- Not yet on OpenNeuro or DABI (Data Archive for the Brain Initiative); access requires institutional agreement.
- No companion paper indexed by Crossref at retrieval; primary source is the conference abstract.

## Citations

- Primary: Huang et al. (2024) Journal of Vision abstract. ID: `Huang2024NsdIeeg`.
- Related: NSD-fMRI (Allen 2022); Hamilton 2018 ECoG/EEG/fMRI on natural movies; Berezutskaya 2022 multimodal Brain (Bang!) iEEG-fMRI.
