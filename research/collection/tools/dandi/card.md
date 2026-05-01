---
slug: dandi
type: platform
strand: tools
year: 2024
authors: [DANDI Team]
venue: BRAIN Initiative resource
doi: null
url: https://dandiarchive.org
license: BSD-3-Clause (software); CC-BY / CC0 (datasets, per asset)
modalities: [ephys, ophys, ieeg, behavior]
tags: [DANDI, archive, NWB, BIDS-iEEG, BRAIN-Initiative, versioned, neurophysiology]
agi_relevance: medium
imported_from: null
added: 2026-04-30

pdf_status: not-applicable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

DANDI (Distributed Archives for Neurophysiology Data Integration) is the BRAIN Initiative archive for cellular neurophysiology data, hosting Neurodata Without Borders (NWB) and Brain Imaging Data Structure (BIDS) datasets with versioning, programmatic access, and a hosted JupyterHub.

## Summary

DANDI provides per-dataset Digital Object Identifiers, programmatic access via the `dandi` Python client, and an in-browser DANDI Hub that lets users analyze data without local download. Native ingestion supports NWB plus growing coverage of BIDS-iEEG and BIDS-microscopy. The archive is the de facto destination for BRAIN Initiative-funded electrophysiology, two-photon imaging, voltage imaging, and intracranial human Electroencephalography (EEG) data. Software is BSD-licensed; dataset licenses are set by contributors and are typically CC-BY or CC0.

## Relevance to AGI

For stimuli that drive non-human or invasive recordings (rodent two-photon viewing of natural images, primate single-unit responses to movies, intracranial human EEG to naturalistic clips), DANDI is the response-side archive that AGI annotations need to interoperate with. The pattern is the same as for OpenNeuro: AGI hosts the stimulus plus annotations, DANDI hosts the recording, and a Stim-BIDS-style stable identifier links them. DANDI's NWB orientation also surfaces a concrete need for AGI: an events.tsv-to-NWB bridge so the same annotations can travel with both BIDS recordings and NWB recordings.

## Notable details

- Native NWB plus growing BIDS-iEEG and BIDS-microscopy support.
- DANDI Hub provides hosted JupyterHub for in-browser analysis.
- Per-version DOIs.
- Integrates with NeuroConv, NWB Inspector, NWB GUIDE for ingestion.
- Backed by NIH BRAIN Initiative; hundreds of datasets as of 2026.

## Open questions / limitations

- Storage scaling depends on continued BRAIN Initiative funding.
- Annotation-side data (HED tags on stimuli) is not yet a first-class search facet.
- Licensing heterogeneity across datasets complicates redistributable analysis.
- Cross-archive provenance with OpenNeuro and NEMAR is informal.
- Bandwidth costs for very large two-photon datasets stress the in-browser model.

## Citations

Primary: `dandi2024`. Related:
- `rubel2022nwb`, primary data language hosted on DANDI.
- `markiewicz2021openneuro`, sister archive for human imaging.
- `delorme2022nemar`, sister archive for neuroelectromagnetic data.
- `halchenko2021datalad`, alternative versioned distribution.
- `wilkinson2016fair`, guiding principles.
