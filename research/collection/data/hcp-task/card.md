---
slug: hcp-task
type: dataset
strand: data
year: 2013
authors: [Barch, Burgess, Harms, Petersen, Schlaggar, Corbetta, Glasser, Curtiss, Dixit, Feldt, Nolan, Bryant, Hartley, Footer, Bjork, Poldrack, Smith, Johansen-Berg, Snyder, Van Essen]
venue: NeuroImage
doi: 10.1016/j.neuroimage.2013.05.033
url: https://www.humanconnectome.org/
license: data-use-agreement (Human Connectome Project / Washington University); paper publisher
modalities: [fmri-3t, mri-anat, dti, behavior]
tags: [cognitive-task, working-memory, language, motor, gambling, social, emotion, relational, n=1200, adults]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Human Connectome Project (HCP) task functional Magnetic Resonance Imaging (fMRI) battery: 1,200 healthy young adults completing seven canonical cognitive tasks (working memory, language, motor, gambling, social, emotion, relational) in 3 Tesla and 7 Tesla scanners.

## Summary

Barch et al. (2013) describe the HCP task fMRI battery: seven well-validated cognitive tasks spanning major domains of cognition, designed to elicit reliable activation patterns in 1,200 healthy young adults aged 22 to 35. The tasks are: Working Memory (n-back), Language (story / math), Motor (foot / hand / tongue), Gambling (Delgado card task), Social (Heider-Simmel animations), Emotion (Hariri faces / shapes), and Relational. The dataset is the most widely cited reference for "controlled task" cognitive neuroimaging at scale; it anchors the right-hand end of the AGI naturalistic-to-cognitive-task spectrum.

## Relevance to Annotation Garden Initiative (AGI)

HCP task fMRI is a flagship example of the cognitive-task end of the spectrum. Each task's events.tsv is straightforward (small set of trial types per task), and the entire battery is HED-taggable in roughly 100 lines of sidecar JSON. AGI's Garden contribution opportunity is to provide a curated, version-controlled HED Generation 3 mapping of every HCP task event (an artifact that does not exist in canonical form). This becomes the canonical reference for cognitive-task HED tagging. HCP tasks also serve as the "controlled comparator" against naturalistic-stimulus encoding gains.

## Notable details

- 1,200+ participants (HCP Young Adult release).
- Seven tasks, ~ 5 to 10 minutes each: Working Memory, Language, Motor, Gambling, Social Cognition, Emotion, Relational.
- 3 Tesla customized Siemens Connectome scanner (TR 0.72 s) plus 7 Tesla retest sub-cohort.
- Behavioral data, retest, twins, and family structure.
- HCP Lifespan extensions: HCP-D (development), HCP-A (aging) reuse subsets of these tasks.
- License: Open Access via DUA at db.humanconnectome.org.

## Open questions / limitations

- Controlled-task design lacks the rich annotation surface naturalistic stimuli offer.
- Adults only (Lifespan extensions cover other ages with overlapping but distinct task batteries).
- Paywalled descriptor.

## Citations

- Primary: `Barch2013FunctionIO`.
- Related: HCP-D Sommerville 2018; HCP-A Bookheimer 2019; ABCD task fMRI (`abcd-task/`); MyConnectome (`myconnectome/`).
