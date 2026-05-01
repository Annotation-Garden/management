---
slug: zheng2022-cognitive-boundaries
type: paper
strand: science
year: 2022
authors: [Zheng, Schjetnan, Yebra, Gomes, Mosher, Saad, Willie, Goncalves, Rutishauser]
venue: Nature Neuroscience
doi: 10.1038/s41593-022-01020-w
url: https://www.nature.com/articles/s41593-022-01020-w
license: publisher-paywall
modalities: [single-unit, ieeg]
tags: [event-cells, hippocampus, single-unit, narrative-movie, episodic-memory, theme-4]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

First single-neuron evidence of "boundary cells" and "event cells" in the human medial temporal lobe (MTL): hippocampal and amygdala neurons selectively fire at cognitive event boundaries during naturalistic movie watching, structuring episodic memory.

## Summary

Zheng and colleagues recorded single-unit activity from microwires in 19 human epilepsy patients while they watched short film clips with annotated soft and hard event boundaries. They identified two functional classes of neurons: **boundary cells** that fire at any event boundary, and **event cells** that fire selectively for one type of boundary (e.g., scene change vs. story-arc shift). Neuronal firing predicted subsequent memory: clips with stronger boundary-cell responses were better remembered. The work directly tests the EST prediction at single-cell resolution and provides the rare bridge between cellular electrophysiology and naturalistic-stimulus paradigms.

## Relevance to AGI

The "Bang! You're Dead" / OpenNeuro ds004798 single-neuron paradigm referenced in the AGI white paper is closely related. AGI's pointer-based architecture for copyrighted clips, combined with HED-annotated event boundaries, would let labs replicate Zheng's boundary-cell analyses on shared stimuli. Foundation-model-driven event-boundary annotations could also be tested directly against single-cell event responses; a unique cross-stream validation between Strand A (tools/foundation models), Strand B (data), and Strand C (science).

## Notable details

- 19 human epilepsy patients, Macroelectrode + Behnke-Fried microwire recordings
- Movie clips with soft (sub-event) and hard (full event change) boundaries
- ~580 MTL neurons; ~6% boundary cells, ~3% event cells
- Boundary cells in hippocampus, amygdala, parahippocampal gyrus
- Predict subsequent memory with simple single-trial readout
- Distinguishes "soft" within-clip boundaries from "hard" between-clip boundaries

## Open questions / limitations

- Patient population (epilepsy) limits generalization to healthy populations.
- Sample size of identified cells is small; sub-categorization (boundary vs. event vs. mixed) needs replication.
- Stimulus annotations (soft/hard boundaries) are hand-coded; whether VLM-generated or HED-tagged annotations align with the same neurons is open.
- Doesn't dissociate sensory-driven (visual cuts) from cognitive-driven (semantic shifts) boundaries; subsequent work (Cohen 2022) addresses this.
- Cross-modality match (do fMRI HMM-discovered events line up with single-cell boundary firing?) is implied but not directly tested.
- Single-trial decoding accuracy is modest; how it scales with stimulus richness or annotation specificity is open.
- Doesn't use HED schema; AGI's HED-LANG / HED-Score libraries would provide a portable annotation layer.
- Memory readout uses recognition; cued recall and source memory not tested.

## Citations

Primary BibTeX key: `zheng2022neurons`

Related works:
- Baldassano et al. 2017; fMRI HMM events; Zheng tests at single-cell scale
- Ben-Yakov & Henson 2018; hippocampal "film editor"
- Cohen et al. 2024; semantic novelty modulation of event boundaries
- Berezutskaya et al. 2022; multimodal iEEG-fMRI dataset
- Aly et al. 2022; event boundaries and prediction error
