---
slug: courtois-neuromod
type: dataset
strand: data
year: 2022
authors: [Boyle, Pinsard, Borghesani, Harrison, Pinho, Pochet, Gilbert, Riva, Bellec]
venue: bioRxiv / Resource paper (Nature Methods stage)
doi: 10.1101/2020.10.07.330183
url: https://www.cneuromod.ca/
license: CC-BY-4.0 (paper); custom DUA (data, primarily Creative Commons-NC)
modalities: [fmri-3t, eyetrack, behavior, audio-stimulus]
tags: [naturalistic-video, friends-tv, movie10, deep-sampling, six-subjects, hundreds-of-hours, multi-task]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Courtois Project on Neuronal Modelling (CNeuroMod): six adults scanned for hundreds of hours each with 3 Tesla functional Magnetic Resonance Imaging (fMRI) while engaging with extensive naturalistic stimuli (Friends television series, 10 films) plus video game play and cognitive tasks. The deepest-sampling individual neuroimaging dataset in existence.

## Summary

Boyle, Bellec and the CNeuroMod consortium (University of Montréal / Mila) maintain a long-running, deep-sampling individual-difference protocol on six subjects. Each subject undergoes hundreds of hours of 3 Tesla fMRI across multiple years, watching all 6 seasons of the Friends television series (more than 100 hours), 10 feature films, playing video games (Shinobi, Mario), and performing cognitive task batteries. The dataset is intended to support training of personalized deep encoding models. Releases include BIDS-formatted fMRI, eye tracking, and detailed task / stimulus event logs. CNeuroMod is the most extreme deep-sampling project beyond NSD and is the natural test bed for person-specific Hierarchical Event Descriptor (HED) annotation pipelines.

## Relevance to Annotation Garden Initiative (AGI)

CNeuroMod's stimulus catalogue (Friends episodes, feature films, video games) is the largest single accumulation of long-form naturalistic content in any neuroimaging project. Each new annotation layer added to a Friends episode (character identity, dialogue, emotion, scene boundary, theory-of-mind events) immediately benefits all six subjects' hundreds of hours of brain data. AGI's pointer-architecture is a perfect fit: stimulus media is third-party (Warner Bros., etc.), but timing and annotation can live in AGI.

## Notable details

- 6 subjects, all actively scanned for years; hundreds of hours per subject.
- Stimuli:
  - Friends television: all 6 seasons (more than 100 hours per subject).
  - "Movie10": 10 feature films viewed each.
  - Video games: Shinobi, Mario.
  - Cognitive batteries: Hyperalignment, Localizer, Multi-Voxel Pattern Analysis (MVPA) tasks.
- BIDS deposits on OpenNeuro (ds002345 and friends).
- Companion eye-tracking and physiology.

## Open questions / limitations

- N = 6 limits between-subject statistics by design.
- Stimuli are copyright; redistribution prohibited.
- Annotation layers (especially for Friends) are partially curated; significant Garden contribution opportunity.

## Citations

- Primary: `Boyle2020TheCP` (arXiv 2204.13099 / bioRxiv 2020.10.07.330183).
- Related: NSD-fMRI (Allen 2022); studyforrest (`studyforrest/`); MyConnectome (Poldrack 2015, `myconnectome/`).
