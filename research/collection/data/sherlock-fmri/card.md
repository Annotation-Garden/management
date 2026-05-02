---
slug: sherlock-fmri
type: dataset
strand: data
year: 2017
authors: [Chen, Leong, Honey, Yong, Norman, Hasson]
venue: Nature Neuroscience
doi: 10.1038/nn.4450
url: https://dataspace.princeton.edu/handle/88435/dsp01nz8062179
license: data-use-agreement (Princeton Neuroscience Institute); paper publisher
modalities: [fmri-3t, behavior]
tags: [naturalistic-video, sherlock-bbc, narrative, episodic-memory, adults, n=17, scene-segmentation]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: rough
---

## TL;DR

3 Tesla functional Magnetic Resonance Imaging (fMRI) of 17 adults watching a 50-minute episode of the BBC's Sherlock followed by a free-recall description, used to study event-segmentation, narrative memory, and Default Mode Network (DMN) dynamics.

## Summary

Chen, Leong, Honey, Yong, Norman, Hasson (Princeton Neuroscience Institute) recorded 3T fMRI from 17 adults during continuous viewing of a 50-minute clip of the BBC television series Sherlock (Season 1 Episode 1: "A Study in Pink") and during a subsequent verbal free-recall of the episode. The dataset has anchored a wave of work on "event boundaries" in continuous narrative experience, the Default Mode Network's role in memory encoding, and shared neural patterns across viewers and recallers. Hand-coded scene-boundary annotations and time-locked transcripts of the recall sessions are distributed alongside the fMRI data via Princeton DataSpace.

## Relevance to Annotation Garden Initiative (AGI)

Sherlock is a long-form naturalistic stimulus with widely cited annotation layers (event boundaries, narrative summaries, character / location / event vectors). AGI inherits its annotation patterns directly: human-rated event boundaries, transcribed verbal recall, semantic vector representations of scenes. The Sherlock+ extensions (Sherlock-Movie, Sherlock-Recall, ProsodyLab transcripts) are exemplar Garden contributions.

## Notable details

- 17 healthy adult participants.
- Stimulus: BBC Sherlock S01E01 ("A Study in Pink"), 50-minute clip.
- 3 Tesla Siemens; 1.5-second TR; whole-brain coverage.
- Free-recall task: subjects verbally retold the episode in the scanner immediately after viewing.
- Annotations: hand-coded scene boundaries (50+ scenes); transcribed recall; semantic-vector representations (Word2Vec, GloVe) per scene.
- Distributed via Princeton DataSpace under DUA.

## Open questions / limitations

- Stimulus copyright (BBC) restricts redistribution.
- Sample size is small (17).
- Annotation layers were curated by the Hasson/Norman labs; community contribution patterns are limited.

## Citations

- Primary: `Chen2017SharedMP`.
- Related: Hasson "neural movies" body of work; Sherlock-Movie ds001132 OpenNeuro.
