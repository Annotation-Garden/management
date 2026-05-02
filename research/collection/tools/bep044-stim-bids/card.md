---
slug: bep044-stim-bids
type: standard
strand: tools
year: 2025
authors: [BIDS Community]
venue: BIDS Extension Proposal (in preparation)
doi: null
url: https://github.com/bids-standard/bids-specification/pull/2022
license: CC-BY-4.0 (specification)
modalities: [image, audio, video, behavior]
tags: [BIDS, BEP044, Stim-BIDS, stimulus, annotation, HED, repository, FAIR]
agi_relevance: high
imported_from: null
added: 2026-04-30

pdf_status: not-applicable
pdf_path: null
md_path: source.md
md_quality: clean
---

## TL;DR

BEP044, also called Stim-BIDS, is the Brain Imaging Data Structure (BIDS) Extension Proposal that defines how to package stimulus repositories with their annotations as standalone BIDS-compliant datasets that other recording datasets can reference by stable identifier.

## Summary

Stim-BIDS extends BIDS so a "stimulus" is a first-class BIDS object rather than just a file living in `stimuli/` next to a brain recording. It specifies the folder layout (`stimuli/`, `annotations/<type>/events.tsv`, `dataset_description.json`), the rules for cross-referencing a stimulus from a recording dataset, and the integration points for Hierarchical Event Descriptors (HED) tagging. The proposal grew out of community discussions at OHBM and BrainHack around the duplicated effort of annotating naturalistic stimuli (Natural Scenes Dataset (NSD) images, Forrest Gump, Healthy Brain Network movies). It is under active review and expected to land in the BIDS 2.0 specification cycle.

## Relevance to AGI

Stim-BIDS is the schema that AGI's entire repository structure implements. Every annotation-garden GitHub repository for a stimulus collection follows the BEP044 layout, and AGI's value is precisely that it operationalizes this schema across many stimuli with shared tooling, validators, and review processes. Without Stim-BIDS, AGI would be inventing its own schema; with it, AGI inherits BIDS validators, BIDS-Apps, and the trust users already have in the BIDS ecosystem.

## Notable details

- Pull request 2022 on bids-standard/bids-specification (under review).
- Defines stable cross-referencing between recording datasets and stimulus repositories.
- HED tags carried in events.json sidecars.
- Compatible with DataLad sub-dataset linkage.
- Anticipated landing window: BIDS 2.0 cycle.

## Open questions / limitations

- Versioning semantics for stimuli that change post-publication are still under debate.
- Copyright-restricted stimuli (HBN movies, broadcast clips) need a federated pointer pattern not yet finalized.
- Cross-modality alignment (image + audio + behavioral rating) within a single stimulus is partly specified.
- No formal validator implementation as of April 2026.
- Participant / annotator metadata schema overlaps with HBM-Annotators and is not fully harmonized.

## Citations

Primary: `bep044stimbids`. Related:
- `gorgolewski2016bids`, base specification BEP044 extends.
- `robbins2021hed`, HED tagging used inside Stim-BIDS annotations.
- `markiewicz2021openneuro`, anticipated host archive for AGI Stim-BIDS repositories.
- `halchenko2021datalad`, distribution backend for stimulus sub-datasets.
- `delavega2022neuroscout`, analysis platform that consumes Stim-BIDS-style annotations.
