---
slug: glmsingle-paper
type: paper
strand: data
year: 2022
authors: [Prince, Charest, Kurzawski, Pyles, Tarr, Kay]
venue: eLife
doi: 10.7554/eLife.77599
url: https://glmsingle.readthedocs.io/
license: CC-BY-4.0
modalities: [fmri, methods]
tags: [single-stimulus-benchmark, methods, single-trial-betas, fractional-ridge, hrf-optimization, glmdenoise]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

GLMsingle: a Python and MATLAB toolbox for accurate single-trial Blood Oxygen Level Dependent (BOLD) response estimation, combining hemodynamic response function (HRF) optimization, GLMdenoise, and fractional ridge regression. The recommended pipeline for naturalistic-stimulus and rapid-event-related fMRI.

## Summary

Prince and colleagues (University of Minnesota / Carnegie Mellon / Glasgow) released GLMsingle in 2022 as the canonical method for single-trial fMRI beta estimation. The toolbox combines three innovations: (1) per-voxel HRF library matching from a pre-fit catalogue, (2) GLMdenoise data-driven noise regressors derived from task-unrelated voxels, and (3) fractional ridge regression for variance-stabilizing single-trial weights. Validation against the Natural Scenes Dataset and BOLD5000 shows 2x to 3x increases in test-retest reliability of single-trial betas compared to standard general linear model (GLM). GLMsingle has rapidly become the reference pipeline for image-to-brain encoding studies.

## Relevance to Annotation Garden Initiative (AGI)

GLMsingle is the methods anchor for stimulus-by-stimulus annotation analyses on naturalistic image datasets. Without GLMsingle (or equivalent), per-stimulus annotations cannot be tied to per-trial brain responses with sufficient signal-to-noise to be useful. AGI Garden contributors building image-level annotation layers should expect downstream users to apply GLMsingle; AGI hosting of GLMsingle-derived betas alongside community annotation layers is a high-value pattern.

## Notable details

- Open Python and MATLAB implementations.
- Validated on NSD (8 subjects, ~40 sessions each) and BOLD5000 (4 subjects).
- Improvements: 2x to 3x test-retest reliability, comparable to averaging over 4 trial repetitions.
- Now a default option in fmriprep BIDS-derivatives.
- License: paper CC-BY 4.0; toolbox MIT.

## Open questions / limitations

- Tuned for slow event-related designs; less optimal for blocks.
- Computationally expensive at high TR.

## Citations

- Primary: `Prince2022ImprovingTA`.
- Related: NSD-fMRI (`nsd-fmri/`); BOLD5000 (`bold5000/`); standard GLM (Friston 1995).
