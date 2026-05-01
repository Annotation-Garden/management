---
slug: naturalistic-neuroimaging-db
type: dataset
strand: data
year: 2020
authors: [Aliko, Huang, Gehman, Bliss, Gibson]
venue: Scientific Data
doi: 10.1038/s41597-020-00680-2
url: https://openneuro.org/datasets/ds002837
license: CC0 (deposit); paper CC-BY
modalities: [fmri-3t, behavior]
tags: [naturalistic-video, feature-films, ten-films, adults, n=86, deep-sampling, cross-film]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Naturalistic Neuroimaging Database (NNDb): 86 adults watching one of 10 full-length feature films during 3 Tesla functional Magnetic Resonance Imaging (fMRI), totaling more than 200 hours of brain data with cross-film and within-film coverage.

## Summary

Aliko, Huang, Gehman, Bliss and Gibson (University College London) released the NNDb as an open functional Magnetic Resonance Imaging (fMRI) corpus where 86 adults each watched one of 10 feature films (Back to the Future, Citizenfour, 12 Years a Slave, The Prestige, The Shawshank Redemption, The Usual Suspects, Pulp Fiction, Little Miss Sunshine, Big Lebowski, Forrest Gump). Films range from 90 to 145 minutes; participants completed in 1 to 3 visits. The deposit is BIDS-formatted and openly licensed (CC0). Annotations include scene boundaries (manually identified), speech transcripts, and audio-feature time series. NNDb is the broadest sampling of feature-length films in a single fMRI database and a key dataset for cross-film generalization studies.

## Relevance to Annotation Garden Initiative (AGI)

NNDb is an exceptional Garden growth target. Cross-film coverage at 3T yields a tractable benchmark for testing how AGI annotation layers transfer across stimuli. The diversity of films lets contributors compare narrative-style hypotheses across genres (drama, action, documentary, comedy). NNDb's annotation layer ecosystem is currently sparse beyond shot boundaries, leaving rich room for community annotation contributions (character emotion, theory-of-mind events, sound design).

## Notable details

- 86 subjects, 10 films, 1 to 3 visits each.
- Films total roughly 23 hours of stimulus across 200+ subject-hours.
- 3 Tesla scanner; 1-second TR with multi-band acceleration.
- BIDS deposit on OpenNeuro: ds002837.
- Annotations: shot boundaries, speech transcripts (auto-aligned), audio loudness time series.
- License: paper CC-BY; deposit CC0.

## Open questions / limitations

- Each film viewed by a different subset of participants; cross-film comparisons require careful design.
- Films are copyright; only timing and annotations distributed.
- Limited demographic spread (adult UK undergraduates).

## Citations

- Primary: `Aliko2020`.
- Related: studyforrest (`studyforrest/`); Sherlock fMRI (Chen 2017); Naturalistic Visualization (Vanderwal 2019).
