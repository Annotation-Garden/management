---
slug: mne-python
type: tool
strand: tools
year: 2013
authors: [Gramfort, Luessi, Larson, Engemann, Strohmeier, Brodbeck, Goj, Jas, Brooks, Parkkonen, Hämäläinen]
venue: Frontiers in Neuroscience
doi: 10.3389/fnins.2013.00267
url: https://mne.tools
license: BSD-3-Clause
modalities: [meg, eeg, ieeg]
tags: [MEG, EEG, Python, source-localization, time-frequency, ICA, MVPA, BIDS, open-source]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

MNE-Python is the Python implementation of the MNE software suite for processing Magnetoencephalography (MEG), Electroencephalography (EEG), and intracranial EEG, providing preprocessing, source localization, statistics, time-frequency, and decoding within a unified pipeline.

## Summary

The 2013 Frontiers paper documents MNE-Python's design: state-of-the-art algorithms re-implemented in pure Python, integrated with the scientific Python stack (NumPy, SciPy, matplotlib, scikit-learn), and interoperable with the broader MNE suite via the Functional Image File Format (FIF). The library covers the full MEG/EEG pipeline: filtering, Independent Component Analysis (ICA), epoching, evoked analysis, source localization (Minimum Norm Estimate, beamformers, MxNE, dynamic Statistical Parametric Mapping (dSPM)), time-frequency decomposition (Morlet, multitaper), connectivity, and Multivariate Pattern Analysis (MVPA). Distributed under the new BSD license, MNE-Python has become the default open-source pipeline in MEG and is a major (and Python-native) alternative to EEGLAB for EEG.

## Relevance to AGI

MNE-Python is the second major analysis endpoint for AGI annotations after EEGLAB. Its native BIDS-EEG and BIDS-MEG support (via the mne-bids package) means AGI events.tsv files, including HED tags, are loaded directly into Raw and Epochs objects. For naturalistic stimuli paradigms (Forrest Gump auditory MEG, HBN-EEG passive viewing) MNE-Python is the standard toolchain to compute Temporal Response Functions (TRFs), encoding-model fits, and decoding scores against AGI-supplied stimulus features. Its Python-first interface also fits AGI's broader infrastructure (FastAPI image-annotation backend, Pliers-based pipelines).

## Notable details

- Pure Python plus NumPy/SciPy; optional dependencies on Mayavi for 3D, scikit-learn for decoding.
- Native support for FIF, BrainVision, EDF, BDF, EGI, Neuroscan, CTF, Elekta/Neuromag.
- Source localization: MNE, dSPM, sLORETA, eLORETA, beamformers, MxNE.
- Companion packages: mne-bids, mne-connectivity, mne-features, mne-realtime, mne-icalabel.
- Routinely cited as the reference pipeline for MEG benchmarks and competitions.

## Open questions / limitations

- Source localization quality depends heavily on subject MRI availability.
- Documentation breadth is large but introductory ramp-up remains steep for newcomers.
- Memory footprint for high-density, long-recording datasets can require chunked processing.
- Some clinical EEG features (HED-SCORE artifact tagging) require external plugins.
- Visualization of long continuous recordings (>2 hours) is bottlenecked by browser rendering.

## Citations

Primary: `gramfort2013mne`. Related:
- `delorme2004eeglab`, MATLAB peer; many users move data between the two.
- `ehinger2019unfold`, regression-based deconvolution complementing MNE.
- `crosse2016mtrf`, temporal response function toolbox interoperable via NumPy.
- `gorgolewski2016bids`, input data standard.
- `robbins2021hed`, HED tags consumed via mne-bids.
