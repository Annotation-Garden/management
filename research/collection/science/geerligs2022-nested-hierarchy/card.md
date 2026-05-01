---
slug: geerligs2022-nested-hierarchy
type: paper
strand: science
year: 2022
authors: [Geerligs, van Gerven, Güçlü]
venue: eLife
doi: 10.7554/eLife.77430
url: https://elifesciences.org/articles/77430
license: CC-BY
modalities: [fmri]
tags: [event-segmentation, neural-states, narrative, cortical-hierarchy, theme-4]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

A multi-scale segmentation analysis of fMRI from naturalistic narrative viewing finds a **partially nested cortical hierarchy of neural states**: events at higher levels of cortex are not strict supersets of lower-level events, complicating the classical strict-hierarchy view of event structure.

## Summary

Geerligs and colleagues extend Baldassano-style HMM segmentation across multiple cortical regions and show that the nesting of neural events is only **partial**: a higher-region boundary frequently lacks a corresponding lower-region boundary, and vice versa. They formalize this with a "boundary alignment" metric and test alternative hierarchical models. The result challenges the strict hierarchical TRW view, suggesting that event boundaries are domain-specific and that different feature dimensions (visual, semantic, social) drive boundaries in different regions. They release tooling and apply it to the Cam-CAN naturalistic dataset, showing event timescales scale with cortical hierarchy but with substantial cross-region heterogeneity.

## Relevance to AGI

Partially nested events imply that **multi-perspective annotations** are not redundant; different annotation layers (cuts, dialogue, semantic shifts, character actions) drive boundaries in different cortical regions. AGI's mission to host **multilayer, versioned annotation sidecars** for canonical stimuli is exactly the data substrate needed to test which annotations match which cortical regions. The paper also makes a sufficiency argument: with too few annotation perspectives, the inferred neural hierarchy will appear strictly nested simply because the analysis lacks resolution.

## Relevance to AGI (continued)

For Phase 2/3 of AGI, partially nested events frame the **annotation-response curve** question: as annotation richness grows, does the cortical event mosaic become finer-grained and less hierarchical? Strand C cards on Theme 6 (Antonello, LeBel, Naspi) intersect this question at the encoding-model level.

## Notable details

- Open-access eLife with code and data
- Multiple naturalistic datasets including Cam-CAN
- Boundary-alignment metric: how well boundaries in one region predict boundaries in another
- Event timescales increase with cortical hierarchy but with non-trivial heterogeneity
- Partial nesting holds across stimulus types

## Open questions / limitations

- Cortex-only; subcortical (hippocampus, striatum) event structure complementary but separately analyzed.
- HMM assumes Markov state transitions; richer dynamics (continuous evolution) not addressed.
- Doesn't link partial nesting to specific stimulus features (no annotation-driven decomposition).
- Cam-CAN is older (2014-era) acquisition; replication with high-temporal-resolution data (e.g., 7T, multiband) is needed.
- Doesn't quantify how the partial-nesting metric scales with stimulus richness or annotation depth.
- Cross-modality (fMRI ↔ MEG ↔ iEEG) partial nesting is open.
- Cross-cultural/developmental generalization not addressed.
- Doesn't characterize subject-level idiosyncratic deviation in event nesting.

## Citations

Primary BibTeX key: `geerligs2022partially`

Related works:
- Baldassano et al. 2017; HMM event segmentation foundation
- Zacks 2007; Event Segmentation Theory
- Lerner et al. 2011; TRW hierarchy that partial-nesting complicates
- Cam-CAN consortium; Shafto et al. 2014; dataset used
- Cohen & Hasson 2024; event-boundary semantic novelty work
