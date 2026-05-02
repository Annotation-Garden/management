---
slug: localizer-ds000114
type: dataset
strand: data
year: 2017
authors: [Papadopoulos Orfanos, Michel, Pinel, Rivière, Joliot, Operto, Pinel, Dehaene, Le Bihan, Thirion, Poline, Varoquaux]
venue: Scientific Data
doi: 10.1038/sdata.2017.110
url: https://openneuro.org/datasets/ds000114
license: CC-BY-4.0 (paper); CC0 (deposit)
modalities: [fmri, behavior]
tags: [single-stimulus-benchmark, multi-task-localizer, large-cohort, n=1311, brainomics, pinel-localizer, openneuro]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Brainomics Localizer dataset: 1,311 healthy adults completing the Pinel multi-task localizer (Pinel 2007), forming the largest open functional Magnetic Resonance Imaging (fMRI) localizer cohort and the canonical benchmark for cross-subject reliability of localizer activations.

## Summary

Papadopoulos Orfanos and colleagues (NeuroSpin / Inria / EuroFranco) released the Brainomics Localizer dataset (OpenNeuro ds000114) as the largest public sample of the Pinel multi-task localizer protocol. 1,311 adult participants completed the 5-minute paradigm spanning 10 elementary cognitive operations (visual / auditory / motor / calculation / language). The dataset includes raw and pre-processed fMRI, behavioural performance metrics, demographic information, and Statistical Parametric Mapping (SPM) contrast maps per subject. The descriptor paper (Pinel et al. 2017 Scientific Data via Brainomics) provides quality control statistics and harmonization details.

## Relevance to Annotation Garden Initiative (AGI)

This deposit is the cleanest "single-stimulus benchmark" reference cohort: hundreds to thousands of subjects on the same short paradigm, BIDS-formatted, openly licensed. AGI hosting of canonical HED Generation 3 sidecars on this dataset establishes a reference annotation layer that all downstream Pinel-localizer applications can inherit.

## Notable details

- N = 1,311 adults from EuroFranco / Brainomics consortium.
- 5-minute Pinel multi-task localizer (visual horizontal/vertical, motor left/right, auditory sentence, visual sentence, auditory calculation, visual calculation).
- BIDS deposit: OpenNeuro ds000114.
- License: paper CC-BY 4.0; deposit CC0.

## Open questions / limitations

- Original recruitment is European adult; demographic homogeneity.
- Stimulus presentation in French (with translations).

## Citations

- Primary: `PapadopoulosOrfanos2017TheBL`.
- Related: Pinel localizer (`pinel-localizer/`); Individual Brain Charting Pinel 2017; HCP Task (`hcp-task/`).
