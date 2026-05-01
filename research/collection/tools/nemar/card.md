---
slug: nemar
type: platform
strand: tools
year: 2022
authors: [Delorme, Truong, Youn, Sivagnanam, Stirm, Yoshimoto, Poldrack, Majumdar, Makeig]
venue: Database (Oxford)
doi: 10.1093/database/baac096
url: https://nemar.org
license: CC-BY-NC
modalities: [eeg, meg, ieeg]
tags: [NEMAR, archive, EEG, MEG, iEEG, BIDS, HED, OpenNeuro, NSG, supercomputer]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

NEMAR (Neuroelectromagnetic Data Archive and Tools Resource) is a web gateway that exposes Brain Imaging Data Structure (BIDS)-formatted Electroencephalography (EEG), Magnetoencephalography (MEG), and intracranial EEG (iEEG) datasets from OpenNeuro, layered with quality reports and a direct path to high-performance computing through the Neuroscience Gateway (NSG).

## Summary

NEMAR was built at the University of California San Diego as a complement to OpenNeuro for neuroelectromagnetic data. It indexes OpenNeuro EEG/MEG/iEEG datasets, computes per-dataset visual quality and Hierarchical Event Descriptor (HED) tag summaries, and provides an in-browser data explorer. Crucially, NEMAR connects directly to the San Diego Supercomputer Center via NSG, letting researchers launch EEGLAB or MNE-Python pipelines on shared data without local download. The 2022 Database paper documents the architecture, BIDS ingestion, HED-tag-aware search, and the design rationale for being the first archive built around HED as a primary data-discovery key.

## Relevance to AGI

NEMAR is the most directly aligned existing platform with AGI's vision for stimulus-anchored neuroelectromagnetic data. AGI annotations (HED tags, scene boundaries, speech envelopes) become first-class search facets in NEMAR if AGI commits to publishing them in BIDS-EEG-compatible events.tsv form. The HBN-EEG and the NeurIPS EEG Competition datasets that AGI plans to support already live in NEMAR, so AGI's role can be to enrich rather than mirror them. NEMAR's NSG link also gives AGI a near-zero-friction compute path for benchmarking new annotations against shared EEG datasets.

## Notable details

- Built on top of OpenNeuro; ingests BIDS-EEG, BIDS-MEG, BIDS-iEEG datasets automatically.
- First archive to use HED tags as a primary discovery facet.
- Direct integration with NSG for free supercomputer access.
- Hosts hundreds of datasets covering tens of thousands of recording sessions.
- Co-led by maintainers of EEGLAB, OpenNeuro, BIDS-EEG, and HED.

## Open questions / limitations

- NEMAR-specific quality metrics are EEG-focused; MEG and iEEG QC is less mature.
- Search depends on contributors having tagged events with HED; un-tagged datasets are less discoverable.
- NSG-routed compute has queue waits during peak demand.
- API for programmatic access is still evolving.
- Long-term funding model is grant-dependent.

## Citations

Primary: `delorme2022nemar`. Related:
- `markiewicz2021openneuro`, upstream archive.
- `delorme2004eeglab`, primary analysis toolbox routed via NSG.
- `gorgolewski2016bids`, input data standard.
- `robbins2021hed`, vocabulary that powers NEMAR search.
- `halchenko2021datalad`, alternative distribution path for the same datasets.
