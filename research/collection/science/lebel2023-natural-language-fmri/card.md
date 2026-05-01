---
slug: lebel2023-natural-language-fmri
type: paper
strand: science
year: 2023
authors: [LeBel, Wagner, Jain, Adhikari-Desai, Gupta, Morgenthal, Tang, Xu, Huth]
venue: Scientific Data
doi: 10.1038/s41597-023-02437-z
url: https://www.nature.com/articles/s41597-023-02437-z
license: CC-BY
modalities: [fmri]
tags: [dataset, naturalistic-language, encoding-benchmark, story-listening, theme-6]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Open dataset of 8 subjects each listening to 27+ hours of narrative podcasts during fMRI, designed as a benchmark for voxel-wise encoding of language; the largest naturalistic-language fMRI corpus to date.

## Summary

LeBel and colleagues release one of the largest single-subject naturalistic-listening fMRI datasets: 8 subjects, each scanned across 20+ sessions, listening to >27 hours of stories from "The Moth Radio Hour", "Modern Love", "Anthropocene Reviewed", and others. The dataset is OpenNeuro-deposited, BIDS-formatted, and includes time-aligned word-level transcripts. The accompanying paper validates baseline encoding model performance against the Huth 2016 988-d semantic embedding and demonstrates that data scaling (within-subject) yields predictable encoding-accuracy gains. The dataset has become the de-facto benchmark for the language-encoding literature (Antonello 2023 scaling laws, Tang 2023 decoder, etc.).

## Relevance to AGI

LeBel 2023 is the **prototypical AGI commons dataset**: open, annotated (word-level transcripts), versioned, BIDS-formatted, and explicitly designed for community re-use. AGI's mission is to extend this pattern from one paradigm to many (NSD images, Forrest Gump, HBN movies, future commons stimuli) and to layer richer annotations (HED tags, semantic graphs, foundation-model embeddings). LeBel 2023 also provides the baseline against which annotation-richness-vs-quantity sufficiency studies (Theme 6) can be run.

## Notable details

- 8 subjects (3 used as primary "deep-sample" cohort)
- 27+ hours per subject, ~80 distinct stories
- BIDS-formatted, OpenNeuro deposit
- Word-level forced alignment provided
- Includes resting state and localizer runs
- Used as the basis for Huth-lab encoding/decoding work since 2022

## Open questions / limitations

- English-only; multilingual extensions are needed for cross-cultural generalization.
- 8 subjects; within-subject deep-sampling does not replace across-subject diversity.
- Word-level alignment but no HED tagging; semantic structure is implicit.
- No explicit event-segmentation or character-tracking annotations.
- Listener attention is uncontrolled; how attentional state modulates encoding is mostly unaddressed.
- Doesn't include eye-tracking or behavioral state measures beyond minimal task button-press.
- Annotation provenance: transcript alignment is automatic; manual rater annotations would enrich Theme 4/6 analyses.
- Cross-modality (does the same listener subset have MEG/EEG counterparts?) not yet realized; a natural AGI Phase 2 deliverable.
- Demographics are limited (small N, narrow age range); developmental and clinical extensions needed.

## Citations

Primary BibTeX key: `lebel2023natural`

Related works:
- Huth et al. 2016; predecessor encoding paradigm
- Antonello et al. 2023; scaling laws on this dataset
- Tang et al. 2023; semantic decoder using this dataset
- Allen et al. 2022 (NSD); analogous dataset for vision
- Hebart et al. 2023 (THINGS-data); multimodal counterpart
