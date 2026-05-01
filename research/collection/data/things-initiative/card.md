---
slug: things-initiative
type: dataset
strand: data
year: 2023
authors: [Hebart, Contier, Teichmann, Rockter, Zheng, Kidder, Corriveau, Vaziri-Pashkam, Baker]
venue: eLife
doi: 10.7554/eLife.82580
url: https://things-initiative.org/
license: CC-BY-4.0 (paper); object-image set has mixed Creative Commons / research-only terms
modalities: [fmri, meg, eeg, behavior]
tags: [naturalistic-images, object-concepts, cross-modal, adults, n=variable, semantic-features]
agi_relevance: high
imported_from: grant-proposals/proposals/R01/2026-nlm-annotation/lit-review/Neuroimaging Annotation Paradigm Literature Review.md
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Things Initiative provides a unified set of 1,854 object concepts with 26,107 high-quality images plus paired functional Magnetic Resonance Imaging (fMRI), magnetoencephalography (MEG), and electroencephalography (EEG) recordings, enabling fair cross-modal benchmarking of object representation.

## Summary

Hebart and colleagues (Max Planck / National Institute of Mental Health) released the Things Initiative as the first cross-modal naturalistic image database designed from the ground up for representational analysis. The image set spans 1,854 object concepts (each a high-frequency English noun) with 12+ exemplars each. Brain data accompany the same concepts: Things-fMRI (3 subjects, 8,640 trials each), Things-MEG (4 subjects, 22,448 trials), and Things-EEG / Things-EEG2 (50+ subjects, rapid serial visual presentation). The package also includes 4.7 million human similarity judgments from the THINGS database and a 49-dimensional embedding of concept similarity. Things has rapidly become the standard for object-decoding benchmarks across fMRI, MEG, and EEG.

## Relevance to Annotation Garden Initiative (AGI)

Things is the cleanest example of "build an annotation graph once, harvest forever" already operating in neuroscience. The 1,854 concept identifiers, hierarchical category structure, and 4.7M similarity judgments are exactly the kind of community annotation layer AGI should host. The dataset proves the multi-modal annotation reuse model AGI is targeting; gaps remain for finer-grained image annotations (saliency, bounding boxes, scene context) which AGI can host as additive layers.

## Notable details

- 1,854 concrete object concepts; 26,107 images (THINGS database).
- Things-fMRI: 3 subjects x 12 sessions, 8,640 trials per subject.
- Things-MEG: 4 subjects x 12 sessions, 22,448 trials per subject.
- Things-EEG2 (Gifford 2022): 10 subjects, 16,540 training trials, 200 concept test set.
- Behavioral: 4.7 million similarity triplet judgments; 49-dimensional concept embedding.
- License: paper CC-BY 4.0 (eLife); image set has heterogeneous Creative Commons / research-use terms.

## Open questions / limitations

- Image background normalization (white background) sacrifices scene context; less ecological than NSD COCO scenes.
- Concept set is English-centric; cultural / linguistic generalization untested.
- Within-modality sample sizes are still small (3 to 10 subjects), limiting individual-difference research.

## Citations

- Primary: `Hebart2023ThingsInitiative`.
- Related: THINGS database (Hebart 2019, PLoS ONE); Things-MEG (Hebart 2022); Things-EEG2 (Gifford 2022); NOD-EEG (Zhang 2025).
