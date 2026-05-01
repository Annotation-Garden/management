---
slug: bold5000
type: dataset
strand: data
year: 2019
authors: [Chang, Pyles, Marcus, Gupta, Tarr, Aminoff]
venue: Scientific Data
doi: 10.1038/s41597-019-0052-3
url: https://bold5000.github.io/
license: CC-BY-4.0
modalities: [fmri-3t, behavior]
tags: [naturalistic-images, scenes, mixed-stimulus-set, deep-sampling, adults, n=4]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

3 Tesla functional Magnetic Resonance Imaging (fMRI) of 4 adults viewing 5,254 distinct images drawn from Microsoft Common Objects in Context (COCO), ImageNet, and Scene UNderstanding (SUN) image databases, totaling 4,916 unique stimuli plus repetitions across 16 sessions per subject.

## Summary

The Brain, Object, Landscape Dataset (BOLD5000) is the precursor and 3T counterpart to the Natural Scenes Dataset (NSD). Chang, Pyles, Marcus and colleagues (Carnegie Mellon University / University of Pittsburgh) collected slow event-related 3T fMRI from 4 adult subjects across 15 to 16 task sessions while they viewed 4,916 unique images plus 112 repeated images. Stimuli combine 1,000 isolated objects from ImageNet, 2,000 scene images from SUN, and 2,000 complex scenes from COCO. The slower trial structure (10 second TR-locked) and 3T magnet make BOLD5000 more accessible than NSD for many labs while still providing massive within-subject trial counts. The release includes a complete BIDS-formatted dataset on OpenNeuro (ds001499) with raw, pre-processed, and beta-weight derivatives.

## Relevance to Annotation Garden Initiative (AGI)

BOLD5000 is a textbook AGI use case: a single image set drawn from three popular image databases now anchors thousands of community studies, yet the rich-annotation graph (HED tags per object, scene categories, saliency, captions) is still scattered. The dataset's 3T accessibility makes it a natural target for the first wave of Garden contributions in the visual-stimulus track.

## Notable details

- 4 subjects, 15 to 16 sessions each; total roughly 5,254 stimulus presentations per subject.
- Stimulus set: 1,000 ImageNet, 2,000 SUN, 2,000 COCO + 112 repetitions.
- 3T Siemens Magnetom Verio at CMU/UPMC. 2-mm isotropic, TR = 2 s.
- Slow event-related design: 1 s on / 9 s off (10 s trial length) for high signal-to-noise per trial.
- BIDS dataset on OpenNeuro: ds001499.
- License: CC-BY-4.0.

## Open questions / limitations

- Slower trial design means fewer trials per session than NSD's rapid design.
- Mixed stimulus set complicates direct comparison to NSD or THINGS.
- Only 4 subjects.

## Citations

- Primary: `Chang2019BOLD5000`.
- Related: NSD-fMRI (Allen 2022); GLMsingle (Prince 2022); Generic Object Decoding (Horikawa & Kamitani 2017).
