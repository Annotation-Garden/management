---
slug: finn2020-idiosynchrony
type: paper
strand: science
year: 2020
authors: [Finn, Glerean, Khojandi, Nielson, Molfese, Handwerker, Bandettini]
venue: NeuroImage
doi: 10.1016/j.neuroimage.2020.116828
url: https://doi.org/10.1016/j.neuroimage.2020.116828
license: publisher-paywall
modalities: [fmri]
tags: [individual-differences, isc, idiosynchrony, naturalistic, theme-3]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

Conceptual and empirical framework for *idiosynchrony*: the systematic individual-specific deviations from group inter-subject correlation (ISC) during naturalistic neuroimaging, providing a route from "shared response" to robust individual-difference markers.

## Summary

Finn and colleagues argue that the field's emphasis on group-level ISC has obscured an equally informative signal: the *residual* timecourse that is not shared. They propose computational approaches (subject-vs-group ISC asymmetries, subject-specific deviations from a shared response) and review evidence that idiosynchrony in default-mode and frontoparietal networks tracks personality, mood, comprehension, and clinical phenotypes. Naturalistic stimuli are uniquely positioned to elicit idiosynchrony because high-level cognition (memory, theory of mind, attention) varies across people viewing the same movie. The paper sets the agenda for using narrative stimuli as **functional probes** of individual differences instead of nuisance variability.

## Relevance to AGI

Idiosynchrony reframes the value of multi-perspective annotations: a single stimulus, when richly annotated (multi-layer events, semantics, social structure), becomes a **probe set** for any number of individual-difference questions. AGI's commons of canonical stimuli with stable annotation layers is the substrate that makes idiosynchrony analyses reproducible across labs and across populations (children in HBN, adults in NSD, clinical populations).

## Notable details

- Review + framework paper rather than primary data
- Distinguishes shared response, idiosynchrony, and noise
- Connects to Hasson 2010 reliability framework
- Provides analytical recipes (single-subject vs. group ISC, model-based residuals)
- Highlights default-mode network as key idiosynchrony hotspot

## Open questions / limitations

- Idiosynchrony measures depend on the stimulus; how to compare idiosynchrony across stimuli is unresolved.
- Doesn't formalize the link between annotation richness and recoverability of individual differences (a Theme 6 question).
- Idiosynchrony in clinical populations is largely undocumented; AGI's HBN-EEG commons is uniquely positioned to fill this gap.
- Without machine-actionable annotations, residual analyses can't be pinned to specific stimulus features.
- Test-retest reliability of idiosynchrony across stimuli is underexplored.
- Doesn't address how to scale idiosynchrony analyses across thousands of subjects (developmental cohorts).
- Cross-modal idiosynchrony (does a person's idiosynchrony pattern in fMRI match their EEG idiosynchrony pattern?) is open.
- Idiosynchrony has not been integrated with hyperalignment frameworks (do they cancel or complement?).

## Citations

Primary BibTeX key: `finn2020idiosynchrony`

Related works:
- Hasson et al. 2010; reliability and ISC review
- Finn & Bandettini 2021; predictive movie-fMRI features
- Vanderwal et al. 2017; naturalistic fMRI test-retest
- Chen et al. 2015; Shared Response Model
- Saggar et al. 2018; narrative individual differences via dynamic mappings
