---
slug: little-prince-fmri
type: dataset
strand: data
year: 2022
authors: [Li, Bhattasali, Zhang, Franzluebbers, Luh, Spreng, Brennan, Hale]
venue: Scientific Data
doi: 10.1038/s41597-022-01625-7
url: https://openneuro.org/datasets/ds003643
license: CC-BY-4.0 (paper); CC0 (deposit)
modalities: [fmri-3t, audio-stimulus, behavior]
tags: [naturalistic-audio, narrative, multilingual, the-little-prince, adults, n=49, english-mandarin-french]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Multilingual 3 Tesla functional Magnetic Resonance Imaging (fMRI) of 49 adults listening to The Little Prince (Saint-Exupéry, 1943) in English, Mandarin, or French, designed for cross-linguistic naturalistic language encoding studies.

## Summary

Li, Brennan, Hale and colleagues (Cornell / Michigan / NYU Shanghai) released a 49-subject fMRI dataset where adult participants listened to a translated audiobook of The Little Prince in their native language (English, Mandarin Chinese, or French) over roughly 100 minutes. The dataset includes time-aligned word-level transcripts with part-of-speech tags, dependency parses, and several pre-computed semantic embedding feature time series. The deposit (OpenNeuro ds003643) is openly licensed and BIDS-compliant. The dataset complements monolingual narrative resources (Moth Radio, Narratives) by enabling cross-linguistic encoding-model studies.

## Relevance to Annotation Garden Initiative (AGI)

The Little Prince audiobook is a natural cross-linguistic Garden target: a single canonical text translated into many languages, with paired brain data already in 3 languages and capacity for more. AGI-hosted HED-Lang annotations on the original French text propagate (with translation-aligned mappings) to the other languages. This is an exemplar use case for multilingual stimulus annotation.

## Notable details

- 49 adults: 19 English, 18 Mandarin Chinese, 12 French.
- Stimulus: The Little Prince audiobook, full text translated.
- Roughly 100 minutes per subject; multiple sessions / runs.
- 3 Tesla; 2-second TR.
- Annotations: time-aligned transcripts, part-of-speech, dependency parses, surprisal estimates, embeddings.
- BIDS deposit on OpenNeuro: ds003643.
- License: paper CC-BY 4.0; deposit CC0.

## Open questions / limitations

- Sample sizes per language are unbalanced.
- Audiobook narrators differ across languages (acoustic confounds).
- Adults only.

## Citations

- Primary: `Li2022TheLP`.
- Related: Narratives (Nastase 2021); Moth Radio Hour (Huth 2016); Hale et al. predictive language fMRI series.
