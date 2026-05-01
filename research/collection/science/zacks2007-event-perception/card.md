---
slug: zacks2007-event-perception
type: paper
strand: science
year: 2007
authors: [Zacks, Speer, Swallow, Braver, Reynolds]
venue: Psychological Bulletin
doi: 10.1037/0033-2909.133.2.273
url: https://doi.org/10.1037/0033-2909.133.2.273
license: publisher-paywall
modalities: [behavior, fmri]
tags: [event-segmentation-theory, event-boundaries, prediction-error, theory, theme-4]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

Foundational statement of Event Segmentation Theory (EST): perception of activity is automatically partitioned into discrete events at moments of high prediction error, governed by a working "event model" that the brain updates whenever the predictive failure exceeds threshold.

## Summary

Zacks and colleagues unify behavioral, neuroimaging, and computational work into Event Segmentation Theory: the brain maintains active **event models** (representations of the current "what's happening") that generate predictions about upcoming sensory input. When predictions fail systematically, the model is updated and a behavioral / neural **event boundary** is registered. The theory explains why people agree on where event boundaries occur in continuous activities (movies, narratives), why memory chunks at boundaries, and why prediction-error signals (in cortex and in working memory) align with subjective boundaries. The paper also connects to brain regions: lateral prefrontal cortex, posterior temporal cortex, and parahippocampal gyrus respond at boundaries. EST is the conceptual framework that all later neural-event-segmentation work (Baldassano 2017, Geerligs 2022, Zheng 2022) operationalizes.

## Relevance to AGI

EST is a theoretical justification for event-level annotations on naturalistic stimuli. AGI's HED Gen-3 onset/offset/inset design directly encodes event-process structure; event annotations on canonical stimuli (Forrest Gump, HBN movies) become testable predictions for EST. Furthermore, AGI's vision of foundation-model-assisted annotation can be evaluated against human event boundaries; does a video LLM segment events the way humans do?

## Notable details

- Synthesis of cognitive psychology, computational modeling, and neuroimaging
- Key prediction: boundaries occur when predictive error exceeds threshold
- Behavioral signature: subjects spontaneously segment continuous activity into nested events
- Neural signature: increased BOLD at boundaries in prefrontal, temporal, and medial-temporal regions
- Hierarchical event structure (fine vs. coarse boundaries) is a core claim

## Open questions / limitations

- EST is a verbal theory; quantitative formalization came much later (Reynolds 2007, Baldassano 2017 HMM-style models).
- Pre-foundation-model: doesn't operationalize "prediction error" in modern Vision-Language-Model terms.
- Event hierarchy is asserted but not anatomically mapped at fine granularity (later work, Geerligs 2022).
- Doesn't address cross-modal event boundaries (audio vs. visual vs. semantic; open AGI commons question).
- Cross-cultural and developmental generalization of event boundaries underexplored.
- Doesn't engage with HED-style annotation standards (which were not yet developed).
- Difficult to test in clinical populations because subjective boundary judgments may differ.
- Doesn't quantify how many subjects' boundary judgments are needed for a stable consensus annotation.

## Citations

Primary BibTeX key: `zacks2007event`

Related works:
- Reynolds, Zacks & Braver 2007; computational EST model
- Speer et al. 2009; fMRI of reading-event boundaries
- Baldassano et al. 2017; HMM-style neural event segmentation
- Geerligs et al. 2022; partially nested cortical hierarchy of events
- Zacks 2020 (Annu Rev Psychol); updated review
