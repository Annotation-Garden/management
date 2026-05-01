---
slug: hasson2010-reliability
type: paper
strand: science
year: 2010
authors: [Hasson, Malach, Heeger]
venue: Trends in Cognitive Sciences
doi: 10.1016/j.tics.2009.10.011
url: https://doi.org/10.1016/j.tics.2009.10.011
license: publisher-paywall
modalities: [fmri]
tags: [reliability, isc, naturalistic, review, theme-3]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

Conceptual review framing **response reliability** (within-subject and across-subject) as a complementary axis to response amplitude for analyzing naturalistic neuroimaging; the methodological backbone of the ISC literature.

## Summary

Hasson, Malach, and Heeger argue that reliability; how reproducibly a region responds to the same stimulus; is a separate dimension from response amplitude and reveals different cortical organization. Within-subject reliability (test-retest of the same stimulus) and across-subject reliability (ISC) both segregate cortex into networks that mirror functional specialization. The paper consolidates a decade of natural-vision and natural-listening work, lays out the analytical pipeline (correlation-based, time-locked metrics), and distinguishes phenomena that response-amplitude analyses miss. It is the most cited methodological touchstone for naturalistic neuroimaging.

## Relevance to AGI

Reliability metrics are model-free: they require only a shared stimulus, not a shared annotation. This makes them the natural first analysis on any new AGI commons stimulus, before annotation-driven encoding. AGI's commons gives reliability analyses scale (thousands of subjects, dozens of stimuli) and reproducibility (versioned stimulus + standardized preprocessing).

## Notable details

- Review of within-subject and between-subject reliability
- Both auditory and visual literature covered
- Reliability vs. amplitude dissociation framework
- Establishes ISC as a community standard analysis
- Methodological recommendations: time-locking, scrambling, control conditions

## Open questions / limitations

- Reliability is feature-agnostic; doesn't tell us *what* a reliable region is responding to.
- Single-modality (fMRI); cross-modal reliability mapping is unresolved.
- Doesn't address modern individual-difference frameworks (Finn 2020 idiosynchrony).
- Pre-foundation-model: doesn't anticipate using reliability as a noise ceiling for encoding-model R^2.
- Doesn't formalize how reliability scales with stimulus length, subject count, or annotation richness.
- Test-retest reliability for naturalistic stimuli over months/years (longitudinal stability) is underexplored.
- Limited treatment of clinical and developmental populations where reliability itself may be a phenotype.

## Citations

Primary BibTeX key: `hasson2010reliability`

Related works:
- Hasson et al. 2004; origin of ISC
- Lerner et al. 2011; TRW hierarchy via temporal scrambling
- Vanderwal et al. 2017; test-retest reliability of naturalistic fMRI
- Finn et al. 2020; idiosynchrony framework
- Pajula & Tohka 2014; voxel-wise ISC reliability methods
