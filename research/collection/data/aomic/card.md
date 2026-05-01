---
slug: aomic
type: dataset
strand: data
year: 2021
authors: [Snoek, van der Miesen, Beemsterboer, van der Leij, Eigenhuis, Steven Scholte]
venue: Scientific Data
doi: 10.1038/s41597-021-00870-6
url: https://nilab-uva.github.io/AOMIC.github.io/
license: CC-BY-4.0 (paper); CC0 (deposit)
modalities: [fmri-3t, mri-anat, dti, behavior, phenotyping]
tags: [cognitive-task, large-cohort, faces, stop-signal, working-memory, n=1500+, adults, students]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Amsterdam Open Magnetic Resonance Imaging (MRI) Collection (AOMIC): three openly released datasets totaling more than 1,500 healthy young adults with paired structural / diffusion / resting / task fMRI plus extensive psychological phenotyping, collected at the University of Amsterdam.

## Summary

Snoek and colleagues released AOMIC as three datasets (PIOP1: n=216, PIOP2: n=226, ID1000: n=928) collected on a single 3 Tesla scanner at the University of Amsterdam over 5 years. Tasks include face perception (PIOP1, PIOP2), Stop-Signal (PIOP1), Working Memory (PIOP1), passive movie viewing (ID1000, a 5-minute clip from "Rocketman"), and resting state. The deposits are BIDS-compliant, openly licensed (CC0 deposit, CC-BY paper), and accompanied by detailed phenotypic data (Big Five, intelligence, mental health screens). AOMIC has become a community benchmark for both task-based and naturalistic-stimulus methods development.

## Relevance to Annotation Garden Initiative (AGI)

AOMIC sits exactly at the naturalistic-to-cognitive-task interface that AGI is designed to articulate: PIOP1/PIOP2 are pure cognitive tasks while ID1000 includes a 5-minute passive-viewing movie. This makes AOMIC an ideal contrast for benchmarking how much annotation density helps. The cognitive task events are simple, HED-taggable, and open-licensed; the movie clip ("Rocketman") is copyrighted but timing and annotations can be hosted in AGI as pointer-architecture layers.

## Notable details

- Three datasets: PIOP1 (n=216), PIOP2 (n=226), ID1000 (n=928); total >1,500.
- Tasks: emotional faces, working memory, Stop-Signal, anticipation, passive movie viewing.
- Movie stimulus: 5-minute clip from "Rocketman" (used in ID1000).
- Single 3 Tesla Philips Achieva scanner; consistent acquisition protocol.
- Deep phenotyping: Big Five, IQ subtests, mental health screens, demographics.
- BIDS deposits on OpenNeuro: ds002785, ds002790, ds003097.
- License: paper CC-BY; deposits CC0.

## Open questions / limitations

- All Dutch university student / Amsterdam metro area; demographic and cultural homogeneity.
- Movie clip is short (5 minutes) and copyrighted.

## Citations

- Primary: `Snoek2021TheAO`.
- Related: HCP Task (`hcp-task/`); Cam-CAN (`cam-can/`); OpenNeuro task deposits.
