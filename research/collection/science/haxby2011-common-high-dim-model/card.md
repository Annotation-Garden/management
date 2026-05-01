---
slug: haxby2011-common-high-dim-model
type: paper
strand: science
year: 2011
authors: [Haxby, Guntupalli, Connolly, Halchenko, Conroy, Gobbini, Hanke, Ramadge]
venue: Neuron
doi: 10.1016/j.neuron.2011.08.026
url: https://doi.org/10.1016/j.neuron.2011.08.026
license: publisher-paywall
modalities: [fmri]
tags: [hyperalignment, shared-representational-space, ventral-temporal, naturalistic-movie, theme-3]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-redistributable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

Foundational hyperalignment paper: a shared high-dimensional representational space across subjects' ventral-temporal cortex (VT), built from naturalistic-movie BOLD responses, in which fine-grained category structure is preserved and cross-subject decoding becomes possible.

## Summary

Haxby and colleagues developed hyperalignment, a Procrustes-style transformation that maps each subject's voxel-by-time matrix into a common high-dimensional response space. They used naturalistic movie viewing (Indiana Jones-class clips) as the alignment basis. Once aligned, classifiers trained on data from N-1 subjects accurately decode novel items in the held-out subject; demonstrating that VT cortex shares a common representational geometry across people, even though anatomical alignment is poor. The paper reframes the cross-subject problem from "matching anatomy" to "matching response geometry to a common stimulus." It established the alignment-via-naturalistic-stimulus paradigm that all later hyperalignment work (Guntupalli 2016, 2020) builds on.

## Relevance to AGI

Hyperalignment requires a shared, time-locked, naturalistic stimulus presented to all subjects; exactly the kind of canonical, well-annotated stimulus AGI's commons aims to host. As more datasets share canonical stimuli (NSD images, Forrest Gump, HBN movies), hyperalignment can scale population-level decoders without each lab re-recording an alignment dataset. AGI's annotation layers (HED, semantic embeddings) can also serve as the shared response basis itself ("model-based hyperalignment").

## Notable details

- 10 subjects watched Raiders of the Lost Ark (~2 hours)
- VT cortex aligned via Procrustes orthogonal transformation
- Common space dimension matches voxel count after alignment
- Cross-subject decoding of object categories outperforms anatomical alignment by large margin
- Released open-source PyMVPA implementation
- Spawned multi-paper hyperalignment program (searchlight, response-space, connectivity-based)

## Open questions / limitations

- Procrustes is global and orthogonal; later searchlight (Guntupalli 2016) and connectivity-based variants (Bazeille 2021) are more flexible but trade off sample efficiency.
- Alignment requires naturalistic stimulus exposure; what happens when subjects watch *different* movies (or movies in different languages) is open.
- VT cortex only; full-brain hyperalignment is more variable, especially in heteromodal regions.
- Doesn't directly model individual differences (residuals after alignment).
- The shared space is implicit; not annotated with semantic labels, making interpretability harder.
- Cross-modality alignment (fMRI ↔ MEG ↔ EEG via the same stimulus) is not addressed.
- How many minutes of shared stimulus are *needed* for high-quality alignment is not characterized; Theme 6 sufficiency question.

## Citations

Primary BibTeX key: `haxby2011common`

Related works:
- Haxby 2001; categorical pattern analysis foundation
- Guntupalli et al. 2016; searchlight hyperalignment
- Guntupalli et al. 2020; response-based vs connectivity-based hyperalignment review
- Chen et al. 2015; shared response model (alternative cross-subject framework)
- Feilong et al. 2018; individual differences after hyperalignment
