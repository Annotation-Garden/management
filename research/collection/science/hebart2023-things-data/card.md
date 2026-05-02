---
slug: hebart2023-things-data
type: paper
strand: science
year: 2023
authors: [Hebart, Contier, Teichmann, Rockter, Zheng, Kidder, Corriveau, Vaziri-Pashkam, Baker]
venue: eLife
doi: 10.7554/eLife.82580
url: https://elifesciences.org/articles/82580
license: CC-BY
modalities: [fmri, meg, eeg, behavior]
tags: [multimodal, things, dataset, object-concepts, cross-modal-benchmark, theme-7]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

THINGS-data: a multimodal mega-dataset of fMRI, MEG, and behavioral responses on the THINGS object database (~1,854 concepts, ~26,000 images), with shared subjects across modalities; the most complete cross-modal benchmark for object representation in cognitive neuroscience.

## Summary

Hebart and colleagues release THINGS-data, an extension of the THINGS object database (Hebart 2019) with three matched neuroimaging modalities. The fMRI cohort (3 subjects, ~22 hours each) viewed a subset of THINGS images at ultra-high field. The MEG cohort (4 subjects) viewed the same subset. The behavioral cohort comprises >12,000 participants in odd-one-out triplet judgments of object concepts. All datasets share a common stimulus space and a common embedding space (SPoSE: Sparse Positive Similarity Embedding) derived from behavior. The paper provides cross-modal RSA, decoding accuracy comparisons, and benchmarks for foundation models and DNNs. THINGS-data is currently the most-used cross-modal naturalistic-stimulus benchmark.

## Relevance to AGI

THINGS-data is **AGI's archetype**: shared stimuli + shared embedding space + multimodal recordings + open license. AGI's commons would generalize this from object images to dynamic narratives (Forrest Gump, HBN movies) and to richer annotation layers (HED Gen-3, scene graphs, narrative annotations). The SPoSE behavioral embedding is itself a layer of community-grade annotation; a model AGI can extend to other stimulus families.

## Notable details

- Stimuli: 1,854 concept categories, ~26,000 images
- fMRI: 3 subjects, ~22 hours each (deep sampling), 7T
- MEG: 4 subjects
- Behavioral: >12,000 participants, ~4.7M triplet judgments
- SPoSE embedding: 49-d sparse positive embedding from behavior
- BIDS-formatted; OpenNeuro deposit; permissive license

## Open questions / limitations

- Static images; does not extend to dynamic or narrative stimuli.
- Same-subject MEG-fMRI overlap is partial; full same-subject cross-modal coverage is the next frontier.
- SPoSE embedding is behavior-derived and powerful but does not include explicit HED-style annotations.
- Cross-language SPoSE replication needed (current behavior is English-speaking participants).
- Doesn't include EEG with the same images at scale; that gap was partly addressed by Hebart-related EEG releases (NOD-EEG).
- Cross-modality alignment with iEEG / single-unit data not yet realized.
- Per-image semantic annotations (HED) are not provided; AGI's commons could augment THINGS with HED layers.
- Subject demographics narrow; developmental and clinical THINGS extensions are pending.

## Citations

Primary BibTeX key: `hebart2023things`

Related works:
- Hebart et al. 2019; THINGS object concept database
- Allen et al. 2022 (NSD); analogous deep-sampling fMRI vision dataset
- Cichy et al. 2014; MEG-fMRI fusion methodology
- Gifford et al. 2022 (NOD-EEG); EEG counterpart to THINGS-fMRI
- LeBel et al. 2023; analogous pattern for language fMRI
