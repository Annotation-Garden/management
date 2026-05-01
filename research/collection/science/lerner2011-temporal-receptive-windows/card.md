---
slug: lerner2011-temporal-receptive-windows
type: paper
strand: science
year: 2011
authors: [Lerner, Honey, Silbert, Hasson]
venue: Journal of Neuroscience
doi: 10.1523/JNEUROSCI.3684-10.2011
url: https://www.jneurosci.org/content/31/8/2906
license: publisher-paywall
modalities: [fmri]
tags: [temporal-receptive-window, isc, narrative-scrambling, hierarchy, theme-3]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: abstract-only
---

## TL;DR

Time-scrambled narrative experiment that identifies a topographic hierarchy of temporal receptive windows: early sensory areas integrate over seconds, intermediate areas over sentences, and high-order regions only synchronize when the full multi-minute narrative is intact.

## Summary

Lerner and colleagues had subjects listen to a story presented in four temporal granularities: intact, paragraphs scrambled, sentences scrambled, words scrambled. Voxel-wise inter-subject correlation (ISC) was computed for each version. Early auditory cortex synchronized regardless of scrambling (short receptive window), associative auditory regions synchronized when sentences were intact (middle window), and the temporoparietal junction, precuneus, and medial prefrontal cortex synchronized only with the full narrative (long, multi-minute window). The result formalized the **temporal receptive window hierarchy** (TRW): cortex is organized along a temporal-integration gradient akin to spatial-receptive-field hierarchies in vision.

## Relevance to AGI

A TRW gradient implies that annotation granularity must match the analysis target: phoneme-level annotations probe early auditory cortex, sentence-level probe intermediate cortex, narrative-level (events, schemas) probe high-order regions. AGI's HED Gen-3 onset/offset/inset structure naturally encodes this multi-scale annotation, letting downstream encoding/ISC analyses choose the right temporal resolution. Moreover, narrative-level synchrony is exactly the regime where richer annotations (event boundaries, character relations, semantic novelty) yield the most analytic value.

## Notable details

- 7-minute audio narrative ("Pie-Man" by Jim O'Grady)
- 4 conditions: intact, paragraph-scrambled, sentence-scrambled, word-scrambled
- 36 subjects total across conditions
- Voxel-wise ISC compared across conditions
- TRW hierarchy: early auditory < belt areas < lateral temporal < parietal < default-mode network

## Open questions / limitations

- Single language, single narrative; cross-cultural generalization untested.
- Auditory only; visual-narrative TRW hierarchy mapped later (Hasson 2008, Honey 2012).
- TRW is operationally defined by scrambling; doesn't decompose into specific narrative features (events, characters, plot).
- No annotation layer: cannot say *which* features drive the long-TRW synchrony.
- Doesn't address whether TRW depth is genetic, learned, or task-modulated.
- Pre-event-segmentation framework: the TRW gradient was later refined into discrete event-state hierarchies (Geerligs 2022, Baldassano 2017).
- Cross-modal TRW (audio vs. text vs. video of the same narrative) not addressed; rich AGI commons could test this directly.

## Citations

Primary BibTeX key: `lerner2011topographic`

Related works:
- Hasson et al. 2008; early TRW evidence with movies
- Honey et al. 2012; TRW in language vs. narrative
- Baldassano et al. 2017; event-state segmentation extending TRW into discrete events
- Geerligs et al. 2022; partially nested cortical hierarchy of neural states
- Chang et al. 2022; narrative engagement and TRW in default-mode network
