---
slug: glmsingle
type: tool
strand: tools
year: 2022
authors: [Prince, Charest, Kurzawski, Pyles, Tarr, Kay]
venue: eLife
doi: 10.7554/eLife.77599
url: https://elifesciences.org/articles/77599
license: CC-BY-4.0
modalities: [fmri]
tags: [GLM, single-trial, HRF, ridge-regression, fMRI, NSD, BOLD5000, naturalistic]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

GLMsingle is a MATLAB and Python toolbox that improves single-trial functional Magnetic Resonance Imaging (fMRI) Blood-Oxygen-Level-Dependent (BOLD) response estimates by combining voxel-specific Hemodynamic Response Function (HRF) selection, cross-validated noise regressors, and ridge regression.

## Summary

Condition-rich fMRI experiments such as Natural Scenes Dataset (NSD), BOLD5000, and Things present thousands of unique stimuli with few repetitions, making per-trial signal-to-noise ratio (SNR) the limiting factor. GLMsingle takes raw fMRI time series plus a design matrix and applies three sequential improvements: per-voxel HRF picked from a 20-function library, GLMdenoise-style noise regressors derived from voxels unrelated to the experiment via cross-validation, and ridge regression with voxel-wise regularization to stabilize betas for closely spaced trials. Applied to NSD and BOLD5000, GLMsingle substantially improves cross-trial reliability across visually responsive cortex, decorrelates nearby trials, increases between-subject representational similarity, and boosts one-versus-many decoding accuracy. The tool is open source at glmsingle.org.

## Relevance to AGI

GLMsingle is the canonical analysis bridge between AGI stimulus annotations and the per-trial BOLD responses they explain. For NSD, AGI annotations such as HED scene tags or CLIP embeddings become regressors that GLMsingle output betas can be regressed against in encoding models. The "single-trial beta per stimulus" output is exactly the data format AGI repositories should aim to enable: one annotation row per events.tsv onset, paired with one beta per voxel. GLMsingle thereby anchors AGI's value proposition for fMRI: better annotations directly translate into better encoding-model fits when paired with high-SNR single-trial estimates.

## Notable details

- Three-stage pipeline: HRF library, GLMdenoise noise regressors, ridge regularization.
- Released in MATLAB and Python; identical interface and outputs.
- Validated on NSD, BOLD5000, and a smaller StudyForrest auditory dataset.
- Reports per-voxel reliability gains of 30-100 percent depending on dataset.
- Outputs include voxel-wise HRF index, betas, noise pool, and reliability maps.

## Open questions / limitations

- Assumes fixed canonical timing per session; not designed for fully event-asynchronous designs.
- Computational cost of ridge cross-validation scales with voxel count.
- Does not address physiological noise correction directly; expects that to come from fMRIPrep.
- Single-trial betas are noisier than block-design betas, which affects univariate inference.
- HRF library is pooled across cortex; true per-region HRF variability may need extension.

## Citations

Primary: `prince2022glmsingle`. Related:
- `esteban2019fmriprep` — upstream preprocessing pipeline.
- `delavega2022neuroscout` — alternative analysis platform that consumes GLMsingle outputs.
- `gorgolewski2016bids` — input format expected by the toolbox.
- `markiewicz2021openneuro` — datasets where GLMsingle is most often applied.
- `radford2021clip` — typical source of per-stimulus regressors used downstream.
