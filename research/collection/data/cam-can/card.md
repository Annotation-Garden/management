---
slug: cam-can
type: dataset
strand: data
year: 2014
authors: [Shafto, Tyler, Dixon, Taylor, Rowe, Cusack, Calder, Marslen-Wilson, Duncan, Dalgleish, Henson, Brayne, Matthews]
venue: BMC Neurology
doi: 10.1186/s12883-014-0204-1
url: https://www.cam-can.org/
license: data-use-agreement (Cambridge Centre for Ageing and Neuroscience); paper CC-BY 4.0
modalities: [fmri-3t, mri-anat, dti, meg, eeg, behavior, phenotyping]
tags: [cognitive-task, lifespan, aging, multimodal, n=700, ages-18-88, multi-task]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Cambridge Centre for Ageing and Neuroscience (Cam-CAN) lifespan dataset: 700 adults aged 18 to 88 with structural / diffusion / resting / task functional Magnetic Resonance Imaging (fMRI), magnetoencephalography (MEG), and a deep cognitive battery, designed to study healthy ageing.

## Summary

Shafto et al. (2014) describe the Cam-CAN protocol and Stage 2 release: a 700-participant lifespan cohort sampled in 10-year age bins from 18 to 88 years. The protocol covers structural T1-weighted (T1w) / T2-weighted (T2w) magnetic resonance imaging (MRI), diffusion tensor imaging (DTI), magnetic resonance spectroscopy (MRS), resting-state fMRI, two task fMRI paradigms (sensorimotor and emotional faces), magnetoencephalography (MEG) with 306 channels, and an extensive cognitive / behavioral battery. The dataset has anchored a substantial body of work on age-related changes in functional connectivity, white-matter microstructure, and cognitive control. Cam-CAN is among the few naturalistic-meets-task lifespan datasets.

## Relevance to Annotation Garden Initiative (AGI)

Cam-CAN is a canonical reference for cognitive-task data across the adult lifespan. Its task event structure (sensorimotor task, emotional faces task) is simple enough to be HED-tagged in a few dozen lines of sidecar JavaScript Object Notation (JSON) but valuable enough that AGI hosting becomes the de facto standard. The dataset's integration of MEG, fMRI, and behaviour also makes it a useful test case for cross-modal annotation propagation.

## Notable details

- 700 participants in Stage 2 release; subsets in Stage 3 (e.g., 280 with full multimodal coverage).
- Age range 18 to 88; balanced across 10-year bins.
- Multimodal: structural, diffusion, MRS, resting-state fMRI, task fMRI (two tasks), MEG.
- Cognitive battery: Cattell fluid intelligence, story recall, n-back, picture priming, etc.
- BIDS-compatible re-release via Cambridge Brain Imaging Repository.
- License: paper CC-BY 4.0; data via DUA.

## Open questions / limitations

- Predominantly White British sample; cultural / ethnic generalization untested.
- Naturalistic stimuli are minimal in original protocol (the "movie watching" extensions came later in Cam-CAN Stage 3 and FACED).

## Citations

- Primary: `Shafto2014TheCC`.
- Related: HCP Aging (Bookheimer 2019); UK Biobank Imaging (Miller 2016); Cam-CAN Stage 3 and FACED extensions.
