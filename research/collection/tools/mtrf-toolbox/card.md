---
slug: mtrf-toolbox
type: tool
strand: tools
year: 2016
authors: [Crosse, "Di Liberto", Bednar, Lalor]
venue: Frontiers in Human Neuroscience
doi: 10.3389/fnhum.2016.00604
url: https://github.com/mickcrosse/mTRF-Toolbox
license: BSD-3-Clause
modalities: [eeg, meg]
tags: [TRF, system-identification, regression, continuous-stimuli, speech, naturalistic, encoding-model, decoding-model]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Multivariate Temporal Response Function (mTRF) Toolbox is a MATLAB package that fits regularized linear regression models mapping continuous sensory stimuli to neural responses (encoding) or vice versa (decoding), with built-in regularization tuning.

## Summary

The mTRF Toolbox treats Electroencephalography (EEG) or Magnetoencephalography (MEG) responses to continuous stimuli (speech envelope, visual motion, music) as the output of a linear time-invariant system whose impulse response is the Temporal Response Function (TRF). The 2016 paper reviews system identification history, derives ridge-regularized TRF estimation, and walks through forward (encoding) and backward (decoding) models with cross-validated lambda selection. The toolbox supports multivariate inputs, optimal-window selection, and noise-floor estimation. It became the standard tool for naturalistic-speech-to-EEG analyses and feeds into the broader encoding-model literature alongside mTRF-Python and Eelbrain.

## Relevance to AGI

mTRF is the canonical pipeline AGI annotations feed into for continuous stimuli. For Forrest Gump audio, AGI's annotation outputs (speech envelope, semantic surprisal from a language model, scene boundaries) become predictor matrices for mTRF, while the corresponding MEG/EEG response (NEMAR-archived recordings) is the dependent variable. The toolbox's well-defined input format (samples-by-features predictor, samples-by-channels response) maps directly onto AGI's events-and-features pattern, and HED tags can be projected through one-hot encoding into mTRF predictors.

## Notable details

- Regularized linear regression with ridge or Tikhonov priors.
- Forward (stimulus to response) and backward (response to stimulus) models.
- Cross-validation selects regularization parameter lambda per dataset.
- Companion mTRFpy Python port maintained by Lalor lab.
- Used heavily in cocktail-party, speech tracking, and music perception studies.

## Open questions / limitations

- Linear assumption breaks down for highly non-linear stimulus features.
- Single-subject analyses are noisy; cross-subject pooling needs careful normalization.
- No native support for non-Gaussian noise or hierarchical priors.
- MATLAB dependency, though the Python port mitigates this.
- Long stimuli with many predictors hit memory limits during ridge cross-validation.

## Citations

Primary: `crosse2016mtrf`. Related:
- `gramfort2013mne`, host environment for many TRF-style analyses in Python.
- `delorme2004eeglab`, MATLAB host environment for the original toolbox.
- `ehinger2019unfold`, alternative regression-deconvolution toolbox for EEG.
- `prince2022glmsingle`, fMRI analogue for single-trial estimation.
- `delavega2022neuroscout`, fMRI analysis platform for naturalistic stimuli.
