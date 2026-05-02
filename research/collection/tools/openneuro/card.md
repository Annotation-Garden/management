---
slug: openneuro
type: platform
strand: tools
year: 2021
authors: [Markiewicz, Gorgolewski, Feingold, Blair, Halchenko, Miller, Hardcastle, Wexler, Esteban, Goncavles, Jwa, Poldrack]
venue: eLife
doi: 10.7554/eLife.71774
url: https://openneuro.org
license: CC0 (datasets); MIT (code)
modalities: [fmri, mri, eeg, meg, ieeg, pet]
tags: [OpenNeuro, archive, BIDS, FAIR, BRAIN-Initiative, sharing, public-data]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

OpenNeuro is an open neuroscience data archive built on the Brain Imaging Data Structure (BIDS) standard that ingests, validates, and shares human neuroimaging datasets under a Creative Commons Zero (CC0) public-domain dedication.

## Summary

OpenNeuro descends from the OpenfMRI archive but pivots to BIDS-only ingestion, automated validation, and minimal restrictions on reuse (CC0 by default). The 2021 paper documents the archive's design principles, ingestion flow, integration with DataLad for distributed access, and case studies of dataset reuse leading to over 150 secondary publications. As of 2025 it hosts thousands of datasets covering fMRI, MRI, EEG, MEG, intracranial EEG, and Positron Emission Tomography (PET), with more than 20,000 unique participants. OpenNeuro is the de facto reference archive for BIDS-formatted human neuroimaging data and is tightly linked to BIDS-Apps, MRIQC, fMRIPrep, NeuroScout, NEMAR, and the Brain Initiative's broader open-data ecosystem.

## Relevance to AGI

OpenNeuro is the canonical destination for AGI-annotated derivatives. When an AGI stimulus repository ships an enriched events.tsv (with HED tags, annotation provenance, multi-rater agreement metrics) the natural endpoint is a corresponding OpenNeuro dataset that uses the enriched events. AGI does not host the brain-recording side; OpenNeuro does, and its tight integration with DataLad lets AGI link stimulus-side annotations to recording-side data through cryptographically stable identifiers. The CC0 licensing also informs AGI's own default license posture for derived annotation tables.

## Notable details

- CC0 default license for datasets; minimal restrictions on reuse.
- Automated BIDS validation on upload via the bids-validator.
- DataLad mirror provides versioned, distributed access.
- Supports modality extensions: MEG (Niso 2018), EEG (Pernet 2019), iEEG (Holdgraf 2019), PET (Norgaard 2021), Arterial Spin Labeling.
- Hundreds of secondary publications cited in the eLife paper.

## Open questions / limitations

- Storage and bandwidth costs scale with adoption; long-term funding model is grant-dependent.
- Dataset retraction or correction workflow is still maturing.
- No native support for stimulus-side artifacts beyond what BIDS provides.
- Search relies primarily on dataset descriptors; rich annotation-level search needs HED indexing.
- Privacy review is the contributor's responsibility; defacing and consent are not centrally enforced.

## Citations

Primary: `markiewicz2021openneuro`. Related:
- `gorgolewski2016bids`, input data standard.
- `halchenko2021datalad`, distribution backend.
- `delorme2022nemar`, sister archive for EEG/MEG/iEEG.
- `dandi2024`, sister archive for cellular neurophysiology.
- `wilkinson2016fair`, guiding principles.
