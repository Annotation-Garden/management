---
slug: eeglab
type: tool
strand: tools
year: 2004
authors: [Delorme, Makeig]
venue: Journal of Neuroscience Methods
doi: 10.1016/j.jneumeth.2003.10.009
url: https://sccn.ucsd.edu/eeglab/
license: GPL-2.0-or-later
modalities: [eeg, ieeg, meg]
tags: [EEG, MATLAB, ICA, time-frequency, ERP-image, plugins, EEGLAB, SCCN]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

EEGLAB is a MATLAB toolbox with a graphical interface for processing single-trial Electroencephalography (EEG) data, originally introducing routine Independent Component Analysis (ICA) and time-frequency decomposition to the wider community and now the de facto plugin host for most EEG analysis innovations.

## Summary

The 2004 paper describes a three-layer architecture: a graphical interface for naive users, history-recording "pop_" functions for scriptable middle-ground use, and raw functions callable from any script. EEGLAB introduced ERP-image plotting, runica-based Infomax ICA, scalp-map dipole modeling, and bootstrap statistics to a community that had largely been confined to amplitude-and-latency ERP measures. Its plug-in mechanism turned it into a platform: ICLabel (component classification), DIPFIT (dipole modeling), AMICA (adaptive ICA), Unfold (regression-based deconvolution), and dozens of others now ship through the EEGLAB extension manager. EEGLAB is GNU-licensed for non-commercial use, runs on any platform with MATLAB, and serves as the reference implementation for the BIDS-EEG specification at the Swartz Center for Computational Neuroscience (SCCN).

## Relevance to AGI

EEGLAB is the analysis endpoint for most of the EEG datasets that AGI's stimuli are designed to feed (HBN-EEG, NEMAR collections, NeurIPS EEG Competition data). Annotations exported from AGI must reach EEGLAB through three paths: (1) HED-tagged events.tsv ingested by the EEGLAB BIDS importer, (2) per-frame stimulus features (CLIP, mTRF predictors) loaded as continuous EEG.event covariates, (3) plugin-level access for downstream regression in Unfold or mTRF. EEGLAB's event structure is the lowest-friction integration target for AGI's annotation outputs.

## Notable details

- Three-layer design: GUI menus, pop_ history-tracking functions, raw functions.
- ICA implementations: Infomax (runica), Extended Infomax, AMICA (plugin).
- Plugins: ICLabel, DIPFIT, Unfold, AMICA, ERPLAB, MoBI Lab, EEG-BIDS, HEDTools.
- Native file format: .set / .fdt; reads BDF, EDF, EGI, Neuroscan, BrainVision.
- Supports HED tagging through the HEDTools plugin (Robbins et al.).

## Open questions / limitations

- MATLAB dependency limits accessibility for Python-first labs.
- Single-machine architecture; cluster execution requires custom wrappers.
- Plugin quality varies; no formal review process for third-party plugins.
- ICA decomposition reproducibility depends on initial random seed and rank.
- Long-running interactive sessions are hard to capture as reproducible scripts.

## Citations

Primary: `delorme2004eeglab`. Related:
- `gramfort2013mne`, Python alternative with overlapping scope.
- `ehinger2019unfold`, EEGLAB-compatible regression deconvolution toolbox.
- `crosse2016mtrf`, companion toolbox for continuous-stimulus models.
- `delorme2022nemar`, archive that exposes EEGLAB-ready BIDS-EEG datasets.
- `robbins2021hed`, HED tagging integrated as an EEGLAB plugin.
