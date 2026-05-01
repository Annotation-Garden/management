---
slug: nsd-eeg-alljoined
type: dataset
strand: data
year: 2024
authors: [Xu, Choksi, Roig, Nemrodov, Cichy]
venue: arXiv (preprint) / OpenNeuro
doi: null
url: https://openneuro.org/datasets/ds005810
license: CC0 (deposit)
modalities: [eeg, behavior]
tags: [naturalistic-images, nsd, scalp-eeg, cross-modal, adults, n=8, alljoined]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-available
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

Scalp electroencephalography (EEG) collected on 8 adults viewing the Natural Scenes Dataset (NSD) shared 1,000-image subset, providing the cross-modal scalp-EEG counterpart to NSD-fMRI and NSD-iEEG.

## Summary

Xu and colleagues (Goethe University / York University / Free University of Berlin) released "alljoined" / NSD-EEG, an 8-subject scalp EEG companion deposit to the Natural Scenes Dataset. Subjects view a subset of NSD images (typically the 1,000 shared NSD images plus an extended set) while 64- to 128-channel EEG is recorded. The dataset is intended as a low-cost, high-temporal-resolution complement to NSD-fMRI for visual-encoding research. Materials are deposited on OpenNeuro (ds005810) and described in arXiv preprints by Xu and Brotherwood et al.

## Relevance to Annotation Garden Initiative (AGI)

NSD-EEG closes the modality triangle for NSD: fMRI (Allen 2022), intracranial EEG (Huang 2024), scalp EEG (Xu 2024). Any annotation layer AGI hosts on NSD images propagates across all three datasets, making NSD the most fully cross-modal target in current naturalistic-image neuroscience. Cost barriers to scalp EEG are far lower than fMRI or iEEG, so AGI's stimulus annotation surface here has high reuse potential for non-imaging labs.

## Notable details

- 8 adult subjects.
- NSD shared 1,000 images plus extension subsets.
- 64- or 128-channel scalp EEG.
- BIDS deposit on OpenNeuro: ds005810 (alljoined) and related.
- License: CC0 (deposit).

## Open questions / limitations

- Small N relative to typical EEG (8 subjects).
- Limited descriptor publication; primary source is arXiv preprints.

## Citations

- Primary: `XuEEG2024Alljoined` (arXiv).
- Related: NSD-fMRI (`nsd-fmri/`); NSD-iEEG (`nsd-ieeg/`); NOD-EEG (`nod-eeg/`).
