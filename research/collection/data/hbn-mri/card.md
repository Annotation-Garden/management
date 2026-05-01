---
slug: hbn-mri
type: dataset
strand: data
year: 2017
authors: [Alexander, Escalera, Ai, Andreotti, Febre, Mangone, Vega-Potler, Langer, Alexander, Kovacs, Litke, O'Hagan, Andersen, Bronstein, Bui, Bushey, Butler, Castagna, Camacho, Chan, Citera, Clucas, Cohen, Dufek, Eaves, Frantz, Gardner, Grant-Villegas, Green, Gregory, Hart, Harris, Horton, Kahn, Kabotyanski, Karmel, Kelly, Kleinman, Koo, Kramer, Lennon, Lord, Mantello, Margolis, Merikangas, Milham, Minniti, Neuhaus, Levine, Osman, Parra, Pugh, Racanello, Restrepo, Saltzman, Septimus, Tobe, Waltz, Williams, Yeo, Castellanos, Klein, Paus, Leventhal, Craddock, Koplewicz, Milham]
venue: Scientific Data
doi: 10.1038/sdata.2017.181
url: https://data.healthybrainnetwork.org/
license: data-use-agreement (Child Mind Institute); paper CC-BY
modalities: [fmri, mri-anat, dti, eeg, behavior, phenotyping]
tags: [naturalistic-video, hbn-movies, despicable-me, the-present, multimodal, developmental, n>5000, ages-5-21, psychiatric]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Healthy Brain Network (HBN) biobank: more than 5,000 children and adolescents aged 5 to 21 with paired structural / diffusion / resting-state / movie-viewing functional Magnetic Resonance Imaging (fMRI), high-density electroencephalography (EEG), eye tracking, and deep psychiatric phenotyping.

## Summary

Alexander et al. (2017) describe the Child Mind Institute's Healthy Brain Network (HBN) initiative, an open transdiagnostic research bio-bank for paediatric mental health. The project aimed to enrol 10,000 youths aged 5 to 21 from the New York City area, with stratification across psychiatric diagnoses (attention-deficit/hyperactivity disorder, autism spectrum, anxiety, depression, learning disorders, plus typically-developing controls). The neuroimaging protocol covers structural T1-weighted (T1w) and T2-weighted (T2w) magnetic resonance imaging (MRI), diffusion tensor imaging (DTI), 4-run resting-state fMRI, and naturalistic-movie fMRI (Despicable Me 10-minute clip and The Present 3.5-minute animated short). EEG, eye tracking, voice samples, hand-motion, and an extensive Kiddie Schedule for Affective Disorders and Schizophrenia (K-SADS)-based clinical battery accompany the imaging. As of 2026, the cohort has surpassed 5,000 participants and continues to release in version-controlled batches.

## Relevance to Annotation Garden Initiative (AGI)

HBN is the largest paediatric naturalistic-stimulus neuroimaging dataset in existence. Its movie selection (Despicable Me, The Present, Pixar shorts) is shared with HBN-EEG and broader developmental literature, making movie-level annotations among the highest-leverage contributions a Garden contributor can make. The dataset's rigorous data-use-agreement structure also illustrates how AGI must architect "pointer" annotations for copyright-restricted media: AGI hosts the events.tsv timing and HED tags; users obtain media independently.

## Notable details

- Targeted N = 10,000; current N > 5,000 (as of late 2025 release).
- Age range: 5 to 21.
- Naturalistic stimuli: Despicable Me (10-minute clip), The Present (3.5-minute short), occasional Pixar shorts in newer batches.
- Resting-state and naturalistic fMRI both 3 Tesla Siemens.
- EEG: 128-channel BioSemi (see `hbn-eeg/`).
- Phenotyping: K-SADS clinician interview, behavioural rating scales, cognitive battery (Wechsler Intelligence Scale for Children / Wechsler Abbreviated Scale of Intelligence), language, motor.
- Brain Imaging Data Structure (BIDS) deposit on Functional Connectomes Project / Neuroimaging Tools and Resources Collaboratory (NITRC) and Amazon Web Services (AWS) Open Data.

## Open questions / limitations

- Movie clips are copyright; only timings released.
- Geographic restriction (NYC metro) limits cultural / socioeconomic diversity.
- Naturalistic fMRI annotations are minimal in the original release; community contributions have started but are not centralized.

## Citations

- Primary: `Alexander2017AnOR`.
- Related: HBN-EEG (Shirazi 2024, `hbn-eeg/`); Movies in the Magnet (Vanderwal 2019); Healthy Brain Network Biobank Imaging (Vega Potler ongoing).
