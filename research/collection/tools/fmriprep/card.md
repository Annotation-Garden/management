---
slug: fmriprep
type: tool
strand: tools
year: 2019
authors: [Esteban, Markiewicz, Blair, Moodie, Isik, Erramuzpe, Kent, Goncalves, DuPre, Snyder, Oya, Ghosh, Wright, Durnez, Poldrack, Gorgolewski]
venue: Nature Methods
doi: 10.1038/s41592-018-0235-4
url: https://fmriprep.org
license: Apache-2.0
modalities: [fmri]
tags: [fMRIPrep, BIDS-App, preprocessing, ANTs, FreeSurfer, FSL, Nipreps, containerized]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

fMRIPrep is a containerized Brain Imaging Data Structure (BIDS) App that preprocesses functional Magnetic Resonance Imaging (fMRI) data with a robust, automated pipeline combining the best practices of Advanced Normalization Tools (ANTs), FSL, and FreeSurfer.

## Summary

fMRIPrep takes raw BIDS fMRI data and produces preprocessed time series in standard or native space along with a comprehensive set of confound regressors and a per-subject Hyper Text Markup Language (HTML) quality control report. Its pipeline includes skull-stripping, bias-field correction, tissue segmentation, susceptibility-distortion correction (fieldmap or fieldmap-less SyN), motion correction, slice timing correction, and spatial normalization to MNI152 or fsaverage. The 2019 Nature Methods paper documents the design and benchmarks robustness across hundreds of public datasets. fMRIPrep is the de facto preprocessing pipeline for OpenNeuro datasets, NeuroScout, Human Connectome Project derivatives, and naturalistic-fMRI work.

## Relevance to AGI

fMRIPrep sits on the response side of AGI's stimulus-anchored data flow. Most AGI repositories will not run fMRIPrep directly; instead, they will reference recording datasets that have already been fMRIPrep-processed, and they will provide annotations (events.tsv with HED tags, continuous predictors) that line up with fMRIPrep outputs. The BIDS-App container model fMRIPrep helped popularize is also the deployment template AGI should follow for any future annotation pipeline that needs to run reproducibly across users.

## Notable details

- BIDS App distributed via Docker, Singularity, Apptainer.
- Tools used: ANTs, FSL, FreeSurfer, AFNI utilities.
- Outputs follow BIDS-Derivatives specification.
- Per-subject HTML report with embedded mosaics and registration checks.
- Maintained by the Nipreps consortium, with siblings sMRIPrep, dMRIPrep, ASLPrep, NIRSPrep.

## Open questions / limitations

- Compute and memory requirements scale with dataset size; full fMRIPrep run can take 10+ hours per subject.
- FreeSurfer recon-all is the slowest step and is only optional.
- Some site-specific artifacts evade automatic correction.
- Confound regressor selection ("the right confounds") remains a downstream choice.
- Continuous evolution between versions can break re-execution; specifying a version pin is essential.

## Citations

Primary: `esteban2019fmriprep`. Related:
- `gorgolewski2016bids` — input data standard.
- `esteban2017mriqc` — companion quality-control tool.
- `prince2022glmsingle` — downstream single-trial estimation.
- `delavega2022neuroscout` — execution platform that wraps fMRIPrep.
- `markiewicz2021openneuro` — primary archive of input data.
