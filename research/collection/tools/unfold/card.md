---
slug: unfold
type: tool
strand: tools
year: 2019
authors: [Ehinger, Dimigen]
venue: PeerJ
doi: 10.7717/peerj.7838
url: https://www.unfoldtoolbox.org
license: GPL-3.0
modalities: [eeg]
tags: [Unfold, regression-ERP, deconvolution, GAM, naturalistic, EEGLAB, overlap-correction]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Unfold is an EEGLAB-compatible MATLAB toolbox that combines massive-univariate regression Event-Related Potentials (regression ERPs), linear deconvolution to correct overlap from closely spaced events, and Generalized Additive Models (GAMs) for non-linear covariate effects.

## Summary

Naturalistic Electroencephalography (EEG) experiments (eye-tracking-coregistered reading, mobile brain-body imaging, multisensory paradigms) have unavoidable overlap between adjacent neural responses. The 2019 PeerJ paper documents Unfold, which models the continuous EEG as a sum of overlapping kernels, recovers per-event regression-ERP weights via a linear deconvolution design matrix, and supports non-linear covariates via spline basis functions in a GAM framework. Unfold integrates with EEGLAB datasets and event structures, supports temporal basis functions (Fourier sets, splines), and handles regularization. The toolbox has become the standard for analyzing fixation-related potentials and naturalistic-stimulus ERPs.

## Relevance to AGI

For AGI's naturalistic stimuli (Forrest Gump auditory EEG, HBN-EEG passive viewing, free-viewing image experiments), responses to closely spaced events overlap and confound conventional epoch-based analyses. Unfold is the right deconvolution layer between AGI's annotation-derived event timelines and the EEG response. Concretely, AGI's per-frame HED tags or CLIP-derived continuous predictors become regressors in Unfold's design matrix, and the toolbox returns clean per-tag waveforms with overlap removed. The MATLAB-EEGLAB pairing also makes Unfold the natural pre-print companion when AGI-tagged datasets are reanalyzed in classical ERP-style outputs.

## Notable details

- Linear deconvolution with FIR or basis-function design matrices.
- Non-linear covariates via Generalized Additive Models (splines, Fourier sets).
- Tikhonov / ridge regularization for ill-conditioned designs.
- Integrates with EEGLAB EEG.event structures; reads BIDS-EEG indirectly via EEGLAB-BIDS.
- Companion Python port (unfold.jl in Julia, plus pymer4-style implementations) under development.

## Open questions / limitations

- Single-subject; group-level inference must be assembled in downstream tools.
- Ill-conditioned designs (highly correlated regressors) need careful regularization choice.
- Memory grows with design-matrix length; very long continuous recordings need chunking.
- No native HED-aware regressor builder; users hand-build design matrices.
- Limited support for non-linear interactions beyond pairwise GAM smooths.

## Citations

Primary: `ehinger2019unfold`. Related:
- `delorme2004eeglab` — host environment.
- `gramfort2013mne` — Python alternative for similar analyses.
- `crosse2016mtrf` — companion regression toolbox for continuous stimuli.
- `prince2022glmsingle` — fMRI analogue for single-trial estimation.
- `delavega2022neuroscout` — fMRI-side platform with overlapping ambition.
