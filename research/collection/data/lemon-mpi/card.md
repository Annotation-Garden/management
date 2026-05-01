---
slug: lemon-mpi
type: dataset
strand: data
year: 2019
authors: [Babayan, Erbey, Kumral, Reinelt, Reiter, Röbbig, Schaare, Uhlig, Anwander, Bazin, Horstmann, Lampe, Nikulin, Okon-Singer, Preusser, Pampel, Rohr, Schroeter, Witte, Villringer, Gaebler]
venue: Scientific Data
doi: 10.1038/sdata.2018.308
url: https://openneuro.org/datasets/ds000221
license: CC0 (deposit); paper CC-BY 4.0
modalities: [fmri-3t, mri-anat, dti, eeg, behavior, phenotyping]
tags: [hybrid, multi-task, resting-state, lifespan, mind-body-emotion, leipzig, n=227, ages-20-77]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Leipzig "MPI-Leipzig Mind-Brain-Body" Study (LEMON): 227 adults aged 20 to 77 with paired structural / diffusion / resting-state functional Magnetic Resonance Imaging (fMRI), 62-channel resting and task electroencephalography (EEG), and a comprehensive mind-body-emotion behavioural battery.

## Summary

Babayan and colleagues (Max Planck Institute for Human Cognitive and Brain Sciences, Leipzig) released the LEMON dataset as the core neuroimaging deposit of the larger Mind-Brain-Body cohort. The 227-subject release covers an age-stratified adult cohort with multimodal magnetic resonance imaging (3 Tesla Verio: T1-weighted (T1w), magnetization-prepared 2 rapid acquisition gradient echoes (MP2RAGE), T2-weighted (T2w), diffusion-weighted imaging (DWI), resting-state functional Magnetic Resonance Imaging (fMRI), single-voxel magnetic resonance spectroscopy (MRS)), 62-channel scalp EEG (resting plus a brief active-listening task), and a comprehensive battery of cognitive tests, personality measures, and emotion-regulation questionnaires. The dataset has anchored work on EEG-fMRI fusion, cognitive correlates of resting-state dynamics, and lifespan trajectories.

## Relevance to Annotation Garden Initiative (AGI)

LEMON sits at the hybrid intersection: long resting-state acquisitions, brief task/listening blocks, and dense behavioural phenotyping. Its EEG resting-state segments are a frequent benchmark for AGI-relevant tools (mne-bids-pipeline, EEGLAB, fmriprep). AGI's contribution opportunity is curating canonical HED Generation 3 sidecars for the brief task/listening segments and standardizing the behavioural-trait sidecar format.

## Notable details

- 227 healthy adults (203 in main release; 318 in cumulative release) aged 20 to 77.
- 3 Tesla MRI (multi-modal), 62-channel BrainAmp EEG.
- EEG conditions: 4 minutes eyes-closed, 4 minutes eyes-open, brief audio paradigm.
- Phenotyping: trait questionnaires (Big Five, emotional regulation), cognitive tests (working memory, attention, processing speed).
- BIDS deposits on OpenNeuro: ds000221 (MRI) and ds000221-derivatives (EEG).
- License: paper CC-BY 4.0; deposit CC0.

## Open questions / limitations

- Sample is German-speaking adult Leipzig metro area; generalization untested.
- EEG task content is minimal; the dataset is not designed for naturalistic listening.

## Citations

- Primary: `Babayan2019AMP`.
- Related: HCP Aging (Bookheimer 2019); Cam-CAN (`cam-can/`); 1000 Brains Caspers 2014.
