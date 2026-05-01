---
slug: bids-spec
type: standard
strand: tools
year: 2016
authors: [Gorgolewski, Auer, Calhoun, Craddock, Das, Duff, Flandin, Ghosh, Glatard, Halchenko, Handwerker, Hanke, Keator, Li, Michael, Maumet, Nichols, Nichols, Pellman, Poline, Rokem, Schaefer, Sochat, Triplett, Turner, Varoquaux, Poldrack]
venue: Scientific Data
doi: 10.1038/sdata.2016.44
url: https://www.nature.com/articles/sdata201644
license: CC-BY-4.0
modalities: [fmri, mri, dwi, eeg, ieeg, meg, pet, behavior, physio]
tags: [BIDS, standard, neuroimaging, file-format, metadata, JSON, TSV, NIfTI, FAIR]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: archived
pdf_path: source.pdf
md_path: source.md
md_quality: clean
---

## TL;DR

The Brain Imaging Data Structure (BIDS) is a community-driven specification for organizing, naming, and describing neuroimaging datasets, designed around plain text formats (NIfTI, JSON, TSV) and lightweight folder conventions that enable automated validation, sharing, and pipelining.

## Summary

BIDS replaces lab-specific data layouts with a single standard that captures the metadata required to reanalyze a dataset without contacting the original investigators. Filenames encode entities (subject, session, task, run, acquisition) as key-value pairs and end in a known suffix; companion JSON sidecars carry acquisition parameters; events.tsv files describe stimulus and response timing. The 2016 paper formalized version 1.0.0 covering structural, diffusion, and functional Magnetic Resonance Imaging (MRI), with an extensibility pathway through BIDS Extension Proposals (BEPs) that has since added Magnetoencephalography (MEG), Electroencephalography (EEG), intracranial EEG (iEEG), Positron Emission Tomography (PET), and other modalities. BIDS underpins the BIDS-Apps ecosystem, OpenNeuro, NEMAR, and most modern neuroimaging pipelines.

## Relevance to AGI

BIDS, and specifically the events.tsv plus sidecar JSON pattern, is the substrate on which the Annotation Garden Initiative (AGI) builds. Every stimulus annotation that AGI distributes (visual saliency, scene boundaries, emotion ratings, Hierarchical Event Descriptors (HED)) lands in a BIDS-compatible events.tsv so it can be ingested by existing analysis tools without bespoke parsing. AGI's Stim-BIDS (BEP044) extension explicitly extends this specification into the stimulus repository case, where the canonical artifact is the stimulus plus its annotations rather than the brain recording.

## Notable details

- File formats: NIfTI for imaging, JSON for metadata, TSV for tabular data.
- Inheritance principle: metadata defined at higher folder levels propagate down unless overridden.
- A reference Python and JavaScript validator enforces the spec (bids-validator).
- Adopted by OpenNeuro, OpenfMRI legacy datasets, ABIDE, ADHD-200, and others.
- Uses Cognitive Atlas and Cognitive Paradigm Ontology for task vocabulary linkage.

## Open questions / limitations

- The original spec did not cover stimuli as first-class objects; this is the gap Stim-BIDS (BEP044) addresses.
- Inheritance can hide misconfigured metadata when sidecars at multiple levels conflict.
- Tabular events.tsv has no native cross-study schema; HED was added later to fill that gap.
- Validation focuses on structural conformance, not semantic correctness of annotation content.
- Versioning of the spec itself is not yet captured inside dataset_description.json in a machine-actionable way.

## Citations

Primary: `gorgolewski2016bids`. Related:
- `markiewicz2021openneuro` — primary archive built on BIDS.
- `halchenko2021datalad` — BIDS datasets distributed as DataLad super-datasets.
- `robbins2021hed` — HED layered on top of BIDS events.
- `bep044stimbids` — Stim-BIDS extension for stimulus repositories.
- `esteban2019fmriprep` — flagship BIDS-App.
