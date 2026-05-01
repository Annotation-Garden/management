---
slug: nod-eeg
type: dataset
strand: data
year: 2025
authors: [Zhang, Song, He, Cui, Du, Yu, Liu]
venue: Scientific Data
doi: 10.1038/s41597-025-05174-7
url: https://openneuro.org/datasets/ds005811
license: CC0 / CC-BY (per OpenNeuro deposit)
modalities: [eeg, meg, behavior]
tags: [naturalistic-images, things-imagenet, cross-modal, adults, n=20+, scalp-electrophysiology]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

Large-scale paired magnetoencephalography (MEG) and scalp electroencephalography (EEG) recordings while subjects view naturalistic object images drawn from the Things Initiative concept set, providing a cross-modal benchmark for object recognition dynamics.

## Summary

Zhang et al. (2025) describe a Natural Object Dataset for MEG/EEG (NOD-MEG and NOD-EEG, OpenNeuro ds005811) collected to complement the Natural Scenes Dataset (NSD) fMRI benchmark with non-invasive electrophysiology. Adult subjects viewed thousands of object images selected from the THINGS database while MEG and high-density EEG were recorded simultaneously or in matched sessions. The dataset is intended to support direct cross-modal benchmarking of object decoding accuracy and to anchor the Things-MEG and Things-EEG2 efforts within a unified release.

## Relevance to Annotation Garden Initiative (AGI)

NOD-EEG/MEG is a critical cross-modal node: it shares its concept set with the THINGS initiative, so any AGI annotation layer attached to a THINGS concept (semantic features, super-ordinate categories, image properties) propagates to all THINGS-affiliated brain datasets. This dataset closes a long-standing gap in non-invasive object-recognition coverage and is a strong test case for Stim-Brain Imaging Data Structure (BIDS, BEP044) cross-references.

## Notable details

- OpenNeuro: ds005811 (currently version 1.0.6 at retrieval).
- Subjects roughly 20 to 30 adults (final N depends on session).
- Stimuli: subset of the THINGS image database (1,854 concepts, 12+ exemplars each).
- High-density scalp EEG (e.g., 64- or 128-channel BioSemi/Neuroscan) and 306-channel Elekta MEG (where applicable).

## Open questions / limitations

- Sample size, while larger than typical MEG cohorts, remains small relative to fMRI (NSD = 8) for between-subject statistics.
- Stimulus presentation timing differs from THINGS-fMRI; cross-modal alignment requires care.
- Paywalled descriptor PDF (Scientific Data 2025) limits redistribution of the document itself.

## Citations

- Primary: `Zhang2025NodMeegEeg`.
- Related: THINGS initiative (Hebart 2023, eLife 10.7554/eLife.82580); Things-EEG2 (Gifford 2022, NeuroImage); Things-MEG (Hebart 2022); NSD-fMRI.
