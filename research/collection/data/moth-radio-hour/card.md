---
slug: moth-radio-hour
type: dataset
strand: data
year: 2016
authors: [Huth, de Heer, Griffiths, Theunissen, Gallant]
venue: Nature
doi: 10.1038/nature17637
url: https://github.com/HuthLab/speechmodeltutorial
license: paper publisher (Nature); data CC-BY (Berkeley deposit)
modalities: [fmri-3t, audio-stimulus, behavior]
tags: [naturalistic-audio, podcast, the-moth, semantic-atlas, adults, n=7, deep-sampling, semantic-encoding]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

3 Tesla functional Magnetic Resonance Imaging (fMRI) of 7 adults listening to about 2 hours of "The Moth Radio Hour" autobiographical stories, used by Huth et al. (2016) to construct a continuous semantic atlas of the cerebral cortex.

## Summary

Huth, de Heer, Griffiths, Theunissen, and Gallant (UC Berkeley) recorded 3 Tesla fMRI of 7 adults listening to 10 to 12 stories from The Moth Radio Hour (about 2 hours total) and used voxel-wise encoding with continuous word-embedding features (Word2Vec) to construct the first whole-cortex "semantic atlas" of brain regions tuned to specific semantic dimensions. The dataset has anchored a sustained programme on language encoding across narrative, instructional, and conversational speech stimuli. Audio stimuli, time-aligned transcripts, and pre-processed cortical surfaces are distributed via Berkeley's Gallant Lab repository.

## Relevance to Annotation Garden Initiative (AGI)

Moth Radio Hour is the canonical reference for continuous-language encoding in fMRI. AGI's Stim-BIDS-Audio plus HED-Lang infrastructure must support exactly this style of stimulus: long monologues with rich semantic structure, time-aligned to brain data. The Gallant lab's transcript and feature pipelines are templates for Garden audio-stimulus contributions.

## Notable details

- 7 subjects (Gallant lab "fmri-language" cohort).
- Stimuli: 10 to 12 autobiographical stories from The Moth Radio Hour podcast (about 2 hours total).
- Acquisition: 3 Tesla Siemens Tim Trio; whole-brain coverage, 2.0-second TR.
- Annotations: time-aligned word-by-word transcripts; phoneme alignment via Penn Forced Aligner.
- Voxel-wise semantic atlas published as interactive viewer (gallantlab.org/huth2016).
- License: paper publisher Nature; transcripts and audio features distributed on Berkeley Gallant lab GitHub.

## Open questions / limitations

- Small sample (N = 7).
- Audio stimuli have podcast license; researchers must verify redistribution rights.
- Paper paywalled.

## Citations

- Primary: `Huth2016NaturalSU`.
- Related: Narratives (Nastase 2021, `narratives-pieman/`); de Heer et al. 2017 hierarchical speech model; Tang & Huth 2023 semantic decoding.
