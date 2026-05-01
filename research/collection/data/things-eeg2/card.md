---
slug: things-eeg2
type: dataset
strand: data
year: 2022
authors: [Gifford, Dwivedi, Roig, Cichy]
venue: NeuroImage
doi: 10.1016/j.neuroimage.2022.119754
url: https://osf.io/3jk45/
license: CC-BY-4.0 (data deposit)
modalities: [eeg, behavior]
tags: [naturalistic-images, things-imagenet, rapid-serial, n=10, adults, single-trial-eeg, decoding-benchmark]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

Things-EEG2: 10 adults viewing 16,540 distinct THINGS object images via rapid serial visual presentation (RSVP) at high-density scalp electroencephalography (EEG); the largest single-trial scalp-EEG object-image benchmark to date.

## Summary

Gifford, Dwivedi, Roig, Cichy (Free University Berlin / Frankfurt / York) released Things-EEG2 as a large-scale scalp EEG counterpart to the THINGS image database. 10 healthy adults viewed 16,540 distinct training images plus a 200-concept test set via 5 Hz rapid serial visual presentation (RSVP) while 64-channel scalp EEG was recorded. The deposit is openly licensed and has rapidly become the standard benchmark for image-from-EEG decoding (Algonauts 2024, Tang 2024 NeurIPS). The companion paper provides extensive baseline decoding metrics and feature-encoding analyses.

## Relevance to Annotation Garden Initiative (AGI)

Things-EEG2 is a high-density scalp EEG counterpart to THINGS / NSD. The 1,854 THINGS concept identifiers anchor it to the rest of the THINGS ecosystem, so any concept-level annotation layer AGI hosts (animacy, super-ordinate categories, naming agreement) propagates here. Good test bed for AGI's annotation-density-versus-encoding-gain studies because the decoding pipelines are openly distributed.

## Notable details

- N = 10 adults.
- 16,540 training images plus 200-concept test set.
- 5 Hz rapid serial visual presentation; 200 ms image-on, no fixation interval.
- 64-channel BrainProducts EEG, 1000 Hz sampling.
- BIDS-style deposit on Open Science Framework (OSF) and Zenodo.
- License: CC-BY 4.0.

## Open questions / limitations

- 10 subjects only (limited individual differences research).
- RSVP design lacks behavioural component during image stream; attention and memory are not measured.

## Citations

- Primary: `Gifford2022ALA`.
- Related: NOD-EEG (`nod-eeg/`); THINGS initiative (`things-initiative/`); NSD-EEG / alljoined (`nsd-eeg-alljoined/`).
