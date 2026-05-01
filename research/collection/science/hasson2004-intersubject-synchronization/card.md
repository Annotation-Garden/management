---
slug: hasson2004-intersubject-synchronization
type: paper
strand: science
year: 2004
authors: [Hasson, Nir, Levy, Fuhrmann, Malach]
venue: Science
doi: 10.1126/science.1089506
url: https://www.science.org/doi/10.1126/science.1089506
license: publisher-paywall
modalities: [fmri]
tags: [isc, naturalistic-movie, shared-response, theme-3]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

Founding inter-subject correlation (ISC) paper: 5 subjects watched 30 minutes of "The Good, the Bad and the Ugly" and showed widespread, time-locked BOLD synchrony across cortex, demonstrating that natural stimuli drive reproducible brain responses across people.

## Summary

Hasson and colleagues exploited the fact that any two brains exposed to the same naturalistic stimulus should produce correlated activity *if* the stimulus drives the response. They computed voxel-wise across-subject correlations of BOLD timeseries and found that more than 25% of cortex was significantly synchronized across the 5 subjects. The synchronized network covered visual, auditory, and higher-order regions and revealed a "naturalistic functional parcellation" of cortex. The paper established ISC as a model-free, feature-free alternative to encoding models; useful when stimulus annotations are unavailable or when the goal is to map regions that *are* stimulus-driven before annotating *what* drives them.

## Relevance to AGI

ISC is the mirror-image companion of annotation-driven encoding. Where encoding maps an annotation onto cortex, ISC maps cortex regions that respond reliably to *some* stimulus feature, motivating subsequent annotation. AGI's commons supports ISC analyses by providing canonical stimuli with verified time-locking metadata so any new lab can replicate the analysis. Crucially, the gap between ISC-mapped reliable cortex and encoding-model-explained cortex is exactly the residual that richer annotations can close.

## Notable details

- 5 subjects, 30-min movie segment ("The Good, the Bad and the Ugly")
- Voxel-wise Pearson correlation across pairs of subjects
- ~25-30% of cortex showed significant ISC
- Pre-Brain Imaging Data Structure (BIDS): no machine-actionable stimulus annotation
- Spawned the entire field of naturalistic neuroimaging

## Open questions / limitations

- 5 subjects, single film clip, single language (no audio in the analyzed window); generalization untested.
- ISC is **stimulus-locked synchrony**, not specific to any particular feature; doesn't decompose into "what" makes regions synchronize.
- Doesn't address what fraction of synchrony is sensory vs. semantic vs. narrative; later work (Lerner 2011, Honey 2012) tackled this with temporal scrambling.
- No annotation provenance: the stimulus was a copyrighted commercial film, foreshadowing AGI's pointer-based architecture for HBN movies.
- ISC saturates within ~5-10 subjects for some regions; data-scaling is asymmetric (Theme 6).
- Doesn't account for individual differences (idiosynchrony, Finn 2020 follow-up).
- Cannot dissociate stimulus-driven response from shared cognitive states (e.g., common surprise).

## Citations

Primary BibTeX key: `hasson2004intersubject`

Related works:
- Hasson et al. 2010; review consolidating ISC methodology
- Lerner et al. 2011; temporal hierarchy via stimulus scrambling
- Hasson et al. 2008; narrative comprehension and synchrony
- Finn et al. 2020 (idiosynchrony); individual differences from shared response
- Vanderwal et al. 2017; movies as test-retest functional connectivity probes
