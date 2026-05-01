---
slug: guntupalli2020-hyperalignment
type: paper
strand: science
year: 2020
authors: [Guntupalli, Feilong, Haxby]
venue: eLife
doi: 10.7554/eLife.56601
url: https://elifesciences.org/articles/56601
license: CC-BY
modalities: [fmri]
tags: [hyperalignment, idiosyncratic-topography, shared-response, naturalistic-movie, theme-3]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Definitive hyperalignment review and unified model: idiosyncratic cortical topographies hide a shared information geometry that can be recovered through response-based or connectivity-based hyperalignment, with measurable improvements over anatomical alignment for both decoding and individual-difference analyses.

## Summary

Guntupalli and colleagues unify the two main hyperalignment families. **Response-based hyperalignment** (RHA) requires subjects to watch the same movie and uses time-locked BOLD trajectories to find a shared space. **Connectivity-based hyperalignment** (CHA) instead aligns subjects via similar functional connectivity profiles, enabling alignment without a shared stimulus. They formalize a single mathematical framework, evaluate both on naturalistic movie data and resting-state, and characterize the shared space across cortex. The paper systematically compares decoding accuracy, ISC, and individual-difference recovery and provides best-practice recommendations: RHA when shared stimulus is available; CHA for legacy datasets without it. Shows that, after hyperalignment, individual differences in cortical patterns become much more reliable indicators of phenotype.

## Relevance to AGI

The dichotomy between RHA and CHA maps directly onto AGI's federation problem: how do we align subjects across sites that may not have shared stimuli? AGI's commons offers RHA via canonical stimuli (NSD, Forrest Gump, HBN movies) and CHA via shared resting-state datasets. Hyperalignment also defines a "minimum viable annotation": the shared stimulus itself, even without per-frame tags. Combining hyperalignment with AGI's annotation layers (events, semantics, foundation-model embeddings) is a natural Phase 2/3 direction.

## Notable details

- Open-source eLife review with mathematical unification
- Procrustes / orthogonal vs. linear / non-orthogonal variants compared
- Searchlight implementation (per-region alignment) preserves topography
- Connectivity-based hyperalignment uses correlation profiles as features
- Demonstrated on Studyforrest, Raiders, resting-state datasets
- Code in PyMVPA and Python re-implementations

## Open questions / limitations

- Hyperalignment is post-hoc and lossy; a learned end-to-end alignment (e.g., contrastive deep nets) might recover more variance.
- Doesn't address cross-modality alignment (fMRI to MEG, EEG, iEEG).
- Connectivity-based hyperalignment depends on parcellation choices.
- Doesn't quantify how alignment quality scales with stimulus duration / TRs available; Theme 6 sufficiency.
- Shared space is opaque; mapping its dimensions back to interpretable annotations is open.
- Doesn't formally treat alignment in the presence of clinical heterogeneity (e.g., aphasia, autism), where idiosyncratic topographies may be informative rather than nuisance.
- Cross-language hyperalignment (subjects watching dubbed Forrest Gump in different languages) is unaddressed.
- The interaction between hyperalignment and downstream encoding-model fitting (does hyperalignment first improve subsequent encoding?) is not formally characterized.

## Citations

Primary BibTeX key: `guntupalli2020hyperalignment`

Related works:
- Haxby et al. 2011; original hyperalignment
- Guntupalli et al. 2016; searchlight hyperalignment
- Bazeille et al. 2021; fast linear hyperalignment alternatives
- Chen et al. 2015; Shared Response Model (SRM)
- Feilong et al. 2018; individual differences in shared-space topography
