---
slug: prince2022-glmsingle
type: paper
strand: science
year: 2022
authors: [Prince, Charest, Kurzawski, Pyles, Tarr, Kay]
venue: eLife
doi: 10.7554/eLife.77599
url: https://elifesciences.org/articles/77599
license: CC-BY
modalities: [fmri]
tags: [single-trial-estimation, hrf-estimation, glmsingle, encoding-precondition, nsd, ridge-regression, theme-1]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

GLMsingle is an open-source toolbox that estimates per-trial Blood-Oxygen-Level-Dependent (BOLD) responses ("betas") for naturalistic fMRI experiments by combining voxel-wise hemodynamic response function (HRF) selection, GLMdenoise nuisance regression, and fractional ridge regression; boosting trial-level signal-to-noise ratio (SNR) two- to threefold on Natural Scenes Dataset (NSD).

## Summary

Prince and colleagues address a precondition for any annotation-driven encoding analysis on naturalistic fMRI: getting reliable trial-level BOLD estimates. GLMsingle is a three-stage pipeline (voxel-wise HRF library selection, GLMdenoise data-driven nuisance regression, fractional ridge regression) packaged as a publicly released MATLAB and Python toolbox. They evaluate on NSD, the Boston Old Library Discrimination dataset, and others, showing 2-3x improvement in across-trial reliability (split-half correlation, leave-one-out r) and corresponding gains in downstream encoding model performance. The paper is methodological infrastructure: every recent NSD-based encoding/decoding paper (MindEye, Conwell 2024, Lahner MOSAIC) uses GLMsingle betas as input.

## Relevance to AGI

Annotation-driven analysis pipelines need **trial-level neural responses** that match per-stimulus annotations. GLMsingle is the canonical solution and is already a flagship tool in the AGI tool ecosystem. AGI's job is to make sure that the betas produced by GLMsingle are linked to BIDS- and HED-annotated stimulus events in a machine-actionable way (HED-MCP server, Stim-BIDS sidecars), so that downstream encoding/decoding can be reproduced by anyone in the commons.

## Notable details

- Open-source toolbox: MATLAB and Python, GitHub-hosted with documentation
- Three stages: HRF library + GLMdenoise + fractional ridge regression
- Per-voxel HRF selected from a library of ~20 candidate HRFs
- Validation: NSD, Boston Adolescent Neuroimaging of Depression and Anxiety (BANDA), and other datasets
- 2-3x SNR improvement claimed; documented effect on encoding model R^2
- Publicly hosted at https://glmsingle.readthedocs.io

## Open questions / limitations

- Designed for event-related designs with discrete trial onsets; continuous-narrative datasets (Forrest Gump, HBN movies) need different methods (continuous regression, finite-impulse-response).
- HRF library is fixed; doesn't handle systematic regional HRF variation tied to vascular pathology.
- No automatic integration with HED or BIDS annotations; users must hand-build event timing files.
- Does not report how the SNR gains scale with within-session trial count; minimum data required for reliable betas is not characterized.
- Does not explicitly model **state-dependent** modulation (attention, arousal) that could confound trial-level estimates.
- Restricted to fMRI; analogous trial-level estimators for Magnetoencephalography (MEG) and Electroencephalography (EEG) are needed for cross-modal annotation work (Theme 7).
- The "noise ceiling" estimation method is heuristic and may overstate explainable variance for low-trial-count regions.

## Citations

Primary BibTeX key: `prince2022improving`

Related works:
- Allen et al. 2022; NSD dataset where GLMsingle was developed
- Kay et al. 2008; early voxel-wise modeling that motivated single-trial estimation
- Lahner et al. 2025 (MOSAIC); uses GLMsingle to aggregate fMRI datasets
- Hebart et al. 2023 (THINGS-data); uses GLMsingle in multimodal fMRI processing
- Naselaris et al. 2011; encoding/decoding framework GLMsingle feeds
