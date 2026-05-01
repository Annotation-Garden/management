---
slug: narratives-pieman
type: dataset
strand: data
year: 2021
authors: [Nastase, Liu, Hillman, Zadbood, Hasenfratz, Keshavarzian, Chen, Honey, Yeshurun, Regev, Nguyen, Chang, Baldassano, Lositsky, Simony, Chow, Leong, Brooks, Micciche, Choe, Goldstein, Vanderwal, Halchenko, Norman, Hasson]
venue: Scientific Data
doi: 10.1038/s41597-021-01033-3
url: https://openneuro.org/datasets/ds002345
license: CC-BY-4.0 (paper); CC0 (deposit)
modalities: [fmri-3t, audio-stimulus, behavior]
tags: [naturalistic-audio, spoken-narratives, pieman, multi-story, adults, n=345, hed-tagged]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The "Narratives" collection: 345 adult subjects listening to 27 spoken-story stimuli (including the canonical Pieman, Black, Sherlock-narrated, and others) during 3 Tesla functional Magnetic Resonance Imaging (fMRI), forming the largest open spoken-narrative neuroimaging corpus.

## Summary

Nastase, Liu and colleagues (Hasson lab, Princeton) aggregated 27 spoken-story listening fMRI experiments collected at the Princeton Neuroscience Institute between 2011 and 2018 into a single openly released BIDS dataset on OpenNeuro (ds002345). The collection spans 345 unique subjects (some performed multiple stories) for a total of 891 functional runs and roughly 6.4 days of cumulative scanner time. Stories include the canonical "Pieman" (Yeshurun 2017), "Black", "Forgot," "Sherlock-Narrated", "21st Year," and many others. Each story has time-stamped transcripts, manually annotated event boundaries (where available), and Praat-derived audio feature time series. The release is the largest single-genre naturalistic neuroimaging corpus and a frequent benchmark for naturalistic language encoding.

## Relevance to Annotation Garden Initiative (AGI)

Narratives is the audio-modality counterpart to NSD: a large open corpus, paired with stimulus annotation infrastructure (transcripts, audio features, scene boundaries), serving as a benchmark for cross-study comparison. AGI's HED-Lang sidecar approach maps cleanly onto the Narratives data dictionary. Garden contributions on top: phoneme-level forced alignment, dependency parses, narrative-event tags, prosodic features.

## Notable details

- 345 subjects, 891 functional runs, 27 story stimuli.
- Stimulus durations: 4 to 56 minutes per story.
- 3 Tesla Siemens Skyra; 1.5-second TR.
- BIDS-Audio compliant: stimuli WAV files redistributed in the deposit (license cleared); transcripts as TSV.
- Openly released annotations: word and phoneme alignment, prosodic features, dramatic event boundaries.
- License: paper CC-BY 4.0; data deposit CC0.

## Open questions / limitations

- Adult sample only.
- English language only.
- Cross-story inter-subject correlation analyses limited by uneven N per story.

## Citations

- Primary: `Nastase2021TheN`.
- Related: Pieman fMRI (Yeshurun 2017, `narratives-pieman/`); Moth Radio Hour (Huth 2016, `moth-radio-hour/`); Little Prince (Li 2022, `little-prince-fmri/`).
