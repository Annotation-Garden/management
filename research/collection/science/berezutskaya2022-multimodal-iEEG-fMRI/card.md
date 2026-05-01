---
slug: berezutskaya2022-multimodal-iEEG-fMRI
type: paper
strand: science
year: 2022
authors: [Berezutskaya, Vansteensel, Aarnoutse, Freudenburg, Piantoni, Branco, Ramsey]
venue: Scientific Data
doi: 10.1038/s41597-022-01173-0
url: https://www.nature.com/articles/s41597-022-01173-0
license: CC-BY
modalities: [ieeg, fmri]
tags: [iEEG-fMRI, naturalistic-movie, dataset, cross-modal, theme-7]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

Open multimodal dataset (OpenNeuro ds003688) with iEEG and fMRI recorded from the same epilepsy patients (and a healthy fMRI cohort) watching a short audiovisual film, enabling fine-grained iEEG-fMRI alignment on a shared naturalistic stimulus.

## Summary

Berezutskaya and colleagues released an open dataset combining intracranial EEG (51 patients) and fMRI (30 healthy adults, 21 patients) collected on the same audiovisual film clip ("La Linea Gialla", a ~6-minute Pixar-style short). The data are BIDS-formatted, with annotations of scene cuts, dialogue, and event boundaries provided. The paper outlines example analyses: cross-modal RSA, broadband-gamma-fMRI alignment, and event-locked responses. The dataset is the canonical reference for iEEG-fMRI alignment on shared naturalistic stimuli and is referenced extensively in the AGI vision (white paper, Strand B data brief).

## Relevance to AGI

This is the **single best demonstration** of AGI's federated, multimodal data thesis. Patients and healthy adults watching the same stimulus, with shared BIDS annotations, allows millisecond-resolution iEEG to be aligned to BOLD spatial maps. The companion movie-annotation file (Figshare) is a multilayer annotation set; exactly the format AGI proposes to standardize via HED Gen-3. Future work can layer foundation-model annotations (VLM scene descriptions, CLIP embeddings) on top of the existing shared stimulus.

## Notable details

- iEEG: 51 epilepsy patients with subdural grids and depth electrodes
- fMRI: 30 healthy + 21 patient adults
- Stimulus: ~6.5-min audiovisual film clip
- Multilayer annotations: cuts, scenes, dialogue, language onset/offset
- BIDS-formatted, OpenNeuro ds003688 + figshare annotation files
- Sister dataset ds004798 adds single-unit microwire data on a different clip ("Bang! You're Dead")

## Open questions / limitations

- Single short clip; longer narrative (Forrest Gump-scale) cross-modal datasets remain rare.
- Patient population introduces clinical confounds (anti-epileptic drugs, surgical context).
- Annotations are useful but not yet HED-tagged; converting to a portable HED layer is an open AGI deliverable.
- Cross-subject iEEG alignment is hard because electrode coverage varies; per-electrode statistics dominate.
- Doesn't include MEG or scalp EEG for the same stimulus; cross-recording-modality fusion (iEEG + MEG + fMRI) on shared narrative is a future need.
- Sample sizes per modality are modest by ML standards; aggregating with similar datasets is needed for foundation-model-grade analyses.
- Eye-tracking and pupillometry were not collected; attentional confounds cannot be modeled.
- Reference to standardized stimulus distribution (DOI for the actual film file) is informal; AGI's pointer-based architecture (white paper) is the natural solution.

## Citations

Primary BibTeX key: `berezutskaya2022multimodal`

Related works:
- Cichy et al. 2014; early MEG-fMRI fusion methodology
- Hebart et al. 2023 (THINGS-data); multimodal large-scale benchmark
- Hermes et al. 2017 (eLife); ECoG-fMRI BOLD relationship
- Ratajczak et al. 2025 (forthcoming); iEEG NSD extension
- Wagner et al. 2019 (OHBM); Forrest Gump empirical iEEG-fMRI contrasts
