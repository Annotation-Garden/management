---
slug: studyforrest
type: dataset
strand: data
year: 2014
authors: [Hanke, Baumgartner, Ibe, Kaule, Pollmann, Speck, Zinke, Stadler]
venue: Scientific Data
doi: 10.1038/sdata.2014.3
url: https://studyforrest.org/
license: CC0 / Public Domain Dedication (annotations CC-BY)
modalities: [fmri-7t, eyetrack, behavior, audio-stimulus]
tags: [naturalistic-video, forrest-gump, deep-sampling, multi-perspective-annotations, adults, n=20]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

7 Tesla functional Magnetic Resonance Imaging (fMRI) of 20 adults listening to the German audio-described version of the feature film Forrest Gump (roughly 2 hours), forming the keystone deep-sampling naturalistic narrative dataset. Subsequent extensions add audiovisual viewing, eye tracking, magnetoencephalography (MEG), and dozens of community annotation layers.

## Summary

Hanke and colleagues (Magdeburg / Otto-von-Guericke University) launched studyforrest in 2014 as the first feature-length-film 7T fMRI dataset. The original release captures whole-brain responses while 20 adults listened to the radio-style audio description of Forrest Gump for 2 hours across 8 segments. Later releases (Hausler & Hanke 2021, Hanke 2016) add audiovisual movie viewing in 3T, 7T retinotopic and category localizers, simultaneous fMRI plus eye-tracking, and magnetoencephalography (MEG). The dataset has spawned a sustained ecosystem of community annotations: shot boundaries, location changes, character speech, phoneme timing, music, emotional ratings (arousal/valence per character), body contact, and high-level constructs like "lies" and "semantic conflict." Studyforrest demonstrated the multi-perspective annotation paradigm AGI is built around.

## Relevance to Annotation Garden Initiative (AGI)

Studyforrest is the historical reference implementation of AGI's value proposition: a single richly annotated naturalistic stimulus that supports many studies. Its annotations live in a heterogeneous ecosystem (DataLad-managed git repos under github.com/psychoinformatics-de). AGI can reuse the proven annotation patterns (shot boundaries, speech, emotion, "social events") as templates and seed Stim-BIDS-formatted aggregations. The Forrest Gump movie itself is copyright-restricted, so AGI must use the pointer-architecture pattern (annotations point at frame timestamps; users supply their own movie).

## Notable details

- 20 subjects (audio-only 7T fMRI); 15 subjects in subsequent audiovisual 3T release.
- Stimulus: feature film Forrest Gump (Robert Zemeckis 1994), German audio description.
- Annotations: shot boundaries, character speech, phoneme timing, music type, location changes, character body contact, character emotion (continuous valence/arousal), eye-gaze patterns, "semantic conflict," "lies," and more.
- Brain Imaging Data Structure (BIDS)-formatted; hosted on Open Magnetic Resonance Archive (OpenMR) and DataLad.
- Multiple companion releases: high-resolution retinotopy, music-listening 7T, MEG (ds003633), eye-gaze (Hanke 2016).

## Open questions / limitations

- Movie is copyright-protected; raw video cannot be redistributed.
- Subject pool is German-speaking adults; cultural and linguistic generalization untested.
- Annotation layers are technically fragmented across multiple Datalad repositories; there is no single canonical source.

## Citations

- Primary: `Hanke2014`.
- Related: studyforrest-eyegaze (Hanke 2016, `studyforrest-eyegaze/`); studyforrest 7T audiovisual extension (Hausler & Hanke 2021); HBN Movies (Alexander 2017); Naturalistic Neuroimaging Database (Aliko 2020).
