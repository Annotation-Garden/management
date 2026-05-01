---
slug: baldassano2017-event-structure
type: paper
strand: science
year: 2017
authors: [Baldassano, Chen, Zadbood, Pillow, Hasson, Norman]
venue: Neuron
doi: 10.1016/j.neuron.2017.06.041
url: https://doi.org/10.1016/j.neuron.2017.06.041
license: publisher-paywall
modalities: [fmri]
tags: [event-segmentation, hidden-markov-model, narrative, hippocampus, theme-4]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

A hidden Markov model (HMM) over BOLD timecourses discovers a **nested cortical hierarchy of event boundaries** during narrative perception, with longer events in higher-order regions and event-locked hippocampal responses linking perception to memory.

## Summary

Baldassano and colleagues fit an HMM to fMRI BOLD activity from subjects watching a narrative film and listening to its audio description. The HMM segments brain timecourses into discrete event states without any external annotation. They find that early visual areas have many short events while higher-order areas (parietal, default-mode network) have fewer, longer events; a TRW-style hierarchy in the time domain. Crucially, hippocampal activity *increases at event boundaries*, predicts subsequent memory recall, and reactivates earlier event representations. The paper unites event segmentation theory (EST) with a concrete, model-based, cortex-wide segmentation method and connects it to memory encoding.

## Relevance to AGI

This paper is the methodological backbone for **automated event annotation**: an HMM applied to brain activity alone discovers events, which can then be linked to behavioral annotations or VLM-derived stimulus features. AGI's commons stimuli with multilayer annotations (visual cuts, semantic boundaries, character changes) become test sets for the HMM-discovered events. The hippocampal-boundary finding also motivates a Phase 2/3 hypothesis: if AGI provides versioned event annotations, downstream studies can quantify *which* annotation layer best predicts the hippocampal boundary signal.

## Notable details

- HMM with state-transition prior, fit to BOLD timecourses
- 17 subjects watching a 50-min Sherlock episode and listening to its description
- Cross-subject consistency of discovered events at multiple timescales
- Hippocampus activates at event ends and predicts memory recall
- Code released; widely re-used (Geerligs 2022, Cohen 2022, others)

## Open questions / limitations

- HMM assumes piecewise-stationary states; soft transitions and overlapping events are not modeled.
- Single narrative film; cross-narrative generalization of the discovered hierarchy untested.
- Doesn't decompose into stimulus features that drive event boundaries (visual cuts, semantic shifts).
- Discovers events from brain data alone; does not validate against multi-perspective stimulus annotations (future AGI work).
- Pre-foundation-model: no comparison to event boundaries proposed by VLM/LLM annotations of the stimulus.
- Memory follow-up uses simple recall metrics; richer memory probes would test the boundary-recall link more deeply.
- Hippocampal effect pooled across regions; sub-field specificity (CA1, CA3, DG) not addressed without intracranial data.
- Cross-modality generalization (does the same HMM fit yield the same events for the silent-film vs. audio-description?) shown qualitatively but not quantified rigorously.

## Citations

Primary BibTeX key: `baldassano2017discovering`

Related works:
- Zacks 2007; Event Segmentation Theory
- Geerligs et al. 2022; partially nested neural-state hierarchy refining the HMM approach
- Ben-Yakov & Henson 2018; hippocampal film-editor for movie boundaries
- Chen et al. 2017; Sherlock dataset that this paper uses
- Antony et al. 2021; event-segmentation memory consequences
